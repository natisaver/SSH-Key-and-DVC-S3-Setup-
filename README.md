# There are 2 files uploaded❗
- ⭐The word document contains all the information an steps to using VS `AWS S3 + s3-pit-restore` VS `DVC+ AWS S3 + Git` 
- ⭐The pdf contains specifics as to the usage of DVC only.

# SSH-Key-and-DVC-S3-Setup-
Showing how to set up SSH keys on github in addition to using DVC in conjuntion with AWS S3 for version control of datasets

## Set Up SSH Key and Origin for pushes
🟠 <u> 1. Generate SSH Key (Git Bash) </u>
- First `Create the config file`, *in this case no password was set
```console
ssh-keygen -t ed25519 -C username@email.com
```
```console
eval "$(ssh-agent -s)"
```
```console
~/.ssh/config
```
```console
touch ~/.ssh/config
```
- Secondly, `edit the config file`, pasting this inside:
```
Host *
 AddKeysToAgent yes
 IdentityFile ~/.ssh/id_ed25519
```
- If you have a password and want it to be stored, type this instead:
```
Host *
 AddKeysToAgent yes
 IdentityFile ~/.ssh/id_ed25519
 UseKeychain yes
```

```console
ssh-add ~/.ssh/id_ed25519
```
🟠 <u> 2. Telling GitHub about the SSH Key </u>
- `Copy the contents` when this command is typed in:
```console
cat ~/.ssh/id_ed25519.pub  
```
- ❗Go to GitHub ➜ Settings ➜ SSH/GPG Keys ➜ New SSH Key 
- `Paste the contents under Key Section`, Title can be whatever

🟠 <u> 3. Setting our remote origin in the command line </u>
- View current origin:
```console
git remote -v
```

- Remove the original origin:
```console
git remote rm origin
```

- Add the new origin with the `SSH` github provides:
```console
git remote add origin git@github.com:username/s3-test-repo.git
```

