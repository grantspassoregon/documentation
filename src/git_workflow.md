# Git Workflow

## Make short, targeted commits

The contents of an ideal commit should address only one issue or feature. A single, concise description should be able to cover the scope of the code changes. When searching through the commit history, you will use the commit descriptions to remind yourself of the contents of each commit, so with each new commit try to consider the well-being of your future self. If you are using a tool like `git blame` to identify the commit associated with a change in code, the other changes in the that commit should be relevant to the code of concern, and not a kitchen sink of unrelated patches, features and documentation. This may mean taking the changes from a single work session and breaking them up into three or four targeted commits.

One primary reason to adopt this strategy is for automating changelog generation. Changelogs are a standard practice in the software industry, where new version releases include a log describing changes from the old version to the new. Part of the reason for their ubiquity is the existence of automatic tooling that converts commit messages from `git` into a reader-friendly changelog, called changelog generators. The current changelog generator used by our team is [`git-cliff`](https://git-cliff.org/). The important part is not so much _which_ tool we use, because they all work from the same set of commit messages. The changelog will only be as well-written as your commit messages. When you write a new commit, imagine your users reading the changelog and write a message with this audience in mind. Try reading some changelogs from software you admire and emulating their style. Use `git-cliff` to generate a changelog from your unreleased edits, and read through the output.

For a more details, see the article [Write Better Commits, Build Better Projects](https://github.blog/developer-skills/github/write-better-commits-build-better-projects/)

### Git-cliff Usage

The configuration file for git-cliff (cliff.toml) looks for certain words at the beginning of the commit message, and uses these terms to map the commit to the correct category of the changelog.

- **feat** - The commit introduces a new feature, corresponding to a minor version bump.
- **feat!** - The commit introduces a new feature that is considered a breaking change, corresponding to a major version bump.
- **fix** - The commit introduces a bug fix, corresponding to a patch version bump.
- **doc** - The commit adds documentation.
- **perf** - The commit pertains to performance improvements.
- **refactor** - The commit refactors existing code without adding or eliminating features.
- **style** - The commit adjusts code style without changing code logic or implementing new features.
- **test** - The commit pertains to unit or integration tests.
- **chore** - Categorize the commit as a miscellaneous task.

While a package is immature and still under active development, we use a major version of 0. Using a major version of zero signals to users that the package is still under development, and the user API may not be stable. When a package is in this state, breaking changes do not result in major version bumps. We have set the bump level in `cliff.toml` to `patch`, so every update increments the patch version number.

## Use a dedicated branch for development

"_Never mess with the main repo_". - Michelle Gienow

When you create a new project using `git`, the code exists in the default branch, called `main`. During development, you can create new branches to try out changes to the code without touching the main branch. When multiple contributors are working on a single project, each contributor will make the changes to their own branch, merging these changes into the main branch when they are ready. Using this method, contributors do not have to worry about the changes others are making conflicting with their own work, when and until these changes are merged. We want the main branch to contain stable, well-tested code. Users should be able to download and use the main branch without finding it in some half-complete state of revision. Keeping working changes on a separate branch helps prevent half-finished work or newly-created bugs from appearing on the main branch between releases.

The intended purpose of branches is to permit you to develop features or changes to existing code safely, "off to the side", merging them back into the main project only after they have been fully tested and reviewed.

### Check Existing Branches

Use the command `git branch -a` to list all of the branches associated with a project. The output will show an asterisk next to the current branch.

### Checkout a New Branch

Use the command `git checkout -b yourBranchName` to create a new branch, here named `yourBranchName`. The `checkout` command switches you to the named branch, and the `-b` flag creates the branch at the same time.

Note that you can also create a branch using the command `git branch yourBranchName`, but this command will not move you to the new branch, and you will still have to enter the command `git checkout yourBranchName`. Passing the `-b` flag to `git checkout` is more concise, and prevents errors from the user creating a branch and forgetting to switch to it.

To switch back to the `main` branch, use the command `git checkout main`.

### Committing Changes to a Branch

The process for committing changes to a branch is identical to working with the `main` branch:

- Use the command `git add` to add changes to the tracked files for the repo.
- Then use the `git commit` command to commit the added changes.
- Finally use the `git push` command to push the committed changes up to Github.

See the [Using git](./using_git.md) section for more details.

### Merging Branches

When the code on your development branch is ready to move into the production branch, it is time to merge branches. When you run the merge command, you are pulling code from another branch into the branch you are currently working in. Since we want to move changes from the development branch into the main branch, we need to switch back to main before running the merge. Switch from the development branch back to the `main` branch using the command `git checkout main`.

To begin the merge, run the command `git merge yourBranchName`.

If you are on the happy path, the merge is successful. The final step is to push the merge up to the Github repo using the command `git push`.

If you are not on the happy path, then you are reading an error message that says something about a "merge conflict". This is a potentially deep rabbit hole, too deep to address here. To get an introduction, check out the article [Git Merge Conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts). The best strategy to deal with merge conflicts is to avoid them. Ensure your development branches are based off the current `main` branch. Use the `git pull` command to ensure your version of `main` is up-to-date. Merge conflicts occur when the `main` branch diverges from the version of the `main` branch that the development branch is based upon.

After merging the development branch, it is best practice to delete the development branch. Rather than using a single development branch called "erik" or "draft", best practice is to name the branch in some way after the work being done, such as "parser" or "unit-tests". When looking through the merge history of your repo, descriptive branch name will help to understand where and why changes have occurred, without having to dig into the details of the commits. Delete a development branch using the command `git branch -d yourBranchName`. The `-d` flag communicates that you would like to delete the indicated branch.

For more details on using development branches, see the article [How to Work With Branches in Git and Github](https://thenewstack.io/dont-mess-with-the-master-working-with-branches-in-git-and-github/).

Note that this article advocates for disabling the default `git` merge behavior of fast-forwarding commits. We are electing to keep the default fast-forward behavior, without a strong compelling reason to do so. Feel free to revisit this policy as needed.
