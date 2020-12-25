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

## Initializing a Repository

```console
git init
```
This command is used to initialize a new empty git repository in our project directory.
