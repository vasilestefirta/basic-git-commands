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

## Set config values
- Set config values globally:
  - ```git config --global user.name "John Smith"```
  - ```git config --global user.email "john.smith@nomail.com"```
- Set config values for a local specific repo (just remove ```--global``` or replace it with ```--local```):
  - ```git config user.name "John Smith"```
  - ```git config user.email "john.smith@nomail.com"```
