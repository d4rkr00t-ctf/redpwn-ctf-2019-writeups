## super hash
> Does hashing something multiple times make it more secure? I sure hope so. I've hashed my secret ten times with md5! Hopefully this makes up for the fact that my secret is really short. Wrap the secret in flag{}.

> Note: Follow the format of the provided hash exactly

> Hash: CD04302CBBD2E0EB259F53FAC7C57EE2

As the challenge suggests string is really short, I assumed it would be less than 4 if it's to be solved by bruteforce.

```
>>> from hashlib import md5
>>> from string import printable
>>> taret = "CD04302CBBD2E0EB259F53FAC7C57EE2"
>>> def transform(x):
	for _ in range(10):
		hash = md5()
		hash.update(x.encode())
	        x = hash.hexdigest().upper()
	return x
>>> for c1 in printable:
	x1 = c1
	if transform(x1) == target: print(x1)
	for c2 in printable:
		x2 = x1 + c2
		if transform(x2) == target: print(x2)
		for c3 in printable:
			x3 = x2 + c3
			if transform(x3) == target: print(x3)
^

```

Flag - `flag{^}`
