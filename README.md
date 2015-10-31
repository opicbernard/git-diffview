<div style="float: right; margin-top: 10px;">
	[![The GNU General Public License v3.0](http://www.gnu.org/graphics/gplv3-127x51.png)](http://www.gnu.org/licenses/gpl.html)
</div>
# git-diffview
A bash script to show the changes between two git paths as a treeview.

## Installation

```code
sudo curl https://raw.githubusercontent.com/opicbernard/git-diffview/master/git-diffview -o /usr/local/bin/git-diffview
sudo chmod +x /usr/local/bin/git-diffview
```

## Usage

```code
git diffview [<path> [<path>]]
```

## Suggestion

Add the following line into the [alias] section of your ~/.gitconfig file.

```code
dv = diffview
```

Doing so, you can also use the command like this:

```code
git dv [<path> [<path>]]
```

## Rationale

Let's suppose that you just pulled the changes from a git repository,
and would like to know what happened between the two last commits.

Using the git dialect, this will correspond to what changed between HEAD, and HEAD~.

| HEAD~  | | HEAD | | HEAD~ | | HEAD | 
| :--: | ---- | :--: | ---- | :--: | ---- | :--: |
| ⭣ | .... | ⭣ | _&nbsp;&nbsp;&nbsp;&nbsp;or&nbsp;&nbsp;&nbsp;&nbsp;_ | ⭣ | .... | ⭣ |
| previous | | last | | commit | | commit |
| commit | | commit | | n-1 | | n |

This is what **git diffview** will show you by default.

```code
user@dev:~/project [master]$ git diffview↲
root
├── node-A
│   ├── node-B
│   │   ├── leaf-1
│   │   └── leaf-2
│   └── node-C
│       └── leaf-3
└── node-D
    └── leaf-4
```

In the above resulting treeview, you'll easily see that some work has 
been done on leaf-1, leaf-2, leaf-3, and leaf-4, under the root 
directory in the master branch of the project.

It's now straigthforward to visualize what part of the project tree get 
touched.

If you're looking for changes elsewhere in the git history, you can add 
one or two additional parameters.

Each of these parameters can be a commit reference (HEAD, or SHA-1 
based), or a branch name, as in the **git diff** command.

For example, use **git diffview HEAD~2** for the changes between 
commits n and n-2, or **git diffview HEAD~2 HEAD~4** for those between 
commits n-2, and n-4.
