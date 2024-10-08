## **Setup**

##### 1. Install the package as dev dependency

```
   npm install --save-dev standard-version
```

##### 2. Add a project name, initial version and a release script to your `package.json`:

```json

   { 
	   "name": "your-project-name", 
	   "version": "0.0.0", 
	   "scripts": { "release": "standard-version" }
    }
```

The `package.json` file must contain an initial version number for `standard-version` to work.

## **Workflow**
##### 1. Make commits

- Valid commits:
    - `git commit -m "feat: add new user login feature"`
    - `git commit -m "fix: resolve issue with navigation bar"`
- Non-impactful commits:
    - `git commit -m "chore: update dependencies"`
    - `git commit -m "docs: update README"`

##### 2. Run release script to update version and changelog

```
   npm run release
```

**This command will do the following:**

- Analyze your commit messages to determine the type of version bump.
- Update the version in `package.json`.
- Generate or update the `CHANGELOG.md` file with the commits since the last release.
- Create a new Git tag for the release.


Output:

- The `feat` and `fix` commits will be included in the changelog and determine the version bump.
- The `chore` and `docs` commits will not affect the version number or appear in the changelog.
 
##### 3. Push changes with tags

```
   git push --follow-tags origin your_branch_name
```


### How `standard-version` works

**Commit Messages**
`standard-version` relies on conventional commit messages. For example:

- `feat: add new user login feature` (minor release)
- `fix: resolve issue with navigation bar` (patch release)
- `BREAKING CHANGE: refactor API endpoints` (major release)

**Controlled Release Process**
It does not update the version or changelog on every commit. 
Instead, it performs these updates when you run the `standard-version` command (`npm run release`), 
allowing you to control when to create a new release.

**Conclusion**
`standard-version` is designed to work with conventional commits, focusing on significant changes like features and fixes. Commits without the recognized prefixes (`feat`, `fix`, etc.) will be ignored for versioning and changelog purposes by default. This ensures that your changelog and version bumps reflect meaningful updates to your project.

#### Version Bumping
In `standard-version`, version bumping is determined by the type of commits made since the last release. The default setup follows the principles of Semantic Versioning ([SemVer](https://semver.org/)):

1. **Patch Version (X.Y.Z) Bump**: This is triggered by `fix` commits.
2. **Minor Version (X.Y.0) Bump**: This is triggered by `feat` commits.
3. **Major Version (X.0.0) Bump**: This is triggered by `BREAKING CHANGE` notes in any commit, regardless of the commit type.

**`Standard-version` applies special rules to pre-1.0.0 versions:**
- **`0.0.x` versions**: All types of changes will bump only the patch number (`0.0.1`, `0.0.2`, etc.).
- **`0.x.0` versions**: A `feat` will bump the minor version to `0.x.0`, and a `fix` will bump the patch version to `0.x.y`.
- **`1.0.0` and beyond**: Once the version hits `1.0.0`, the standard SemVer rules apply: `fix` for patch bumps, `feat` for minor bumps, and `BREAKING CHANGE` for major bumps.

#### Manually Setting Project Version with `standard-version`

In some cases, you may want to manually set your project's version rather than relying on the automatic version bumping provided by `standard-version`. This guide explains how to manually bump your project's version and ensure your changelog and Git tags are correctly updated.

##### **Steps to Manually Set the Version**

 1. **Manually Bump the Version**
	To manually set the version of your project, use the `npm version` command. This is useful when you want to jump to a specific version, such as moving from a pre-release version to `1.0.0`. 

	 Example: Moving from `0.0.1` to `1.0.0`

	```
	npm version 1.0.0
	```

	This command will:
	- Update the `version` field in your `package.json` to `1.0.0`.
	- Create a new commit with the message `v1.0.0`.
	- Create a new Git tag `v1.0.0`.

2. **Update the Changelog and Tag Using `standard-version`**
	After manually setting the version, you can run `standard-version` to update the changelog and apply any additional release-related changes.
	
	```
	npm run release -- --first-release
	```
	
	The `--first-release` flag informs `standard-version` that this is the first release or a major version milestone, so it will start the changelog from this version (`1.0.0` in this case).

3. **Push Changes to Your Git Repository**
	Finally, push the changes, including the new tag, to your Git repository to share them with your team or deploy the release.
	
	```
	git push --follow-tags origin your_branch_name
	```
	
	This command pushes both the commit and the new Git tag to the repository.

##### **Recap of the Steps**

1. **Manually bump the version** using `npm version <version>` to set the desired version.
2. **Run `standard-version`** with the `--first-release` flag to update the changelog and create a release tag.
3. **Push changes and tags** to your Git repository using `git push --follow-tags`.


### Customizing `standard-version`

You can customize the behavior of `standard-version` by creating a `.versionrc` file or by adding a `standard-version` field in your `package.json`. This allows you to configure things like:

- Pre-release and post-release scripts.
- Different changelog file locations.
- Custom tag prefixes.


**Example of a `.versionrc` File**

This `.versionrc` file customizes `standard-version` to include additional commit types and defines some scripts to run at various stages of the release process.

```json
   {
  "types": [
    { "type": "feat", "section": "Features" },
    { "type": "fix", "section": "Bug Fixes" },
    { "type": "chore", "section": "Chores", "hidden": false },
    { "type": "docs", "section": "Documentation", "hidden": false },
    { "type": "style", "section": "Styles", "hidden": false },
    { "type": "refactor", "section": "Code Refactoring", "hidden": false },
    { "type": "perf", "section": "Performance Improvements" },
    { "type": "test", "section": "Tests", "hidden": false }
  ],
  "scripts": {
    "postbump": "npm run build",
    "prerelease": "npm test",
    "postrelease": "echo Post-release script!"
  },
  "tagPrefix": "v"
}
```


**Example of a `package.json` File with `standard-version` Field**

This `package.json` file includes a `standard-version` field with the same customizations as the `.versionrc` file. The custom scripts and commit types are defined directly within the `package.json`.

```json
{
  "name": "your-project-name",
  "version": "1.0.0",
  "description": "Your project description",
  "main": "index.js",
  "scripts": {
    "start": "vite",
    "build": "vite build",
    "test": "jest",
    "release": "standard-version"
  },
  "devDependencies": {
    "standard-version": "^9.3.0"
  },
  "standard-version": {
    "types": [
      { "type": "feat", "section": "Features" },
      { "type": "fix", "section": "Bug Fixes" },
      { "type": "chore", "section": "Chores", "hidden": false },
      { "type": "docs", "section": "Documentation", "hidden": false },
      { "type": "style", "section": "Styles", "hidden": false },
      { "type": "refactor", "section": "Code Refactoring", "hidden": false },
      { "type": "perf", "section": "Performance Improvements" },
      { "type": "test", "section": "Tests", "hidden": false }
    ],
    "scripts": {
      "postbump": "npm run build",
      "prerelease": "npm test",
      "postrelease": "echo Post-release script!"
    },
    "tagPrefix": "v"
  }
}
```

**Key Components Explained**

- **`types`**: Defines the commit types that `standard-version` will recognize and include in the changelog. Each type has a `section` that will be used as a heading in the changelog and a `hidden` field to determine if it should be included in the changelog.
- **`scripts`**: Defines scripts to run at various stages of the release process:
    - **`postbump`**: Runs after the version bump but before the changelog is generated.
    - **`prerelease`**: Runs before the release process begins.
    - **`postrelease`**: Runs after the release process is complete.
- **`tagPrefix`**: Specifies a prefix for the Git tags created by `standard-version`.

By including these customizations, you can tailor `standard-version` to better fit your project's needs and ensure that your release process is both automated and consistent.