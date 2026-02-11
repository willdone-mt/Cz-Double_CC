# Cz-Double_CC

Implementing [Common-Changelog](https://common-changelog.org/) from [Conventional-Commits](https://www.conventionalcommits.org/en/v1.0.0/) via [Commitizen](https://commitizen-tools.github.io/commitizen/)

[![Common Changelog](https://common-changelog.org/badge.svg)](https://common-changelog.org) [![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org) 

## Goal

Since Conventional-Commits have their own specification, we cant do much to change its template.

Therefore, the main goal of this repository is to:
1. Change how Commitizen read Conventional-Commits
    - So Cz can extract the field to build Common-Changelog
2. Make new Cz changelog template based on Common-Changelog
3. Make new Conventional-Commit template that be used especially for Cz
4. Document the result for beginner programmers

## To Do List

### How Cz read Conventional Commits so commmits can be build automatically into Common-Changelog

### Common-Changelog rules which already be applied in the current template

- Format
  - [ ] File format
  - [x] Release 
  - [ ] Notice
  - [ ] Change group
    - [ ] Change _(brokenly applied)_
    - [ ] References
    - [ ] Authors
    - [ ] Prefixes _(brokenly applied)_
  - [ ] Markdown formatting
- Writing
  - [ ] Generate a draft
  - [ ] Remove noise _(brokenly applied)_
  - [ ] Rephrase changes
  - [ ] Merge related changes
  - [ ] Skip no-op changes
  - [ ] Separate commit message and description
  - [ ] Promoting a prerelease
- Antipatterns
  - [ ] Verbatim copying of content
  - [ ] Conventional Commits
  - [ ] Confusing dates

### New Conventional-Commit template
 
### Documentation to guide users

## HELP WANTED

Help and Contribution are very needed!

1. Fork this repository
2. Make Changes based on To Dos
3. Pull Request
