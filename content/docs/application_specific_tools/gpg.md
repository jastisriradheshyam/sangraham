+++
title = 'GPG'
date = 2024-12-19T19:23:56+05:30
draft = false
+++

# GPG common commands

- Generate GPG keys: `gpg --full-generate-key`
- List GPG keys: `gpg --list-keys`
- list GPG keys with key-id (key-id format): `gpg --list-keys --keyid-format LONG`
- List GPG keys for which you have both a public and private key: `gpg --list-secret-keys --keyid-format LONG`
- Output public key using GPG key-id: `gpg --armor --export gpg-key-id`
- Output public key to file: `gpg --output public.pgp --armor --export user@email`
- Output private key to file: `gpg --output private.pgp --armor --export-secret-key user@email`
- Import GPG private key: `gpg --import private.gpg`
- Encrypt a file: `gpg -r RECIPIENT_EMAIL -e FILE_NAME`
- Decrypt a file: `gpg -d FILE_NAME`


----
- If passphrase is not asked : `gpg -c --pinentry-mode=loopback test`
   - `--pinentry-mode=loopback` will force passphrase
- Ask password from terminal: `export GPG_TTY=$(tty)`

----
# using GPG key from external device
- `mkdir /path/to/the/a/desired/directory/in/external/drive/`
- `gpg --homedir /path/to/the/a/desired/directory/in/external/drive/ --import /path/to/the/gpg_private_key.gpg`
  - this will make the necessary files to manage the key and make the homedir for the particular key
- `export GNUPGHOME=/path/to/the/a/desired/directory/in/external/drive/`
  - now use it for encryption and decryption as required, this will be temporary and good practice for using key from external device
  - importing is required once per a external device.
  - On windows (powershell) : `$ENV:GNUPGHOME=/path/to/the/a/desired/directory/in/external/drive/`

# Disable Password Caching [^3]

- `vi ~/.gnupg/gpg.conf`
- Add the following lines

```conf
default-cache-ttl 1
max-cache-ttl 1
```

- then restart the agent
  - `echo RELOADAGENT | gpg-connect-agent`

----

- For particular command (v2.2.15 and above): `gpg -c --no-syskey-cache file.txt`
  - Do not apply to git signing

# GPG best practices

1. [implementation of the Riseup OpenPGP Best Practices](https://raw.githubusercontent.com/ioerror/duraconf/master/configs/gnupg/gpg.conf)
2. [OpenPGP Best Practices - riseup.net](https://riseup.net/en/security/message-security/openpgp/best-practices)
3. [pgp](http://curtiswallen.com/pgp/)
4. [attila-lendvai/gpg-keygen: Generate PGP keys with GnuPG, following best practices](https://github.com/attila-lendvai/gpg-keygen)

# Additional Links

1. [pgp - What is an OpenPGP Key ID collision? - Information Security Stack Exchange](https://security.stackexchange.com/questions/74009/what-is-an-openpgp-key-id-collision)
2. [cryptography - When changing a PGP passphrase, does it only affect the private key? - Information Security Stack Exchange](https://security.stackexchange.com/questions/37510/when-changing-a-pgp-passphrase-does-it-only-affect-the-private-key/37513)

# References:

1. [encryption - GnuPG decryption not asking for passphrase - Information Security Stack Exchange](https://security.stackexchange.com/a/230555/184792)
2. [homedir](https://www.gnupg.org/gph/en/manual/r1616.html)
[^3]: [encryption - GnuPG decryption not asking for passphrase - Information Security Stack Exchange](https://security.stackexchange.com/questions/103034/gnupg-decryption-not-asking-for-passphrase/103037#103037)
