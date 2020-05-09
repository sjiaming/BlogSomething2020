---
layout: article
title: Git Bash Commands
description: Some basic commands of git bash
imgsrc: assets/pics/tools/github.png
banner: assets/pics/tools/github_banner.png
date: 2017-10-25
category: Tool
tags:
  - Github
  - Cheatsheet
author: Song Jiaming
---
This post shows some git bash commands for manuipulating github repositories locally.

Note: in the following content, `<something>` means to be replaced by users when using the command.

### Basic Commands
* `ls` : list all the file of the folder you are currently in
* `cd <Foldername>` :  move to the folder where your current folder contains 
    * `cd desktop` : move to desktop
    * `cd ..` : move back to parent folder
    * `cd` : move to the root folder
* After you type part of folder name, `press Tap` to auto-fill the whole folder name. 
* `UP` key will help you auto-fill the last command you used.

### Create an Repository
1. Move to the folder where you want to save your project: `cd path/to/the/folder`
2. `git init`

Alternatively, you can use `git init <project directory>` straightaway.

### Clone an Existing Repository
1. Go to github and copy the project url
2. cd to the folder where you want to store your project
3. `git clone <url>`

### Manipulate Your Repository
- `git status` : show status/files inside th repository. If the file is red, it hasn't been add to repository
- Commit Change (All 3 steps are necessary and must be executed in order):
    1. `git add <filename>` : add the file to the repository (but havent uploaded)
        - `git add -A` : add all files. Alternatively: `git add --all` or `git add .`
    2. `git commit -m "<msg>"` : Comment you want t write about the file you add
    3. `git push` : uploaded the file to github.com
- `git pull` : get all the latest changes from github repository
- `git` : show all different git commands

### Conflict
Conflict normally occurs when two or more contributors work on the same file.<br>
When one of the contributors pushs his changer, the other contributors' push requests will be rejected.

To solve this problem:
1. `git pull`
2. Reopen the file, the conflicted parts will be highlighted
3. Remove any one version of the code
4. Push again

### Branch and Merge
- `git branch <name>` : create a branch with name 'name'
- `git checkout <name>` : switch to the branch 'name'
- `git checkout master`: switch to branch 'master'
- `git merge <name>` : merge from branch 'name' into current branch<br>(You should be at 'master' branch currently)
- `git branch -D <name>` : delete branch 'name'
- `git push origin <name>` : the changes are pushed to the branch 'name'   

<br>

----
#### References
1. [Introduction to Github](http://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)
2. [Github Beginners](https://www.youtube.com/watch?v=q2Zg4fhiMx4)
3. [Relevant Terminal command](http://mac.appstorm.net/how-to/utilities-how-to/how-to-use-terminal-the-basics/)
4. [Git Documentation](https://git-scm.com/doc)
5. [Set up a personal website using Github io](https://www.youtube.com/watch?v=WV7Pn0wWmrs&list=PLi3oIq0O9sJmrexdJnjjCGMc_pZ-oQuge)
6. [How to Setup Github Pages Website on Github](https://www.youtube.com/watch?v=W2bbU9YIwiQ&index=5&list=PLi3oIq0O9sJmrexdJnjjCGMc_pZ-oQuge)
7. [Branching and Merging](https://www.youtube.com/watch?v=uR-9NGrpU-c)
8. [Github cheatsheet written by other github user](https://gist.github.com/hofmannsven/6814451)
