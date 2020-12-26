# Learn-Git

## Configuring Git

We can configure git in three levels. At the very top we have system level the settings that we have here are applied to all users of the current computer.

* User - applys to all users of the current computer
* Global - applys to all repositiries of the current user
* Local - applys to the current repository or the repository in the current folder.

So we can have different settings for different repositories or different projects.

```console
git config --global -e
```
All this configuration settings are stored in a text file .gitconfig. This command will open the configuration file in our default editor.

## Creating Snapshots

### Initializing a Repository

```console
git init
```
This command is used to initialize a new empty git repository in our project directory.

### Git Workflow

Our git repository is actually a hidden sub directory in our project directory. Creating a commit is like taking a snapshot of our project.  
In git we have a intermediate step or area called staging area or index. It's essentially what we are proposing for the next commit or next snapshot.  
We add the modified files to the staging area or index, review our changes and if everything is fine then we'll make a commit.  
The proposed snapshot will get permanently stored in our repository. Each commit clearly explains the state of the project at that point in time.  
Staging area is either a reflection of what we currently have in production or the next version that's gonna go into production.  
Each commit contains a unique id which is generated by itself and details of who, when and why the changes were made.  
In terms of storage git compresses content and doesn't store duplicate content.

### Committing changes

```console
git commit -m "Initial Commit."
```
Here within the quotes we type a short description to identify what this snapshot represents. At times a short one liner description is not sufficient.
In situation like this we drop the message and we just type 

```console
git commit
```
This opens our default code editor with COMMIT_EDITMSG tab open which is stored in our git repository.  
We add a short description and after a line break we type a long description. When we save the changes and close the window our changes will be committed.

### Skipping the Staging Area

```console
git commit -am "Learn how to commit without staging the changes."
```

By supplying the options flag -a which means all modified files will be committed direct without staging them.

### Removing Files

```console
git ls-files
```

When we remove a file from our working directory it still exists in the staging area. This command displays the files in our staging area.  
To remove a file we have to remove it from both the working directory and as well as from the staging area.

```console
git rm file2.txt
```

This command removes the file from both the working directory and the staging area in one go.

### Renaming or Moving Files

We use standard unix mv command to rename or move files and directories. In git renaming or moving files are two step operation.  
First we have to modify our working directory and we have to stage two types of changes, an addition and deletion. 

```
git mv file.txt main.js
```

This command will apply the changes to both the working directory and the staging area. 

### Ignoring files

To prevent git from adding certain files to the repository we use a special file .gitignore.  
This file don't have a name and should be placed in the root of the project directory.
It only works if we add the files to the .gitignore before committing the changes.  
It doesn't work and git keeps tracking the changes even if we add the file or directory to the .gitignore. To remove the files from staging area  

```console
git rm --cached -r bin/
```
We use git rm command to remove files from both the working directory and as well as from the staging area.  
By using --cached flag git removes the files only from the staging area.

### Short Status

```console
git status -s
MM file1.js
?? file2.js
```
Using this command we can get a shorthand status output. We have two columns. The one in the left represents the staging area and the other represents the working directory.

### Viewing Staged and Unstaged changes

To view the exact lines of code that has been changed we use the diff command. 

```console
git diff --staged
git diff
```

By providing the staged option git compares the files in the staging area with the files in the previous commit.  
This shows what we have in the staging area that goes into the next commit.  
Without the staged option it compares the files in the working directory with the files in the staging area.

```console
git diff --staged
diff --git a/file1.js b/file1.js
index badfb70..47c3216 100644
--- a/file1.js
+++ b/file1.js
@@ -1,3 +1,5 @@
 hello
 world
 test
+sky
+ocean
diff --git a/file2.js b/file2.js
new file mode 100644
index 0000000..f5e95e7
--- /dev/null
+++ b/file2.js
@@ -0,0 +1 @@
+sky
```

a/file1.js is the older copy which we have in the last commit. b/file1.js is the newer copy in our staging area. We compare two copies of the same file.   
Git divide the file into chunks, every chunck has a header that has information which gives you context in this case @@ -1,3 +1,5 @@.  

If we run git diff without any arguments we can see unstaged changes and if we pass --staged we can see the staged changes that are gonna go into next commit.
