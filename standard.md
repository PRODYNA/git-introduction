# Standard fail-safe worfklow

## Create issue an branch n GitHub/GitLab/Bitbucket

* Create an issue or pick an existing one.
* Create a new branch from `main` with the issue number and a short description.

## Local development

* Update local repository with `main` branch.

```sh
git checkout main
git pull
```

This will also give you the branch from the remote repository.

* Switch to your feature branch.

```sh
git checkout feature/issue-123-description
```

* Develop your feature or fix.
* Stage and commit your changes.

```sh
git add .
git commit -m "Fix issue #123: Description"
```

* Push your branch to the remote repository.

```sh
git push origin feature/issue-123-description
```

## Pull request

* Create a pull request on GitHub/GitLab/Bitbucket.
* Assign reviewers and add labels.
* Wait for the CI/CD pipeline to pass.
* Merge the pull request after approval.
* Delete the feature branch.
* Update your local repository with the latest changes.

```sh
git checkout main
git pull
```
