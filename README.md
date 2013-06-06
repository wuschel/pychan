# Go-style Chan for Python

Implements Go's chan type in Python.

## Examples

You can `put` onto channels, and `get` from them:

```Python
c = Chan()

# Thread 1
c.put("Hello")

# Thread 2
print "Heard: %s" % c.get()
```

Channels can be closed (usually by the sender.
Iterating over a channel gives all values until the channel is closed:

```Python
c = Chan()

# Thread 1
for word in ['get', 'off', 'my', 'lawn']:
    c.put(word)

# Thread 2
for thing in c:
    print "Heard:", thing
```

You can wait on multiple channels using `chanselect`.  Pass it a list of input channels and another of output channels, and it will return when any of the channels is ready.

```Python
def fan_in(outchan, input1, input2):
	while True:
		chan, value = chanselect([input1, input2], [])
		if chan == input1:
		    outchan.put("From 1: " + str(value))
		else:
		    outchan.put("From 2 " + str(value))
```

You can see more examples in `pick-conc-patt.py`.


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/stuglaser/pychan/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
