# Conventional Commits (new rule for Commitizen) Template

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## type

As it should already be specified by Conventional Commits itself.

## scope

As it should already be specified by Conventional Commits itself. With the emphasis at "_A scope MUST consist of a noun describing a **section of the codebase**_". Which Common Changelog refer it to as **`subsytem`**, that will be written on the changelog as it.

## description

> **\+ which file,** 
>
> from Common-Changelog, "_**Each change must be self-describing, as if no category heading exists.** ..._", therefore **\+ which commit type**
>
> `*kw <something> in <file> by adding/removing <subject>`

## body

## footer

```text
BREAKING-CHANGE: 
References: linked commit hash, linked issue, linked pullrequest
Commit-Author: commit author
```
