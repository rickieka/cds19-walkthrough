# Keybase.io
Keybase is a great way to start adopting cryptographic communications

start at [keybase.io](https://keybase.io) and create an account

**TODO:** Need to walk through this process again

```bash
$ keybase pgp export | gpg --import
$ keybase pgp export --secret | gpg --import --allow-secret-key-import
# prompted for keybase password first
Please enter your Keybase passphrase to unlock the secret key for:
PGP key keybase.io/[USERNAME] <[USERNAME]@keybase.io> [KEY_ID]
# next prompted to create a new passphrase to procted my key
Enter passphrase to protect your PGP key. Secure passphrases have at least 8 characters.:
Please reenter your passphrase for confirmation:
```
