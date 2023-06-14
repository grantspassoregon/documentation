# Using git

This section describes how to use `git` commands to download code from the GitHub repository onto your local machine, make changes to this code and then upload these changes back onto the repository, as well as how to make a new repository and associate it with the GitHub account.  We introduce the most common commands that you will use to manage the code base.  Although `git` offers many additional features, and you are welcome to use these features to improve your productivity, the following commands should be sufficient for a new user to set up a basic workflow.

## Cloning a Repository (git clone)

GitHub offers centralized cloud-based code storage that allows users of an organization to collaborate across multiple locations.  Changes made to the code from an individual computer synchronize the with the centrally-stored code database, ensuring that all users are able to access a shared version.  The first step in gaining access to the shared code is to make a local copy of the relevant GitHub project onto your local machine, a process called "Cloning a Repository."

The City of Grants Pass organizational account is located at [https://github.com/grantspassoregon/](https://github.com/grantspassoregon/). This account hosts projects related to the GIS Division.  Each project is an independent repository that you may elect to download to your local machine.  If you select a repository by clicking on its link, the file tree of the main branch will load onto the screen.  Clicking on the green `<> Code` button displays a dropdown field showing the download path to use in order to clone the repository.  The image below shows the download path to the `documentation` repository, which holds the source for this markdown book.

![Clone by SSH](./images/clone_repository_ssh.png)

Running the `clone` command will download and install the specified code into the current working directory.  You may wish to create a dedicated directory on your machine for storing repositories on your system, such as a `repos` directory in `C:\Users\%Username%\`.  First, navigate to this directory in the terminal:

```
  cd c:/users/%Username%/repos
```

Then make a local copy of the selected repository, in this case `documentation`, using the `clone` command:

```{bash}
git clone git@github.com:grantspassoregon/documentation.git
```

This command will create a folder with the same name as the project in the working directory.  You can view the downloaded files by navigating into the directory (e.g. `cd documentation`) or by opening the files directly into your favorite code editor.

## Updating Your Local Version (git pull)


## Adding Locally-Hosted Code to a New Repository

As the scope and duties of the GIS Division change over time, we create new projects to meet the changing needs of the City government. The easiest method to add a new project to the GitHub account is to begin with code hosted on your own machine, and then to push this code into an empty repository on GitHub using the CLI.
Referring to the [docs](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github):

* Create a new repository on GitHub.com.
  * Click the new repository button:
  ![New Repository Button](./images/new_repository_button.png)
  * Enter the name of the new project:
  ![Create New Repository](./images/create_new_repository.png)
  * Unless there are overriding privacy concerns, a Public repository is standard.
  * Do not initialize the new repository with a README, license, or gitignore files.  Leave it empty.
  * An empty repository prevents merge errors when uploading the code hosted on the local machine.
* At the top of the new Quick Setup page for the new repository, copy the remote repository URL.
  ![Remote Repository URL](./images/remote_repository_url.png)
* Open Git Bash or the Alacritty terminal and navigate to the local project directory.
  * Ensure that the local repository is committed and ready to push.
    * If the code is not set up as a git repository, run `git init`.
    * Run `git status` and add any outstanding changes using `git add .`.
    * Commit the changes using `git commit -m "descriptive message"`.
* Link the local directory to the remote repository:
  ```{bash}
  # replate <remote-URL> with the URL copied from the Quick Setup page on GitHub.com
  git remote add origin <remote-URL>
  # change the default branch name to "main"
  git branch -M main
  # push the contents of the local directory to the remote repository
  git push -u origin main
  ```

