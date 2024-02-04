##### Project from Scratch

1. Initialize the project as a git repository. By default the initial branch is called master. But we can change this using the -b option as shown below
```bash
	$ cd MyProj

	$ git init 
		or
	$ git init -b main 	
		or
	$ git init && git symbolic-ref HEAD refs/heads/main` If you’re using Git 2.27.1 or an earlier version

```
2. Add the files in your new local repository. This stages them for the first commit.
```	bash
	$ git add .

	# To unstage a file, use 
	$ git reset HEAD YOUR-FILE
```
3. Commit the files that you've staged in your local repository.
```bash
	$ git commit -m "First commit"
	
	# To remove this commit and modify the file, use 
	$ git reset --soft HEAD~1 	
	and commit and add the file again
```
4. Create a new repository on GitHub.com. To avoid errors, do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.
5. At the top of your repository on GitHub.com's Quick Setup page, click to copy the remote repository URL
6. In Terminal, add the URL for the remote repository where your local repository will be pushed.
```bash
	$ git remote add origin <REMOTE_URL>
	 (Sets the new remote)
	 
	$ git remote -v
	(Verifies the new remote URL)
```
7. Push the changes in your local repository to GitHub.com.
```bash
	$ git push -u origin main
	(Pushes the changes in your local repository up to the remote repository you specified as the origin)
```

##### Example

for the dotfiles repo we did the following

```bash
$ cd dotfiles
$ git init -b main
$ git add .
$ git commit -m "neovim and tmux configuration"
$ git remote add origin https://github.com/narayanbs/dotfiles.git
$ git push -u origin main
```


##### Creating a Remote Repository on github

* Login to github account. 
* In the upper-right corner of any page, use the  drop-down menu, and select New repository.
* Type a short, memorable name for your repository. For example, "hello-world".
* Optionally, add a description of your repository. For example, "My first repository on GitHub."
* Choose a repository visibility
* Select Initialise this repository with a README. (if needed)
* Click Create Repository.

##### Creating Access tokens on github

* First of all, you must create a personal Access Token on GitHub. To do so follow the steps below:
* Click on your GitHub profile icon on the top right corner
* Click Settings
* From the menu shown on the left, click Developer Settings
* Click Personal access tokens
* Click Generate new token
* Add a note that will help you identify the scope of the access token to be generated
* Choose the Expiration period from the drop down menu (Ideally you should avoid choosing the No Expiration option)
* Finally, select the scopes you want to grant the corresponding access to the generated access token. Make sure to select the minimum required scopes otherwise you will still have troubles performing certain Git Operations.
* Finally click Generate Token
