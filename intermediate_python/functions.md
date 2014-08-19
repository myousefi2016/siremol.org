
# Functions

In the [last session](1_lists_and_dictionaries.md), you wrote a couple of scripts that could encode and decode messages from Morse code. The scripts are good, but are not very easy to use or reusable. For someone to make use of the scripts, they will have to edit them and copy and paste your code every time they want to encode or decode a message.

Functions provide a way of packaging code into reusable and easy-to-use components. Lets imagine we have some code to add together two arrays. Open a new `ipython` session and type the below;

```python
a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
c = []

for i in range(0,len(a)):
    c.append( a[i] + b[i] )

print(c)
```

This code has added the arrays `a` and `b` together to make `c`. We can turn this into a function that can add any two arrays together by using `def`. To do this, type;

```python
def addArrays(x, y):
    z = []
    for i in range(0,len(x)):
        z.append(x[i] + y[i])
    return z
```

You can now add the arrays together by calling the function using;

```python
d = addArrays(a,b)
print(d)
```

In this case you have called the function `addArrays` and passed in the arguments `a` and `b`. `a` is copied to `x`, while `b` is copied to `y`. The function `addArrays` then acts on `x` and `y`, creating the summed array `z`. It then returns the new array `z`, which is copied back to `d`.

You can use your new `addArrays` function to add together other arrays. Try typing;

```python
r = [ 0.1, 0.2, 0.3 ]
s = [ 5, 12, 8 ]
t = addArrays(r, s)
print(t)
```

You should see that `t` is the array `[5.1, 12.2, 8.3]`.

Note that we can pass the values to the function directly, e.g. type;

```python
r = addArrays( [ 1, 2, 3], [5, 6, 7] )
print(r)
```

This should show you that `r` is equal to the array `[6, 8, 10]`.

Note that you must pass in the right number of arguments to a function. addArrays expects two arguments, so if you pass more or less, then that is an error. Try this now;

```python
r = addArrays()
```

should show;

```
TypeError: addArrays() takes exactly 2 arguments (0 given)
```

while if you type;

```python
r = addArrays(a, b, c)
```

you should see something like;

```
TypeError: addArrays() takes exactly 2 arguments (3 given)
```

Note also that you can define your function to take as many arguments, and return as many values as you want, e.g. try typing;

```python
def lotsOfArgs(a, b, c, d, e):
    return (a+b, c+d, e)

(r, s, t) = lotsOfArgs(1, 2, 3, 4, 5)
print(r)
print(s)
print(t)
```

This should print out that `r` is equal to 3, `s` is equal to 7, while `t` is equal to 5. Can you work out why?

***

## Exercise

### Exercise 2a

The python script below contains the a loop that takes strings from a user, and depending on input, will encode or decode the message from Morse code. However, this script is missing the functions "encodeToMorse" and "decodeFromMorse" that are needed to make it work. 

```python
import sys

letter_to_morse = {'a':'.-', 'b':'-...', 'c':'-.-.', 'd':'-..', 'e':'.', 'f':'..-.', 
                   'g':'--.', 'h':'....', 'i':'..', 'j':'.---', 'k':'-.-', 'l':'.-..', 'm':'--', 
                   'n':'-.', 'o':'---', 'p':'.--.', 'q':'--.-', 'r':'.-.', 's':'...', 't':'-',
                   'u':'..-', 'v':'...-', 'w':'.--', 'x':'-..-', 'y':'-.--', 'z':'--..',
                   '0':'-----', '1':'.----', '2':'..---', '3':'...--', '4':'....-',
                   '5':'.....', '6':'-....', '7':'--...', '8':'---..', '9':'----.',
                   ' ':'/' }

morse_to_letter = {}

for letter in letter_to_morse:
    morse = letter_to_morse[letter]
    morse_to_letter[morse] = letter

def encodeToMorse(message):
    # function is missing - you need to add the code

def decodeFromMorse(message):
    # function is missing - you need to add the code

while True:
    print( "Instruction (encode, decode, quit) :-> ", )

    # Read a line from standard input
    line = sys.stdin.readline()
    line = line.rstrip()

    # the first line should be either "encode", "decode"
    # or "quit" to tell us what to do next...
    if line == "encode":
        # read the line to be encoded
        message = sys.stdin.readline().rstrip()

        print( "Message is '%s'" % message )
        print( "Encoded is '%s'" % encodeToMorse(message) )

    elif line == "decode":
            # read the morse to be decoded
            message = sys.stdin.readline().rstrip()   
    
        print( "Morse is   '%s'" % message )
        print( "Decoded is '%s'" % decodeFromMorse(message) )

    elif line == "quit":
        print( "Exiting...")
        break

    else:
        print( "Cannot understand '%s'. Instruction should be 'encode', 'decode' or 'quit'." % line )
```

