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
* `npm install` needed to create the package-lock.json file later required by `npm ci`

## Publish
* `npx lerna version --conventional-commits --yes`
* `npx lerna publish from-git --yes`

## CI/CD
* Checkout requires the following variables to be set in order to write to the repo
```
- name: "Checkout"
        uses: actions/checkout@v3
        with: 
          fetch-depth: 0
          token: ${{ secrets.PAT }}
```
* Node setup needs to the following to properly set for a private registry
```
- name: "Setup Node environment"
        uses: actions/setup-node@v3
        with:
          node-version: '16.x'
          registry-url: 'https://npm.pkg.github.com'
          scope: '@private-registry-name'
        env:
          NODE_AUTH_TOKEN: ${{ secrets.PAT }}
```
* Needs to the following git setup to create a user
```
- name: "Setup git"
        run: |
          git config --global user.name "${{ github.actor }}"
          git config --global user.email "${{ github.actor}}@users.noreply.github.com"
```