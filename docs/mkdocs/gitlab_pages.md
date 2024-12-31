# Setting Up GitLab Pages

1. Create a GitLab repo
    - Create from template -> Pages/Plain HTML.
2. Set up `Deploy -> Pages`
    ```yaml
    image: busybox

    pages:
      stage: deploy
      script:
        - echo "The site will be deployed to $CI_PAGES_URL"
      artifacts:
        paths:
          - public
      rules:
        - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    ```
    Reference: https://gitlab.com/pages/plain-html

    Now, everything under `public/` will be deployed to GitLab Pages.

3. `Deploy -> Pages -> Use unique domain` untick to make the URL shorter.
4. `Settings -> Access Tokens -> Add new token`, `write repository` scope, Maintainer role
6. (Optional) If you want to make the documentation public, `Settings -> General -> Visibility (expand) -> Pages -> Everyone`


## GitHub repo setup

1. `Setting -> Secrets and variables -> Actions` -> Add `New repository secret`
    - Name: `GITLAB_TOKEN`
    - Secret: GitLab access token
2. `Setting -> Secrets and variables -> Actions` -> Variables -> Add `GITLAB_PROJECT`
    - Name: `GITLAB_PROJECT`
    - Value: Name of the GitLab docs repo (e.g. gitlab-user/my-project-docs)
    - Warning: it's not the URL of the documentation. It's the name of the repository with the username.

## GitHub Actions

Use the following GitHub Actions to deploy MkDocs to GitLab Pages. If you omit the gitlab-related settings, it will be published to GitHub on the `gh-pages` branch.

```yaml
name: Manually deploy MkDocs

on:
  workflow_dispatch:
    inputs:
      version-tag:
        description: Version tag
        required: true
        default: v0.1.0

jobs:
  deploy-mkdocs:
    uses: deargen/workflows/.github/workflows/deploy-mkdocs.yml@master
    with:
      requirements-file: requirements.txt
      version-tag: ${{ github.event.inputs.version-tag }}
      deploy-type: tag
      gitlab-project: ${{ vars.GITLAB_PROJECT }}
      gitlab-branch: master
    secrets:
      GITLAB_TOKEN: ${{ secrets.GITLAB_TOKEN }}
```

```yaml
name: Deploy MkDocs on latest commit

on:
  push:
    branches:
      - main
      - master

jobs:
  deploy-mkdocs:
    uses: deargen/workflows/.github/workflows/deploy-mkdocs.yml@master
    with:
      deploy-type: latest
      requirements-file: requirements.txt
      gitlab-project: ${{ vars.GITLAB_PROJECT }}
      gitlab-branch: master
    secrets:
      GITLAB_TOKEN: ${{ secrets.GITLAB_TOKEN }}
```
