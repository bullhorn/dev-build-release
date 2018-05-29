# dev-build-release

> Small script to append the build number to the version number

## Usage

You must use `scripts` in a folder with a `package.json` and a remote to push to.

`dev-build-release -b BUILD_NUMBER -g BRANCH_NAME`

Updates version of package.json to a "feature" branch version schema

`dev-build-release -b BUILD_NUMBER`

Updates version of package.json to a "development" branch version schema

# determine-version

> Outputs message about what repositories to update and what the version of this project should be

## Usage

`determine-version`

Outputs dependency version range that should be used in repos that depend on your repo

`determine-version -p comma-delimited,list,of-parent-repos`

Outputs message of what repos should be updated and what version range should be used

## Post Commit Git Hook
To make repository print out this message whenever a user makes a commit

* Add dev-build-release and ghooks as dependencies to package.json
```
npm install ghooks dev-build-release --save-dev
```

* In package.json, add the following configurations. Replace `<parentRepos>` with names of repos that depend on your repo

```
"scripts": {
    "determineVersion": "node ./node_modules/dev-build-release/bin/determine-version -p <parentRepos>",
},
"config": {
    "ghooks": {
        "post-commit": "npm run determineVersion"
    }
}
```

# generate-version-file

> Generates a version.json file based on package.json and other build information

## Usage

`generate-version-file`

## Post Build Step

* Add dev-build-release as a dependency to package.json
```
npm install dev-build-release --save-dev
```

* In package.json, add the following to "scripts"

```
"scripts": {
    "version-file": "node ./node_modules/dev-build-release/bin/generate-version-file"
}
```