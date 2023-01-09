# symfony-recipes

Collection of 7thSENSE Symfony Recipes

## Installation

Update your projects composer.json

```json
{
    "config": {
        "gitlab-domains": [
            "gitlab.7thsense.de"
        ]
    }
}
```

```json
{
    "symfony": {
        "allow-contrib": "true",
        "endpoint": [
            "https://gitlab.7thsense.de/api/v4/projects/shopware-6%2F7thsense%2Fsymfony-recipes/repository/files/index.json/raw?ref=master",
            "https://raw.githubusercontent.com/shopware/recipes/flex/main/index.json",
            "flex://defaults"
        ]
    }
}
```

- [Create a gitlab access-token](https://gitlab.7thsense.de/shopware-6/7thsense/symfony-recipes/-/settings/access_tokens) 
for the 7thsense-sw6/project-commands repository
- The token needs the right to `read_api` and `read_repository`
- Add it to your auth.json 
- Update the deployment variable for auth.json

```json
{
    "gitlab-token": {
        "gitlab.7thsense.de": "<your-gitlab-token>"
    }
}
```

Run `composer require 7thsense-sw6/project-commands` to add the package.

If the recipe is not installed, run 
`composer recipes:install 7thsense-sw6/project-commands --force`.
But watch out, it resets your `config/plugins.yaml`. 

## WIP

### Update Recipes

Install https://github.com/symfony-tools/recipes-checker

```shell
git clone https://github.com/symfony-tools/recipes-checker.git
cd recipes-checker
composer install
```

```shell
cd <symfony-recipes-folder>
../recipes-checker/run generate:flex-endpoint 7thsense-sw6/project-commands master master . < <(git ls-tree HEAD */*/*)
```

This creates json files for each symfony recipe.
Currently, it is necessary to update the template urls to our 7thsense gitlab in index.json

```json
{
    "aliases": [],
    "recipes": {
        "7thsense-sw6/project-commands": [
            "1.0"
        ]
    },
    "recipe-conflicts": [],
    "versions": [],
    "branch": "master",
    "is_contrib": true,
    "_links": {
        "repository": "gitlab.7thsense.de/shopware-6/7thsense/symfony-recipes",
        "origin_template": "{package}:{version}@gitlab.7thsense.de/shopware-6/7thsense/symfony-recipes:master",
        "recipe_template": "https://gitlab.7thsense.de/api/v4/projects/shopware-6%2F7thsense%2Fsymfony-recipes/repository/files/{package_dotted}.{version}.json/raw",
        "archived_recipes_template": "https://gitlab.7thsense.de/api/v4/projects/shopware-6%2F7thsense%2Fsymfony-recipes/repository/files/archived/{package_dotted}/{ref}.json/raw"
    }
}
```
