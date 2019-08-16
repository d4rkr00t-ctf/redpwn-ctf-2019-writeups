## crypt
> Store your most valuable secrets with this new encryption algorithm.

Here is the [source](./files/crypt.html)
Simplifying the script tag function, we get following function
```
> f=>btoa([...btoa(f)].map(s=>String.fromCharCode(s.charCodeAt(0)+(location.host.charCodeAt(0)%location.host.charCodeAt(3)))).join(''))
```
Let's break this down.
```
btoa gives base64 encoded string.
(location.host.charCodeAt(0)%location.host.charCodeAt(3)) can be simplified to 99 (constant)

1. [...btoa(f)] gives an array containing letters of base64 encoding of string 'f'

2. Each character of (1) is mapped as char(ascii(c) + 99)

3. All the above characters are joined back into a string, and once more base64 encoded
```

So, all we have to do is reverse the process. We are given the encoded flag `vdDby72W15O2qrnJtqep0cSnsd3HqZzbx7io27C7tZi7lanYx6jPyb2nsczHuMec`
```
> x = atob('vdDby72W15O2qrnJtqep0cSnsd3HqZzbx7io27C7tZi7lanYx6jPyb2nsczHuMec');
> x = [...x];
> x = x.map(s=>String.fromCharCode(s.charCodeAt(0)-99));
> x = x.join('');
> atob(x)
"flag{tHe_H1gh3st_quA11ty_antI_d3buG}"
```
