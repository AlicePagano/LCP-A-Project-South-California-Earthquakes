# LCP-Project-South-California-Earthquakes

## Git Steps
- See all the changes you have done:
```
$ git status
```
- Syncing
```
$ git remote show origin
```
- Downloading changes
```
$ git fetch origin
```
```
$ git pull
```
- Uploading changes:
```
$ git add .
```
```
$ git commit -m "Brief description of changes"
```
```
$ git push origin
```

## Git Instructions

### 1) First time configuration (only do this once per computer)
After making an account on ​https://github.com/​, in a terminal (in the folder in which you want to work), launch the following commands:
```
$ git config --global user.name ​"Name Surname"
$ git config --global user.email mail_used_on_registration@example.com
```
You can check the config at any time with:
```
$ git​ config ​--list
```
### 2) Download the repository (only do this once per computer)
A ​git repository​ is just the folder containing the project’s files, along with some ​hidden information ​used by git to store all the files history. All of this is stored locally, meaning that every user will have a copy of the ​entire project data ​on their hard drive. All changes will be first applied to the local (personal) repository, and then synced to a common server by using git commands.
```
$ git clone https://github.com/AlicePagano/LCP-Project-South-California-Earthquakes
```
This will create a folder “LCP-Project-South-California-Earthquakes” containing all the data. This is the local repository.
### 3) Basic git commands.
The idea is to make some changes, and ​save them​ in a new “version” of the project. These versions are called “commits”, and are stored by git, allowing undoing previous changes at any time. In the most basic workflow, the project will evolve as a continuous series of commits:
![Master](https://github.com/AlicePagano/LCP-Project-South-California-Earthquakes/blob/master/Git%20Instructions%20Images/master.png?raw=true)
A “line” of commits is called ​branch.​ Every git repository starts with only a single branch, called ​master​.

To create a ​new commit​, you first make some changes to the files inside the repository. You can see all the changes you have done by typing:
```
$ git status
```
This command will show:
- Which branch you are now currently (e.g. “On branch master”)
- If you are up to date with the server version (e.g. “Your branch is up to date with
‘origin/master’)
- All files that have unregistered changes from the last commit are shown in ​red.
New files are initially “​untracked​”, while pre-existing files that have been modified are denoted as “​modified​” under “changes not staged for commit”.

You can now ​register ​the changes you want to be saved on the new commit. This is called “staging”, and is done by typing:
```
$ git add [name files]
```
where [files] can be several filenames, or even the wildcard “.”, meaning “register everything”.
​Staged files​ will appear in ​green ​in the output of “git status”. Note that git will register the ​current version of the file​ - meaning that if you stage something, and then modify it, you will need to ​stage it​ again (if you want to register also the newer edits).

You can discard changes with:
```
$ git checkout -- filename
```
When you are ready to save the new commit (for example after having finished a work session), run “git status” again, check that you have staged everything you need, and finally create the commit with:
```
$ git commit -m ​"Brief description of changes"
```
#### Syncing
All commits are initially stored locally, and are not available to other users. To share them, you need to save them on the GitHub server.
GitHub s​tores a copy of the repository, which is called a “​remote​”. As you downloaded the repo from GitHub, the address of that “remote” is stored as the “​origin”​ . You can check this by typing:
```
$ git remote show origin
```
You can upload (= “push”) files from your local repo to ​origin,​ or download changes from origin ​(= “pull”). By default, a local branch will be configured to ​track​ changes of the corresponding remote branch. For example, the local “master” will track “origin/master”.

#### Downloading changes
If another user has made changes and uploaded them to “origin/master”, your “master” will be ​behind​ several commits:
![Origin](https://github.com/AlicePagano/LCP-Project-South-California-Earthquakes/blob/master/Git%20Instructions%20Images/origin.png?raw=true)
So you’ll need to download the newer commits (the magenta ones in the pic) before starting to work. To do this, first you need to ​check​ if there are changes to download:
```
$ git fetch origin
```
Then you “pull” the changes:
```
$ git pull
```
If everything goes well (meaning that there are no ​conflicts​ between your local files and the newer ones) you will have the newest version of the repository.

#### Uploading changes
After having created a ​commit​ on your machine, you will need to ​upload it ​to the server. You do this by simply typing:
```
git push origin
```
#### Conflicts
Suppose you have modified a file “test.py”. At the same time, another user has modified their version of “test.py”, and uploaded it to the server. Now, when you try to upload your commit, there will likely be a ​conflict.​
Git will warn you about which files contain conflicts. If you open them with an editor, you’ll find a strange new section of code:
```
 <<<<<<< HEAD ======= >>>>>>> new_branch_to_merge_later
```
This block contains the conflicting changes. The first half, from HEAD to ====, is the code in the ​source commit​ (for example, if you are ​pushing​ to the server, the source will be your machine). The second half is the ​destination commit​. You’ll have to remove these
dividers, and manually merge the edits.
When you’re done, you use “git add file” to register the changed file, and finally ​git commit -m ​"Merged changes"​ to ​resolve ​the conflict. You can now ​retry t​ he initial command (e.g. the ​git ​push​). Hopefully it will work just fine.
Note that there are graphical tools to ease this tedious process. Search online for “git mergetool” for more info.

#### Branches
It is best to avoid conflicts entirely. The first tip is to always sync the repository (with git fetch and git pull) ​before ​applying any changes. But the most useful technique is to work on separate versions - i.e. on ​separate branches.​
![Development](https://github.com/AlicePagano/LCP-Project-South-California-Earthquakes/blob/master/Git%20Instructions%20Images/development.png?raw=true)

You can have multiple parallel “histories” of the project, and then “merge them” when needed. An example of workflow could be:
- Master holds always a working version of the project
- Development holds new changes that may break the program, and need to be
tested. When they are ready, they will be copied to master
Another example. Suppose that you have found a bug in the master code. You can correct it and upload the correction on the ​master​ branch, risking to create other bugs, or create a parallel branch named “Bugfix”, correct there the mistakes, test thoroughly and only then apply the changes to master.

Let’s see how to do this. You create a new branch with:
```
$ git checkout -b branch_name
```
At any time, you will be in a ​specific branch.​ You can see your location with ​git status​. Your files will reflect the status of that branch, and all changes you do will be local to that branch. So, if you are not in master, whatever you do you will not influence it.

To move to a different branch, you do:
```
$ git checkout branch_name
```
You can use this to return to ​master,​ if needed.
You can use all of the previous commands to make changes, register them, commit and sync them.

Finally, when you are ready, you can ​copy​ all your commits to the “master” branch. This is the “​merge​” operation - and it simply “replays” everything you have done on the destination branch.

First, you move to the branch you need to apply edits on (e.g. master) with git checkout. Then:
```
$ git merge branch_to_merge_from
```

# Final Projects for Laboratory of Computational Physics

In each of the branches of this repo you find all the necessary to complete your final project.

Each branch is named after the group of students a given project is assigned to. The name is left generic, "GroupN", on purpose, the actual group members are listed in the Members.txt file.

Students are supposed to work together to produce a short report on the assigned task, which will have to be committed to the group branch together with the code developed to achieve the results. The preferred format for the latter is a jupyter notebook, with the proper description, the code implemented for the purpose and the actual results (plots, tables, etc.). Alternatively, description and results could be provided in a paper-like document, whereas the code still in a jupyter notebook.

Further information about the deliverables are given in the project instructions.

The following files are there for reference:

*  Members.txt the list of students belonging to the group

*  Project.ipynb the actual description of the assigned project

Other files could be present if needed
