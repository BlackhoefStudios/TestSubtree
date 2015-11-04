### Using Subtree modules

To include a library as a subtree, follow these steps:

	1. Add the project as a remote
	   git remote add <remote-name> <source-repo>

	2. Fetch the remote
	   git fetch <remote-name>

	3. Add the project
	   git subtree add --prefix "path/to/project" <remote-name> <remote-branch-name> --squash

Notes about this process:

	* Path separators must be forward-slash as Windows git breaks otherwise. To allow this, quote paths.
	* Using SourceTree to achieve this currently doesn't work because it will pass back-slashes.
	* Afterwards, SourceTree won't list the subtree until you try to "Add/Link" it from its UI.
	* Squashing the commits (--squash) reduces all source repo commits to one simple commit (doesn't spam your main list).

To push changes made in the subtree upstream to the source repo, use:

	git subtree push --prefix "path/to/project" <remote-name> <remote-branch-name>

If the upstream repo currently has <remote-branch-name> checked out, THIS WILL FAIL. So instead, make sure the source
repo has an extra branch to receive any pushes.

Suggested pattern:

	* Have "develop" and "master" branches.
	* In the upstream/source repo, always work on "develop".
	* In downstream/dependent repo, always push to "master".

Assuming you have "master" in the upstream/source repo checked out, it's a simple case of merging back to "develop" to
have everything synced up again:

	git checkout develop
	git merge master

Pulling remote changes is a little simpler:

	git subtree pull --prefix "path/to/project" <remote-name> <remote-branch-name> --squash

Again, the commits are squashed.