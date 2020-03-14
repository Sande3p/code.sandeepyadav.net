---
layout: post
title:  "Advanced Git Techniques"
date:   2020-03-14 16:13:58 +0530
categories: jekyll update
---
## Git Configurations
### 3 Levels of configs
`-- local`, `--global`, `--system`  
Example  
`git config --local user.name Sandeep [hi4sandy]`  
`git config --local user.email sandeep.yadav@msn.com`

### Removing config
`git config --global --unset user.name`

### Editing config
`git config --global -e`
`git config --global --edit`  //opens editor to update file

### Listing all configs
`git config --list --show-origin`

### Showing code diff
`git diff`

### Opening difftool/mergetool
`git difftool`
`git mergetool`

### Creating Alias
`git config --global alias.ss 'status --short'`

### Amending comming
`git commit --amend`  
The git commit --amend command is a convenient way to modify the most recent commit. It lets you combine staged changes with the previous commit instead of creating an entirely new commit. It can also be used to simply edit the previous commit message without changing its snapshot.

## Attributes
File `.gitattributes`  
### Editing gitattributes
`code .gitattributes`

### Tag
Tagging is used to create a new release
Creating a tag & adding/editing releasing note creates a new release
```
git tag 0.0.1
git push origin 0.0.1
```

Using `.gitattributes` files or folders can be excluded from release.
Exmaple of `.gitattributes` file content
```
*.jpg diff=exif
*.png diff=exif
# for images we are using exif tool

#anything that starts with a dot will be excluded from releases
.* export-ignore

# tests folder will be excluded from release
tests export-ignore
```

## Git Submodules
A constructor within Git that enables you to keep a separate Git repository as a subdirectory within an existing repository. This effectively keeps two separate repositories linked together within a project.

Creating a new submodule  
`git submodule add git@github.com:Sande3p/gitAdvTech.git external/repo1`

A `.gitmodules` file is added in the repo.

### Clone the repository 
`git clone <repo_name>`

### Initialize submodules
`git submodule init`

### Grab the content of the submodule
`git submodule update`

Submodules must be updated explicitly

### To recursively clone git repo with all the submodules
```
git clone --recursive <repo_name.git> 
git clone --recursive <repo_name.git> <folder_name>
```


### Temporarily removing a submodule
`git submodule deinit external/repo1`

### To add back temporarily removed module
`git submodule reinit external/repo1`

### Permanently removing a repository
`git submodule deinit external/repo1`
`git rm external/repo1`
`git commit -m “Removed project submodule repo1”`

### Listing nested submodule
`git submodule foreach ‘cat .gitmodules’`

### Synching .gitmodules configuration 
If in child module new modules are added or config is changed.
`git config sync --recursive`

### Synching & updating together
`git submodule update --init --recursive`


### Git pull all the repositories of a submodule
If it's the first time you check-out a repo you need to use --init first: 
`git submodule update --init --recursive`

For git 1.8.2 or above, the option --remote was added to support updating to latest tips of remote branches:
`git submodule update --recursive --remote`


# Editing & pushing changes in Submodules

# Set global config
`git config --global push.recurseSubmodules on-demand`

### Pushing changes
Do the commit in the submodule 
Do the commit in the parent repo
Push from the parent repo after setting glob config to `on-demand`
`git push`


### Push all updates at once
`git push --recurse-submodules=on-demand`

## Git Hooks
[Pluralsite Tutorial](https://app.pluralsight.com/course-player?clipId=87423554-2d43-4852-9e23-ac13885cce12)

![git hooks](https://lh6.googleusercontent.com/KCWSXU6tklxnJ3sjqLMAtb12WQBqQUTRWqVcNli8a373PJi4hCSCbCJ2eAYKYeU9qpl-ajuPEbHn2XuKMsBmDaewWgzMBY8WynWh7lvdSt5KkAXRfe0UNySjdpk5h3MH3XjuAXcg)

Type
- Client-side Hook
- Service-side Hook

#### Client-side Hook

Update the hooks files in the `.git>hooks` director to create a new client side hooks.

Configuring hooks outside `.git` folder.
```
➜ example-js-project git:(master) ✗ git config --local core.hooksPath .githooks
 example-js-project git:(master) ✗ mkdir .githooks
➜  example-js-project git:(master) ✗ mv .git/hooks/pre-comit .githooks/
mv: rename .git/hooks/pre-comit to .githooks/pre-comit: No such file or directory
➜  example-js-project git:(master) ✗ mv .git/hooks/pre-commit .githooks/
➜  example-js-project git:(master) ✗ chmod +x .githooks/pre-commit 
```

#### Server-side Hook
Create or clone a bare repo.
Create hooks in the .git/hooks file (hooks/pre-receive) file
Make this executable $ chomd +x hooks/pre-receive
After this pushing changes to the remote repo will run this test.
Creating Custom Git Commands


Content of git-testscript file:
```
#!/bin/bash
echo "Test script worked"
```

Can create git-subpull to pull submodules 

## Git-bisect
Enables us to see when bad code added to our repo & who added.  
[Pluralsite tutorial](https://app.pluralsight.com/course-player?clipId=b23cf86d-0947-471b-b5e4-d798c68b82e9)

Mark start & stop then run the test


