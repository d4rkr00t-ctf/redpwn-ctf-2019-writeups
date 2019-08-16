## easy cipher
> This is an [easy cipher](./files/easy_cipher.html)? I heard it's broken.

Only some part of code is necessary for analysis to solve this challenge.
```
> var _0x29a9=["\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x61\x62\x63\x64\x65\x66","","\x63\x68\x61\x72\x41\x74","\x6C\x65\x6E\x67\x74\x68","\x63\x68\x61\x72\x43\x6F\x64\x65\x41\x74","\x57\x68\x61\x74\x20\x69\x73\x20\x74\x68\x65\x20\x70\x61\x73\x73\x77\x6F\x72\x64","\x61\x61\x34\x32\x62\x32\x33\x34\x63\x62\x30\x35\x39\x31\x35\x37\x31\x36\x63\x31\x34\x33\x34\x30\x35\x38\x66\x65\x31\x61\x65\x65\x31\x36\x63\x31\x34\x33\x34\x30\x63\x62\x30\x35\x39\x31\x35\x37\x61\x61\x34\x32\x62\x32\x33\x34","\x73\x75\x62\x6D\x69\x74\x20\x61\x73\x20\x72\x65\x64\x70\x77\x6E\x63\x74\x66\x7B\x50\x41\x53\x53\x57\x4F\x52\x44\x7D","\x3A\x28"];
> _0x29a9
0: "0123456789abcdef"
1: ""
2: "charAt"
3: "length"
4: "charCodeAt"
5: "What is the password"
6: "aa42b234cb05915716c1434058fe1aee16c14340cb059157aa42b234"
7: "submit as redpwnctf{PASSWORD}"
8: ":("
```
At the end of script, you will find
```
if(calcMD5(prompt(_0x29a9[5]))=== _0x29a9[6]){alert(_0x29a9[7])}else {alert(_0x29a9[8])}
```
So basically, we have to find the password whose md5 hash is `aa42b234cb05915716c1434058fe1aee16c14340cb059157aa42b234`

Searching it online in md5 db, we quickly get a hit - `shazam`. Flag - `redpwnctf{shazam}`