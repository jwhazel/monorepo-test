# Test monorepo

## Setup
* `git init`
* `npm init`
* `npx lerna init`
* `"private": true` in root package.json (unclear if this is needed)
* /packages/{packagename}/package.json 

      "publishConfig": {
          "registry": "https://npm.pkg.github.com"
      }
* `npm login --registry=https://npm.pkg.github.com` - better way to handle this?

## Publish
* `npx lerna version`
* `npx lerna publish from-package`