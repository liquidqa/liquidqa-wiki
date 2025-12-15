# Branching strategy
This page will explain the branching and merging for the project.

## Branches
The following four branches are used in the strategy:
- **develop**
- **feature**
- **bugfix**
- **release**


### Develop branch
The develop branch serves as an integration branch for features.

The branch is configured as:
- Requires pull request for code merging
- New code is merged as "**squash-merge**"
- For each pull request:
  - Automatic approvers are added
  - At least 2 approvers are needed
  - Build must pass successfully
  - All comments must be resolved

### Feature branch
Each user story should have a feature branch, configured as:
 - Should be named **feature/#123456-foo-bar**, where #xxxxxx is the corresponding WorkID

### Bugfix branch
Bugfixes are merged to the develop/release branch.

The pull requests are configured as:
  - Automatic approvers are added
  - At least 2 approvers are needed
  - Build must pass successfully
  - All comments must be resolved
  - Member of the test team must approve the fix as well


### TL;DR
- Features
  - Create a feature branch from develop
  - Merge into develop
- Releases
  - Create a release branch from develop
  - Tag each commit
- Bug fixes
  - Create a bugfix branch from develop
  - Merge into develop
  - Cherry-pick to the release branches if needed




