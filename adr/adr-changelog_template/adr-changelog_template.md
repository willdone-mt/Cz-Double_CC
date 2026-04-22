# Decisions for the Current Template Design

[WIP]

> Numbering the rules
>
> Note some new C-Commit Convention
>
> Other adr files are numbered by the rules. this adr files are only for the approved one

**Common-Changelog's Principle**

> 1.2. Guiding principles
>
> - Changelogs are for humans.
> - Communicate the impact of changes.
> - Sort content by importance.
> - Skip content that isn't important.
> - Link each change to further information.

## Format

---

> ### [2.1. File format](https://common-changelog.org/#21-file-format)
>
> [1] Filename must be `CHANGELOG.md`. [2] File content must be Markdown and [3] start with a first-level heading.
>
> ...

[Answering 1 and 2] Using Cz, filename MUST manually configured trough Cz's Configuration File, and [Answering 3] the first-level heading is also manually typed. Version entries are somehow skip first line of the document to overwrite

```Jinja
            {# <--- no `# Changelog` here #}
{% for entry in tree -%}
{# --- Definitions: build groups first --- #}
...
...
```

---

> ### [2.2. Release](https://common-changelog.org/#22-release)
>
> ...
>
> Where [4] VERSION is a semver-valid version (without "v" prefix) matching a git tag (with optional "v" prefix). If the version is new then the changelog entry should be committed before creating the git tag. [5] The DATE must be in the form of YYYY-MM-DD (ISO 8601).
>
> ...

The original Cz' changelog template showing its `v` prefix. Changing the field to entry.tag also showing its prefix because it auto reads from the git tag. [Answering 4] This problem should be fixed by replace the `v` with blank via `...|replace("v","")`. [Answering 5] Meanwhile the `entry,date` field is already output as YYYY-MM-DD.

```Jinja
...
{# --- Output starts here --- #}

## {{ entry.version|replace("v", "") }} - {{ entry.date }}
{##}
...
```

---

> ...
> 
> [6] The version should link to further information. [6.1] If the project is hosted on GitHub, link the version to a GitHub release that should contain the same content as the changelog entry, alongside useful GitHub features like assets and the compare view. [6.2]Preferably use reference-style links to keep the unrendered Markdown form of the changelog readable.
>
> ...

(_**UNIMPLEMENTED**_)

[_(1) New rule for `cz` commands_]

---

> After the heading, [7] a release must have Markdown content that is either:
>
> 1. One or more change groups;
> 2. A notice followed by zero or more change groups.

[Answering 7] All category/changes are only available if there are changes in corresponding category.

```Jinja
{% if changed %}

### 🔄 Changed

...

{% endif %}
```

---

> ### 2.3. Notice
>
> ...
>
> For these purposes [8] a notice must be used. This is a single-sentence paragraph with otherwise arbitrary Markdown content. Adding Markdown emphasis markers is recommended.
>
> ...

(_**UNIMPLEMENTED**_)

[_(2) New rule for `cz` commands_]

---

> ### 2.4. Change group
>
> [9] A change group must start with a third-level, text-only Markdown heading containing a category:
>
> ...
>
> [10] The category must be one of (in order):
>
> - `Changed` for changes in existing functionality
> - `Added` for new functionality
> - `Removed` for removed functionality
> - `Fixed` for bug fixes.
>
> ...

[Answering 9 and 10] This already being implemented in order.

```Jinja
{% if changed %}

### 🔄 Changed

...

{% endif %}
{##}
{% if added %}

### 🆕 Added

...

{% endif %}
{##}
{% if removed %}

### 🗑️ Removed

...

{% endif %}
{##}
{% if fixed %}

### 🐛 Fixed

...

{% endif %}
```

---

> ...
> 
> The category must be one of (in order):
> [11]
>
> - [11.a]`Changed` for changes in existing functionality
> - [11.b]`Added` for new functionality
> - [11.c]`Removed` for removed functionality
> - [11.d]`Fixed` for bug fixes.
>
> [11.1] **The word _functionality_ here can also mean documentation, supported runtime environments and so forth**. The categories exist to easily recognize the impact of changes and to allow skimming a changelog. 
> Changes that are listed under `Removed` will typically be breaking, while anything under `Added` is potentially interesting to the reader but carries no risk when upgrading.
>
> ...

Looking up into the bolded sentence, the word `so forth` can be widely and generally intepreted. I will ask this later to the author for the specific. But for now i will intepret this by my opinion.

[Answering 11.1] (_based on my opinion_) the word _functionality_ includes:

- Documents, Assets, and Data
- Supported Environments and Infrastructure
- Configuration & Build Artifacts
- Interfaces & User-Facing Elements
- Dependencies, Utilities, & Tooling
- Performance, Testing, and Monitoring
- Security & Compliance

Therefore, most of the C-Commits's commit can be grouped into C-Changelog categories mainly based on their type, scope, and their starting verb (which C-Commit use as imperative mood). This section will not explain about grouping via scope, since scope is not obligated by C-Commit

[Answering 11.a] Commits that grouped into C-Changelog's `Changed`:

(_**#! needs to reconsidered**_)

- commit type: `perf` and `refactor`
  except commit with description that starts with verbs: `fix`
- commit type: `revert`
- every commit with description that starts with verbs: `move`, `rename`, `deprecate`, `change`, `refactor`, `optimise`, `tweak`
  except from commit type `style` and `chore`
- NO COMMIT TYPE `feat` and `fix`

[Answering 11.b] Commits that grouped into `Added`:

(_**#! needs to reconsidered**_)

- commit type: `feat`
- every commit with description that starts with verbs: `start`, `introduce`, `implement`  
  except from type `perf`, `refactor`, `fix`

[Answering 11.c] Commits that grouped into `removed`:

(_**#! needs to reconsidered**_)

- every commit with description that starts with verbs: `remove`, `stop`, `discard`

[Answering 11.d] Commits that grouped into `Fixed`:

(_**#! needs to reconsidered**_)

- commit type `fix`
- every commit with description that starts with verbs: `fix`, `repair`, `stabilize`, `patch`
  except from type `docs`, `style` and `chore`

**NOTICE**: some commits are not and never included in some categories

- commit type: `style` and `chore` only appear in `Added` and `Removed` category, and never appear in `Changed` and `Fixed`

---

> ... 
>
> [12] The heading must be followed by (and only by) an unnumbered Markdown list. 
> [13] Each item in the list should be a single line that [13.1] must start with a [change](#241-change), [13.2] followed by one or more [references](#242-references) and [13.3] then zero or more [authors](#243-authors).
>
> ...

[Answering 12] This already implemented by using the if statement after a dash.

```Jinja
{% if changed %}

### 🔄 Changed

{% for change in changed -%}
- {% if change.footer and "breaking" in change.footer|lower -%}
```

[Answering 13] Only point `13.1` are supportly implemented. 

(_**There will be a Cz commit field which store reference and author from the commit.
This field will be extracted from the footer with the word token `REFERENCES:` and `COMMIT-AUTHORS:`, in planned**_)

[_(1) New rule for Conventional Commits_]

---

> [14] The list should be sorted: breaking changes first, then by other importance, then latest-first. [14.a] The importance of a change is left to the writer's discretion.

[Answering 14] The template list managed to sort the breaking change first. And by other importance, which Common Changelog left it to the writer's discretion, are then sorted by its scope (_**UNIMPLEMENTED, scope/subsytem still alphabetically sorted**_). Then latest first, which will be some scopeless change. (_**UNIMPLEMENTED, scopeless change appear last, but still not sorted chronologically**_)

_[?SIRENIA ONLY?: importance will sort from 1. commit type feat, fix, perf, refactor, then 2.commits with scope that touches src/ first, then outside of it.]_

---

> #### 2.4.1. [15] Change
>
> [15.1] Write a change using the [imperative mood](https://en.wikipedia.org/wiki/Imperative_mood). 
> [15.2] It must start with a present-tense verb, for example (but not limited to) `Add`, `Refactor`, `Bump`, `Document`, `Fix`, `Deprecate`.
>
> ...
> 
> **Each change must be self-describing, as if no category heading exists.** ...

[Answering 15] This already fullfilled by Conventional Commit itself. With the emphasis at the last line

[_(2) New rule for Conventional Commits_]

---

> #### 2.4.2. [16] References
>
> ...
>
> For these reasons, [16.a] changes must reference relevant commits, and should reference tickets or pull requests when available. ...
