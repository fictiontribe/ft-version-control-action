# Automated Changelog GitHub Action

This GitHub Action automatically updates a changelog file (`changelog.json`) based on commit messages. It follows semantic versioning principles and provides a structured way to track changes in your project.

## Table of Contents

- [Features](#features)
- [Setup](#setup)
- [Usage](#usage)
- [Commit Message Format](#commit-message-format)
- [Version Determination](#version-determination)
- [Changelog Structure](#changelog-structure)
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)

## Features

- Automatic changelog updates based on commit messages
- Semantic versioning support
- Customizable commit types for different change categories
- JSON-based changelog for easy parsing and integration
- Ignores its own commits to prevent infinite loops

## Setup

1. Create a `.github/workflows` directory in your repository if it doesn't already exist.
2. Create a new file named `update-changelog.yml` in the `.github/workflows` directory.
3. Copy the contents of the provided GitHub Action YAML into this file.
4. Commit and push these changes to your repository.

## Usage

Once set up, the action will run automatically on every push to the `main` branch (or whichever branch you specify in the YAML file). It will analyze the latest commit, update the `changelog.json` file in the `src` directory, and commit the changes.

## Commit Message Format

To make the most of this action, format your commit messages as follows:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Where `<type>` can be one of:

- `major`: Breaking changes
- `feat`: A new feature (minor version bump)
- `fix`: A bug fix (patch version bump)
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools and libraries

Example:
```
feat: add user authentication feature

This commit adds a new user authentication system using JWT tokens.

Closes #123
```

## Version Determination

The action determines the new version number based on the following logic:

1. It finds the latest version number in the existing changelog by:
   - Selecting all non-TBD versions
   - Sorting them numerically (considering all parts of the version number)
   - Selecting the highest version

2. It then increments this version based on the commit type:
   - `major`: Increments the major version (X.0.0)
   - `feat`: Increments the minor version (0.X.0)
   - `fix`: Increments the patch version (0.0.X)
   - All other types do not cause a version increment

For example, if the latest version is 1.2.3:
- A `major` commit would result in version 2.0.0
- A `feat` commit would result in version 1.3.0
- A `fix` commit would result in version 1.2.4

## Changelog Structure

The `changelog.json` file is structured as an array of objects, each representing a change:

```json
[
  {
    "version": "1.2.3",
    "commitHash": "abc123...",
    "author": "John Doe",
    "date": "2023-08-21T10:00:00Z",
    "message": "Add new feature",
    "type": "feat",
    "versionBump": "minor"
  },
  ...
]
```

New entries are added to the end of this array, maintaining a reverse chronological order (newest last).

---
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---
## Credits
- [@mishapetrov](https://github.com/kombuchapunk)
- [@connorburgess](https://github.com/connorburgess)

---
## License
```
MIT
```

---
## Fiction Tribe ®
<img alt="FictionTribe Logo" src="https://mishapetrov.github.io/Contrast.js/img/ft-logo.png" width="100">  
Created at <a style="color:#52337c;" href="https://fictiontribe.com">Fiction Tribe ®</a> in Portland, OR

---
