# git

> Distributed version control system.
> More information: <https://git-scm.com/>.

- Check the Git version:

`git --version`

- Call general help:

`git --help`

- Call help on a command:

`git help {{command}}`

- Execute Git command:

`git {{command}}`

- Remove last commit keep changes:

`git reset HEAD^`


# https://stackoverflow.com/questions/7103631/how-to-unstage-large-number-of-files-without-deleting-the-content
- Unstaged and keep changes:

`git reset`

- Unstaged and discard changes:

`git reset --hard`


- Stage all unstaged changes:

`git add -u`

- Compare commits Azure DevOps https://stackoverflow.com/questions/59533905/azure-devops-compare-two-commits-right-in-the-web-ui

# Run git pull over all subdirectories
# https://stackoverflow.com/questions/3497123/run-git-pull-over-all-subdirectories?noredirect=1
# Copy output to file and edit and paste in
`find ./ -maxdepth 1 -type d -exec echo git -C {} pull \;`