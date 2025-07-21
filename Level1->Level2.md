# Level Info

> The password for level 2 is in the file ‘krypton2’.
> It is ‘encrypted’ using a simple rotation. It is also in non-standard ciphertext format.
> When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns.
> This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!
>
## Log-In Info
Username:  **krypton1**

Password:  **KRYPTONISGREAT**

```console
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

## Procedure
From the level info we know that we're looking for a file called `krypton2` that contains some ciphertext, we can search for this using the `find` command:
```console
krypton1@bandit:~$ find / -name "krypton2" 2>/dev/null
/krypton/krypton2
/krypton/krypton1/krypton2
/etc/krypton_pass/krypton2
/home/krypton2
```

We can see that there is a directory called `krypton_pass` in `/etc/` which likely contains the passwords for all krypton users, but we do not have read permissions to see the contents of `/etc/krypton_pass/krypton2`.
However there is another interesting file called `krytpon2` in the directory `/etc/krypton/krypton1` and we do have read permissions for this one:
```console
krypton1@bandit:~$ cat /etc/krypton_pass/krypton2
cat: /etc/krypton_pass/krypton2: Permission denied
krypton1@bandit:~$ cat /krypton/krypton1/krypton2
YRIRY GJB CNFFJBEQ EBGGRA
```

So it looks like we have our ciphertext now: `YRIRY GJB CNFFJBEQ EBGGRA`.  

In the level info we are told that
> This file has kept the plain text word boundaries and carried them to the cipher text.

In simple terms, this means that a three-letter word in the ciphertext represents a three-letter plaintext word and so on, which makes it a lot simpler to decipher.  

We are also told that
> It is ‘encrypted’ using a simple rotation

Rotation refers to a technique were the alphabet is shifted by `x` number of characters and each plaintext letter is substituted by the corresponding character `x` steps away.  The most commonly use rotation cipher is ROT13 (since it simply splits the English alpahbet in two).
We can use an online ROT13 convertor to decipher the contents of `Krytpon2`.  I chose to use [Cyberchef](https://gchq.github.io/CyberChef) for this with the following recipe:

```json
[
  { "op": "ROT13",
    "args": [true, true, false, 13] }
]
```

And just liek that, we can see that the password to the next level is `LEVEL TWO PASSWORD ROTTEN`


