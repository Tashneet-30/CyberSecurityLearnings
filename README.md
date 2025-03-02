# Cyber Security Learnings – Day 1 (03 March 2025)

## Understanding Gobuster for Web Directory Enumeration

### What is Gobuster?

Gobuster is a command-line tool for finding hidden directories and files on a website. It works by brute-forcing URLs using a predefined wordlist. This is useful in penetration testing to discover unlisted web pages containing sensitive information.

## Using Gobuster in TryHackMe Lab

Today, I worked on a TryHackMe lab with a fake bank website. I used Gobuster to discover hidden pages.
### Command Used:

```bash
gobuster dir -u http://fakebank.thm -w wordlist.txt
```

## Gobuster and Wordlists in Parrot OS

### Breaking Down the Command

| Command Part | Meaning |
|-------------|---------|
| `gobuster dir` | Specifies we are searching for directories |
| `-u http://fakebank.thm` | The target website URL |
| `-w wordlist.txt` | The wordlist file used for guessing directories |

## Does Gobuster Work Without a Wordlist?
❌ **No**, Gobuster does not guess directories randomly. It requires a wordlist to function. If no wordlist is provided, it returns an error.

## What Happens If Wordlist is Missing or Empty?

If `wordlist.txt` does not exist, Gobuster returns the following error:

```bash
Error: stat wordlist.txt: no such file or directory
```


If the wordlist is empty, Gobuster runs but finds nothing.

## Where to Find Prebuilt Wordlists in Parrot OS?

Parrot OS comes with several built-in wordlists, stored in `/usr/share/wordlists/`.

### Useful Wordlists in Parrot OS:

| Wordlist Path | Purpose |
|--------------|---------|
| `/usr/share/wordlists/dirb/common.txt` | Common directory names (good for Gobuster) |
| `/usr/share/wordlists/dirb/big.txt` | Extended version of `common.txt` |
| `/usr/share/wordlists/seclists/Discovery/Web-Content/common.txt` | Another good wordlist for web directory brute force |
| `/usr/share/wordlists/wfuzz/general/common.txt` | Used for fuzzing web applications |

## Using Prebuilt Wordlists in Gobuster

If `wordlist.txt` is missing, use a system wordlist:

```bash
gobuster dir -u http://fakebank.thm -w /usr/share/wordlists/dirb/common.txt
```

## Working with rockyou.txt (Password Wordlist)

`rockyou.txt` is a famous password list, but it is compressed by default.

### Extracting and Using rockyou.txt

```bash
gunzip /usr/share/wordlists/rockyou.txt.gz
```

Now, you can use it for password attacks with Hydra:

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt http://fakebank.thm/login.php
```

## Key Takeaways from Today’s Learning

✅ Gobuster requires a wordlist; it does not guess randomly.  
✅ If a wordlist is missing or empty, Gobuster fails or finds nothing.  
✅ Parrot OS includes prebuilt wordlists in `/usr/share/wordlists/`.  
✅ `rockyou.txt` is a password wordlist, but it must be extracted before use.  
