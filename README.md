## A timer as a context manager

When one wants to measure the wall clock time of a code snippet, one usually do:

```python
start = time.time()
# ...
# Some code we want to time
# ...
end = time.time()
elapsed = start - end # in secs
elapsed_ms = elapsed * 1000 # in ms
```

I find this quite heavy to read and un-pythonic. `timer` allows you to do
the exact same thing with a context manager:

```python
with Timer() as t:
    # Some code we want to time
print t.elapsed_seconds
print t.elapsed_milliseconds
```

## The ctimer.Timer class
`ctimer.Timer` is a [context manager](http://docs.python.org/reference/datamodel.html#context-managers) with 5 attributes:
* `default_timer`: a platform specific timer function (`time.time` for Unix platforms and `time.clock` for Windows platforms)
* `start`: the time of the beginning of the execution of the code block, measured with  `default_timer`
* `end`: the time of the end of the execution of the code block, measured with  `default_timer`
* `elapsed_seconds`: the wall clock timing of the execution of the code block, in seconds
* `elapsed_milliseconds`: the wall clock timing of the execution of the code block, in miliseconds

## Example

```python
>>> from timer import Timer
>>> with Timer() as t:
... for i in xrange(10000000):
... pass
...
>>> print(t.start)
1341568310.06
>>> print(t.end)
1341568310.14
>>> print(t.elapsed_milliseconds)
73.6618041992 # in miliseconds
>>> print(t.elapsed_seconds)
0.0736618041992 # in seconds
```

## Thanks
Thanks to halloi for its helpful insights and contributions.

## License
ctimer is released under the GPLv3 license.
