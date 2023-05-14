## Symmetric key encryption
#symmetric_encryption
- Some information is encrypted using a key
- Same key is used to decrypt the encrypted data.
- `DES`, `3DES` are some of obsolete algorithms for symmetric encryption
- `AES` is a modern symmetric encryption.

## Hashing
#hashing
- Converting data in to string of defined length no matter what ever the size of data is called  hashing.
- Data is converted using hash function, data is transferred to other systems with the hash.
- On the second system hash is split from data, Hash is again generated from the data and compared with the provided hash.
- This provides additional integrity 
- Even a small character or byte change will lead to to a different hash creation.
- Once hash is created from data, it is a irreversible function, meaning data cannot be retrieved just by using hash.

### MD5 hashing
#MD5_hashing

- MD5 hashing algorithm will always generate a 128bit string for every data that we use to generate the hash.

In a windows machine to generate a MD5 hash use
```
certutil -hashfile <file_name> MD5
```

In mac
```
md5 <file_name>
```

With openssl we can use as `openssl md5 <filename>`

### SHA hashing
#sha_hashing

SHA hashing also generates a string of specified length. It depends on the version of the SHA that we are using.

- There are three version of SHA algorithm
	- SHA1 - generates 160 bit string
	- SHA256 - generates 256 bit string
	- SHA512 - generates 512 bit string

On a windows machine
```
certutil -hashfile <file_name> SHA1 #for 160 bit hash
certutil -hashfile <file_name> SHA256 #for 256 bit hash
certutil -hashfile <file_name> SHA512 #for 512 bit hash
```

Using open ssl
```
openssl sha1 <filename>
```