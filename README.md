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


DVC
New Dataset
Checkout new branch and add new remote url


git checkout -b babystroller
dvc remote add -d babystroller s3://vama-sceneuds-images/babystroller
Add a folder babystroller and within it, two folders images & labels. Add the data into the folders. Create a babystroller.dvc & cache the data and hashes with the below command.


dvc add babystroller
Push data to S3. VERY IMPT!: do not just use dvc push as other data will be uploaded to this folder in S3. Be specific as shown below.


dvc remote default babystroller
dvc push babystroller.dvc
Upload changes to repository.


git add *
git add .dvc/config
git commit -m "your commit msg"
git push --set-upstream origin babystroller
Send a merge request to master

Adding New Data to Existing Dataset
Checkout to the branch with the dataset you need, and update changes from master branch.


git checkout wheelchair
git merge master
Pull your dataset from S3 after ensuring the remote url is correct.


dvc remote default wheelchair
dvc pull wheelchair.dvc

# add your new data into the downloaded folders, then update the cache and hashes
dvc add wheelchair
Push data to S3. VERY IMPT!: do not just use dvc push as other data will be uploaded to this folder in S3. Be specific as shown below.


dvc remote default wheelchair # not required if already set previously
dvc push wheelchair.dvc
Upload changes to repository.


git add *
git add .dvc/config
git commit -m "your commit msg"
git push
Send a merge request to master

Load from Existing Dataset
First, remember to export the AWS access key and secret key

Suppose the object of interest you want to download is babystroller

Check that the number of images matches what is written in information.txt


dvc remote default babystroller
dvc pull babystroller.dvc
