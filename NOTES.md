## Need help?
- ```git help <verb>```
- ```git <verb> --help```

> **Example:** ```git help config``` or ```git config --help```

---

## Pull Request WorkFlow
- Begin by doing a ```git pull``` to get the latest content on your master branch:
  - ```git branch``` - double-check if you are currently in the master branch
  - ```git pull origin master```
- Create a new branch:
  - ```git branch <your-branch-name>```
- Switch from master branch to your new branch
  - ```git checkout <your-branch-name>```
- Code in your changes, add and commit the files:
  - make changes
  - ```git add -A```
  - ```git commit -m "my changes"```
- Switch back to master: 
  - ```git checkout master```
- Pull the master branch again:
  - ```git pull origin master```
- Switch back to your new branch and merge master into it:
  - ```git checkout <your-branch-name>```
  - ```git merge master```
- Push the branch up to github and submit it as a pull request:
  - ```git push -u origin <your-branch-name>```
- That pull request can now receive comments and code discussion, as well as accept new commits before being merged in with the master branch

---

## Set config values
- Set config values globally:
  - ```git config --global user.name "John Smith"```
  - ```git config --global user.email "john.smith@nomail.com"```
- Set config values for a local specific repo (just remove ```--global``` or replace it with ```--local```):
  - ```git config user.name "John Smith"```
  - ```git config user.email "john.smith@nomail.com"```
- Check config values:
  - ```git config --list```

---

## Move commits from one branch to another using ```git cherry-pick```
**Example:**

Let's say you have 2 branches: *master* and *dev*. You've made a bunch of changes and committed them accidentally to *master* instead of *dev*. Here are the steps how to move your commit from *master* to *dev* and then remove that commit from *master*

1. make sure you're in the *master* branch, by running ```git branch```

2. run ```git log``` and copy your commit's hash string (*NOTE:* you don't need to copy the entire hash, just first 6-7 characters should work)

3. switch to the *dev* branch: ```git checkout dev```

4. run ```git cherry-pick <PASTE_YOUR_HASH_STRING_HERE>```. This will copy the commit you've made on *master* to the *dev* branch, but will not delete the original commit

5. run ```git log``` and double-check that your commit was copied

6. switch back to the master branch: ```git checkout master```

7. run ```git log``` and copy the hash string of that commit you want to reset your branch to.

8. run ```git reset --hard <PASTE_YOUR_HASH_STRING_HERE>``` to reset your branch to that commit.

**A FEW NOTES HERE:**

1. ```git reset --soft <PASTE_YOUR_HASH_STRING_HERE>``` - this will reset your branch to a specific commit, but will keep all your changes you've done since then into the *staging area*

2. ```git reset <PASTE_YOUR_HASH_STRING_HERE>``` (default/mixed) - this will reset your branch to a specific commit and will remove all your changes you've done since then from the *staging area*, but will keep them into the *working directory* (basically to that moment before you ran ```git add``` to add your changes to the *staging area*)

3. ```git reset --hard <PASTE_YOUR_HASH_STRING_HERE>``` - this will reset your branch to a specific commit and will remove all your changes you've made since then. **NOTE** that it will keep all *untracked* files and if you want to remove them, then you'll need to run ```git clean -df```, where ```d``` stads for *directories* and ```f``` stands for *files*.

---

## Recover committed changes after running ```git reset --hard``` using ```git reflog```

> **NOTE:** You can get the commit back so long as it's been within a few days. git only garbage collects after about a month or so unless you explicitly tell it to remove newer blobs.

Let's say you've been working on the *master* branch and you have quite a bit of commits created. At some point you wanted to do a ```git reset --hard``` and reset your branch to a previous commit. How do you undo that?

- run ```git  reflog``` - this will list all the commits in the order you last referenced them (it includes ```commit``` commands as well as ```reset```, ```checkout``` etc.). 
  
  **Output example:** 
  
  ```
  0239a45 HEAD@{16}: pull origin master: Fast-forward
  19ddd52 HEAD@{29}: commit: App version update
  ```

- Copy the hash of your commit you want to revert to then:

**OPTION 1:**

- run ```git checkout <PASTE_YOUR_HASH_STRING_HERE>``` - this will get you in a detachead HEAD state. This state will be garbage collected at some point.

- to save this state, you can create a branch out of it by running ```git checkout <YOUR_BRANCH_NAME>```

- use that *"backup"* branch you just created to merge those lost changes back into *master*

**OPTION 2:**

- run ```git reset --hard <PASTE_YOUR_HASH_STRING_HERE>``` - this will *"move"* your head back to the desired commit.
  
  **NOTE:** This will destroy any local modifications. Don't do it if you have uncommitted work you want to keep.
  
  Alternatively, if there's work to keep:
  
  ```
  git stash
  git reset --hard <PASTE_YOUR_HASH_STRING_HERE>
  git stash pop
  ```
  
  This saves the modifications, then reapplies that patch after resetting. You could get merge conflicts, if you've modified things which were changed since the commit you reset to.
  
**References:**

- [http://stackoverflow.com/a/34519716](http://stackoverflow.com/a/34519716)
- [http://stackoverflow.com/a/21778](http://stackoverflow.com/a/21778)