In the last session you wrote two python scripts, [encode.py](1a_encode.md) and [decode.py](1b_decode.md) that encoded and decoded from English to Morse code and vice versa. Copy and paste the above script into a file called `morse.py`. Using the code you wrote for [encode.py](1a_encode.md) and [decode.py](1b_decode.md), edit `morse.py` and add in the missing `encodeToMorse` and `decodeFromMorse` functions.

If you are really stuck, there is an example completed script [here](2a_morse.md).

## Modules

Functions are great for organising your software into self-contained, reusable blocks of code. However, as it stands, you have to copy and paste your function into every script or program in which it is used. Modules (also called libraries) provide a way of packaging up a collection of functions into a single, reusable package. In python, creating a module is very easy. Indeed, you have already done it! The python scripts you have written are actually already python modules. You can import all of the functions defined in a script by using the "import" command.

    $ import morse
    Instruction (encode, decode, quit) :->

The "import" command has loaded the script, importing all functions, and then running all of the code. If we type "quit" we can exit back to the prompt.

Now at the prompt, I have access to all of the functions and variables contained in [morse.py](2a/example/morse.py). These functions are prefixed with the name "morse.", e.g.

    $ morse.[TAB]
    morse2a.decodeFromMorse  morse2a.letter_to_morse  morse2a.morse_to_letter  morse2a.string
    morse2a.encodeToMorse    morse2a.line             morse2a.py               morse2a.sys
    morse2a.letter           morse2a.morse            morse2a.pyc              

I can call the encode and decode functions from the prompt

    $ morse.encodeToMorse("Hello World")
    '.... . .-.. .-.. --- / .-- --- .-. .-.. -..'
    $ morse.decodeFromMorse(".... . .-.. .-.. --- / .-- --- .-. .-.. -..")
    'hello world'

While this is great, it was quite annoying that the actual code in [morse.py](2a/example/morse.py) was run when we imported the function. We can stop this from happening by using a python hidden variable. Hidden
variables begin with one or two underscores, and we can list them all using ipython TAB

    $ _[TAB]
    _                  __IPYTHON__        __doc__            _i                 _ih                
    _2                 __IPYTHON__active  __import__         _i1                _ii                
    _3                 ___                __name__           _i2                _iii               
    _4                 __builtin__        __package__        _i3                _oh                
    __                 __debug__          _dh                _i4                _sh           

We want the one called "__name__"

    $ __name__
    '__main__'

This gives the name of the current function or module. The top level function is called "__main__". To stop the code in our morse.py script from running, we just need to make sure that it is only run if the value of "__name__" is "__main__". For example, the [checkmain.py](checkmain.py) script does exactly that;

    def addArrays(x, y):
        z = []
        for i in range(0,len(x)):
            z.append( x[i] + y[i] )
    
        return z
    
    
    if __name__ == "__main__":
        # Don't run this code if this script is being
        # imported as a module 
    
        a = [ 1, 2, 3, 4 ]
        b = [ 5, 6, 7, 8 ]
    
        c = addArrays(a, b)
        print( c )

If I run this script from the command line, then the whole script is executed;

    $ python checkmain.py
    [6, 8, 10, 12]

However, if I import the script, then "__name__" is not equal to "__main__", so that part of the script is skipped;

    $ ipython
    $ import checkmain
    $ checkmain.addArrays( [1, 2, 3], [4, 5, 6] )
    [5, 7, 9]

It is extremely good programming practice to write all of your scripts as if they were modules (and indeed to write all of your code as if they were part of a reusable library). This makes it really easy for you to pick up and reuse all of your code, preventing you from having to continually rewrite the same functionality over and over again.

## Exercise

### Exercise 2b

Edit your [morse.py](morse.py) script so that it can be re-used as a module. Do this by adding in an 'if __name__ == "__main__":' check.

If you are really stuck, there is an example completed script in [2b/example/morse.py](2b/example/morse.py).

Make sure that you commit your edited script to your Git repository.

    $ git commit -am "...commit message..."
    $ git push

# [Previous](1_lists_and_dictionaries.md) [Up](python_and_good_programming_practice.md) [Next](3_documenting_code.md) 