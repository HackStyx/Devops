## Initializing a Repository

* `git init` - Initialize a new Git repository.

## Configuring User Information

* `git config --global user.name "Your Name"` - Set the username for commits.
* `git config --global user.email "you@example.com"` - Set the email for commits.
* `git config --list` - Verify the configuration settings.

## Creating a Personal Access Token (PAT)

1. Go to GitHub Settings > Developer settings > Personal access tokens > Fine-grained tokens.
2. Click **Generate new token** and provide a descriptive name.
3. Select the scopes and permissions required (e.g., repository access, workflow, etc.).
4. Click **Generate token** and copy the token. Store it securely as it will not be shown again.

## Staging and Committing

* `git add .` - Stage all changes for commit.
* `git commit -m "initial commit"` - Commit changes with a message.

## Checking Status

* `git status` - Show the current working tree status.

## Managing Remotes

* `git remote add origin <repo_url>` - Add a remote repository.
* `git remote -v` - Verify remote URLs.
* `git remote set-url origin <new_url>` - Change the remote repository URL.

  > Example: `git remote set-url origin https://{PAT}@github.com/<username>/<repository>.git`

## Pushing Changes

* `git push -u origin master` - Push local changes to the remote repository and set tracking.
