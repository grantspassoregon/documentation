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

