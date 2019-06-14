# Signing Commits

Signing commits is a way to verify authenticity of the author. This will help us prevent bad actors from injecting code bits into our projects.

__Objectives__
- setup GPG key
- adding GPG key to gitlab account
- associating GPG key with git

## Setup GPG key
The first step is to generate (or if you already have one, import) a GPG key. The GPG key will be used to associate your identity to gitlab, and verify you as an author of the commits, and code being pushed to the gitlab repository.

Need this to prevent `Inappropriate ioctl for device` error
```bash
# had to do this to import keybase pgp key, only for the import
# add this to your .rc file
export GPG_TTY=$(tty)
```

### Generating a new key
Gitlab has some instructions already on how to [generate a GPG key](https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/#generating-a-gpg-key) they contain a lot more depth and detail, below is an abbreviated version of what is on that page.

```bash
# instructions and more detail in link provided
# this is the abreviated version
gpg --full-gen-key

 Please select what kind of key you want:
    (1) RSA and RSA (default)
    (2) DSA and Elgamal
    (3) DSA (sign only)
    (4) RSA (sign only)
 Your selection? 1

 RSA keys may be between 1024 and 4096 bits long.
 What keysize do you want? (2048) 4096
 Requested keysize is 4096 bits

 Please specify how long the key should be valid.
          0 = key does not expire
       <n>  = key expires in n days
       <n>w = key expires in n weeks
       <n>m = key expires in n months
       <n>y = key expires in n years
 Key is valid for? (0) 0
 Key does not expire at all

 Is this correct? (y/N) y

 GnuPG needs to construct a user ID to identify your key.

 Real name: Mr. Robot
 Email address: <your_email>
 Comment:
 You selected this USER-ID:
     "Mr. Robot <your_email>"

 Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O

# export the public key so it can be added to gitlab
gpg --armor --export $(KEY_ID)
```

### Configure git to use your key

[Git Signing](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work)
get the ID of your gpg key `gpg --list-keys` and configure git to use that key
[Gitlab & GPG](https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/)

```bash
# You can configure git to "Auto sign" commits for you, with the key we've created
# configure git GLOBALLY
git config --global user.signingkey [KEYID]
git config --global commit.gpgsign true

# configure git for only this specific project (Leave off --global)
git config user.signingkey [KEYID]
git config commit.gpgsign true

# if you don't want to do auto signing, then just make sure to commit with the -S flag
git commit -S -m "signing this commit specifically"

# if having issues w/ gpg
gpgconfg --kill gpg-agent
```

GPG config for verified in gitlab (if unverified when added)

```bash
gpg --edit-key [KEYID]
  gpg> adduid
  # enter information that match gitlab email
  Real name: [YOUR_NAME]
  Email address: [YOUR_EMAIL]
  Comment:
  You selected this USER-ID:
      "[YOUR_NAME] <[YOUR_EMAIL>"
  
  Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
  # list uids and select the one that doesn't match
  gpg> uid [NON_MATCHING_ID]
  gpg> deluid
  # to remove the other uid
```

## Configure gitlab

### Only allow signed commits

https://gitlab.com/[GROUP]/[PROJECT]/walkthrough/settings/repository#js-push-rules

![gitlab push rules](images/push_rules.png)

when you commit, add in the `-S` tag to make sure you sign the commit

### add GPG key to repository hosting

[GitLab Instructions](https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/#adding-a-gpg-key-to-your-account)

[GitHub Instructions](https://help.github.com/en/articles/adding-a-new-gpg-key-to-your-github-account)
