# JS Node Script Template

[![License](https://img.shields.io/github/license/Player1os/js-node-script-template.svg)](https://github.com/Player1os/js-node-script-template/blob/master/LICENSE)
[![NodeJS version](https://img.shields.io/badge/node%20version-v10.15.3-brightgreen.svg)](https://nodejs.org/dist/v10.15.3/)

A template project from which simple scripts written in Javascript for NodeJS can be derived.

These scripts usually serve as a cross-platform replacement for shell scripts that automate specific tasks and are intended to be executed
directly. Projects derived from this template are not meant to be *tested* nor *published*. There are no non-standard restrictions to the
project's file structure.

## Contents

This project contains an `.eslintrc.json` file, which references a common configuration for *eslint* used in all derived
Javascript projects. This configuration file is intended for use within the **VSCode** editor, using the `dbaeumer.vscode-eslint` extension.

## Creating a new project

Follow these instructions to create a new project based on this template:

1. Create a new repository for the project and clone it locally, by running:

	```
	git clone REPOSITORY_URL
	```

1. Add the template's `origin` remote to the newly created project as an additional remote repository named `base`, by running:

	```
	git remote add base git@github.com:Player1os/js-node-script-template.git
	```

	Alternatively, we can use the HTTPS url, if an ssh connection cannot be established, by running:

	```
	git remote add base https://github.com/Player1os/js-node-script-template.git
	```

1. Pull the latest commits of the `master` branch from the newly set `base` remote, by running:

	```
	git pull base master
	```

1. Make sure to change the default values found in the following files:

	- `package.json`
		- `name`
		- `description`
		- `repository.url`
		- `keywords`
		- `bugs.url`
		- `homepage`
	- `README.md`

1. Propagate these changes to the `package-lock.json` file while installing all required dependencies, by running:

	```
	npm i
	```

1. Apply any other changes required by the new project. When done, commit them, by running:

	```
	git add .
	git commit -m "Transform the template boilerplate into the the project's initial form"
	```

1. Push the local `master` branch and set it to track the remote `origin/master` branch, by running:

	```
	git push -u origin master
	```

## Creating a copy of an existing project

Assuming we have already [created a new project](#creating-a-new-project) as described above, we can create a new copy of the project
(on a different machine, for instance), by following these steps:

1. Create a local clone from the `origin` remote repository, by running:

	```
	git clone REPOSITORY_URL
	```

1. Add the template's `origin` remote to the project as an additional remote repository named `base`, by running:

	```
	git remote add base git@github.com:Player1os/js-node-script-template.git
	```

	Alternatively, we can use a modified version of the URL, if the ssh connection needs to be tunneled, by running:

	```
	git remote add base ssh://git@ssh.github.com:443/Player1os/js-node-script-template.git
	```

1. Fetch the newest version of the `base` repository's branches, by running:

	```
	git fetch base
	```

	This should only download the `master` branch of the `base` repository.

1. Install all of the project's required dependencies, by running:

	```
	npm i
	```

## Implementing a change to the project

Whether we are adding a feature or fixing a bug, it is recommended to follow these steps while doing so:

1. Checkout the `master` branch of the project, by running:

	```
	git checkout master
	```

1. Create and checkout a new, appropriately named topic branch, by running:

	```
	git checkout -b XYZ
	```

1. Apply the desired changes into the newly created topic branch. If any changes occurred in the `master` branch while we were still
working on the topic branch, pull these changes and rebase the topic branch, by running:

	```
	git checkout master
	git pull
	git checkout XYZ
	git rebase master
	```

	It is recommended to do this as soon as possible when the `master` branch is updated to minimize the amount of conflicts that need
	to be addressed at any given time.

1. When done, make sure all changes to the topic branch are pushed to the remote `origin` repository, by running:

	```
	git push -u origin XYZ
	```

1. Optionally, we may want to *squash* or otherwise reorganize the branch's commits before publishing them, thus producing a more
readable commit history, by running:

	```
	git rebase -i master
	```

	It is recommended to check the repository's *git history* after the interactive rebase operation, to make sure we've achieved
	the desired changes.

1. Using the remote `origin` repository's interface, create a **pull request** from the topic branch back to the `master` branch.

1. Since the topic branch has already been rebased to the newest version of the `master` branch, there will be no conflicts and the
topic branch can be simply merged by fast-forwarding the `master` branch.

1. Delete the local topic branch after checking out and pulling the newest version of the `master` branch, by running:

	```
	git checkout master
	git pull
	git branch -d XYZ
	```

1. If the `origin` remote repository has already deleted its topic branch during the **pull request** operation, the local remote refs
can simply be fetched and pruned, by running:

	```
	git fetch -p
	```

	Otherwise, we need to remove the `origin` remote topic branch manually, by running:

	```
	git push -d origin XYZ
	```

## Update the project's version

At some point (usually after [implementing one or more changes to the project](#implementing-a-change-to-the-project), as described above)
we may want to update the project's version, by running:

```
npm version [patch | minor | major]
```

The corresponding `preversion` and `postversion` scripts defined in the `package.json` file ensure that the *new version* value is stored
in all the relevant locations, which include:

- Modifying the `package.json` and `package-lock.json` files.
- Tagging in the latest `master` branch commit.

## Updating the project with changes from the template

We can apply any changes introduced to the template after a project has been derived from it, by running:

```
npm run update-base-create
```

This rebases the `master` branch of the project's repository to the newest commit of the template's `master` branch, creating a new tree.
This new tree is then pushed to to the `origin` remote repository. The script also ensures all of the repository's tags remain unchanged
during this process and any newly introduced dependencies are installed.

As is the case with any rebase operation, it is recommended that we check the current *git history*, to make sure the update has been
applied correctly.

Optionally, we may wish to [update the project's version](#update-the-project%27s-version) as explained above.

If the project is being developed on another machine, the local repository on it will need to be updated, by running:

```
npm run update-base-load
```

This overwrites the local repository tree with the contents of the newly rebased tree located in the `origin` remote repository and
ensures any newly introduced dependencies are installed.

## Debugging

The following **VSCode** debugger configurations can be used in derived projects:

- **[Node] Current file** to debug the currently open Javascript file.

## Inherited development assets

This project inherits development assets from the following projects:

- [@player1os/javascript-support](https://github.com/Player1os/javascript-support)
