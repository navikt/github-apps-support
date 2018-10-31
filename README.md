Github Apps Support
===================

This project aims at providing scripts that help you in using Github Apps from services like Jenkins or Travis.

## Getting started

Clone the project and make the scripts available to your `$PATH` for ease of use.

```
git clone https://github.com/navikt/github-apps-support.git
export PATH=`pwd`/github-apps-support/bin:$PATH
```

### Getting an installation token

Generate an installation token by [authenticating as a Github App](https://developer.github.com/apps/building-github-apps/authenticating-with-github-apps/) using a signed JWT.
```bash
INSTALLATION_TOKEN=$(generate-installation-token.sh `generate-jwt.sh "$PRIVATE_KEY" $APP_ID`)
```

The private key must be kept secret, e.g. encrypting it and placing it in your code. 
Travis lets you do this quite easy via `travis encrypt-files`:
https://docs.travis-ci.com/user/encrypting-files/

Depending on the permissions you set on your Github App you can now the installation token when communicating with the API
or when pushing commits:

```bash
git clone https://x-access-token:<token>@github.com/owner/repo.git
```

### Permissions

Unsure what permissions you need for the different API endpoints? [Check out the documentation](https://developer.github.com/v3/apps/permissions/).

### Creating commits on the command line

If you want to create commits using `git`, make sure you configure the committer with the name
and email of your Github App. If you have an app called `My Team` then the name and email 
would be `my-team[bot]` and `my-team[bot]@users.noreply.github.com`

```bash
git config user.name my-team[bot]
git config user.email my-team[bot]@users.noreply.github.com
```

### Requirements

Some of the scripts needs `openssl` and `jq` (both of which are pre-installed on Travis).

# Contact

Code related questions may be asked using GitHub Issues.
