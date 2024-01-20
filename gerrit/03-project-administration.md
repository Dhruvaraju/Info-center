- [Creating a Project](#creating-a-project)
- [Creating branches and Tags](#creating-branches-and-tags)
- [Creating tags](#creating-tags)
- [Access Controls](#access-controls)

## Creating a Project

- Navigate to Browse > Repositories > Create New
- A pop up will appear as shown below

![create-project.png](images/create-project.png)

- Enter repository name of your choice
- select a default branch main or master
- Inherit the right as it is an optional field leave it as it is.
- In the owner textbox choose the owner name.
- Set the 'Create initial commit' to true.
- Only serve as parent: meaning this repo will be used as a parent repo for other repos so choose the option based on your need.
- Click on cerate and it will create a new project.

## Creating branches and Tags

- Branches and tags can be created by git push command or from gerrit UI
- To create a new branch, click on branches from project page
- Click on create new a pop up will appear as below

![create-branch.png](images/create-branch.png)

Provide Branch name and which branch it should be created from, then click create.

## Creating tags

- Tags can also created in the same way.
- Click on Create New and provide information and click create
  ![create-tag.png](images/create-tag.png)

## Access Controls

These are vital parts of security. They enable of the projects and define what users can or cannot do.

- Controlled per project basis
- Access controls can be controlled on access settings page for a project.
- Access controls can be inherited from other projects.
- They are normally inherited by a project called All Projects by Default, where access settings can be altered for administrator access to all projects created
- More information on project settings can be found at: https://gerrit-review.googlesource.com/Documentation/access-control.html
