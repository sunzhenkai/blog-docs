---
title: python - coroutines
categories: 
	- [python, notes]
tags:
	- python
date: 2021/06/05 00:00:00
---

# 协程

由程序负责任务切换，可以减少线程/进程上下文切换的消耗。用户态实现任务切换，无需进入内核态。

# 用途

虽然 Python 有多线程的概念，但是由于 GIL 的存在，并不能利用多核资源。如果易不能充分利用单进程资源，可能会带来严重的性能问题。

# 示例

## 定时器

下面是使用协程实现的定时器。

```python
# coding: utf-8
import asyncio
import threading
import time
from datetime import datetime
from typing import Callable


class Scheduler:
    cache: set[str] = set()

    @classmethod
    async def _do_schedule(cls, name: str, delay: int, interval: int, cb: Callable, args, kwargs):
        await asyncio.sleep(delay)
        while name in cls.cache:
            try:
                cb(*args, **kwargs)
            except Exception as e:
                print('execute target failed, e=', e)
            await asyncio.sleep(interval)

    @classmethod
    def _schedule_wrapper(cls, name: str, delay: int, interval: int, cb: Callable, args, kwargs):
        asyncio.run(cls._do_schedule(name, delay, interval, cb, args, kwargs))

    @classmethod
    def schedule(cls, name: str, delay: int, interval: int, cb: Callable, *args, **kwargs):
        assert name not in cls.cache, 'duplicate scheduler with name ' + name
        threading.Thread(target=cls._schedule_wrapper,
                         args=(name, delay, interval, cb, args, kwargs),
                         daemon=True).start()

        cls.cache.add(name)

    @classmethod
    def stop(cls, name: str):
        if name in cls.cache:
            cls.cache.remove(name)


def cbk(a, b, c):
    print('execute at', datetime.now(), 'with args:', (a, b, c))


if __name__ == '__main__':
    Scheduler.schedule('first', 1, 1, cbk, 'a', 'b', c='c')
    Scheduler.schedule('second', 1, 1, cbk, 'd', 'e', c='f')
    time.sleep(3)
    Scheduler.stop('first')
    try:
        while True:
            pass
    except KeyboardInterrupt:
        pass
```

# 参考

- https://docs.python.org/zh-cn/3/library/asyncio-task.html