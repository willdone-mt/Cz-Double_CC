# Decisions for the Current Template Design

[WIP]

## Common-Changelog's Principle

> 1.2. Guiding principles
>
> - Changelogs are for humans.
> - Communicate the impact of changes.
> - Sort content by importance.
> - Skip content that isn't important.
> - Link each change to further information.

## Decisions

### Format

---

> #### [2.1. File format](https://common-changelog.org/#21-file-format)
>
> [1] Filename must be `CHANGELOG.md`. [2] File content must be Markdown and [3] start with a first-level heading.

[Answering 1 and 2] Using Cz, filename MUST manually configured trough Cz's Configuration File, and the first-level heading is also manually typed.

```Jinja
            {# <--- no `# Changelog` here #}
{% for entry in tree -%}
{# --- Definitions: build groups first --- #}
...
...
```

---

> #### [2.2. Release](https://common-changelog.org/#22-release)
>
> ...
>
> Where [4] VERSION is a semver-valid version (without "v" prefix) matching a git tag (with optional "v" prefix). If the version is new then the changelog entry should be committed before creating the git tag. [5] The DATE must be in the form of YYYY-MM-DD (ISO 8601).

The original Cz' changelog template showing its `v` prefix. Changing the field to entry.tag also showing its prefix because it auto reads from the git tag.

```Jinja
...
{# --- Output starts here --- #}

## {{ entry.version|replace("v", "") }} - {{ entry.date }}
{##}
...
```

---

> [5] The version should link to further information. [5.1] If the project is hosted on GitHub, link the version to a GitHub release that should contain the same content as the changelog entry, alongside useful GitHub features like assets and the compare view. [5.2]Preferably use reference-style links to keep the unrendered Markdown form of the changelog readable.

_Not yet implemented_

---

> After the heading, [6] a release must have Markdown content that is either:
>
> 1. One or more change groups;
> 2. A notice followed by zero or more change groups.

_Will be explained in upcoming_

---

> 2.3. Notice
>
> ...
>
> For these purposes [7] a notice must be used. This is a single-sentence paragraph with otherwise arbitrary Markdown content. Adding Markdown emphasis markers is recommended.

_Not yet implemented_

---

> 2.4. Change group
>
> [8] A change group must start with a third-level, text-only Markdown heading containing a category:
>
> ...
>
> [9] The category must be one of (in order):
>
> - `Changed` for changes in existing functionality
> - `Added` for new functionality
> - `Removed` for removed functionality
> - `Fixed` for bug fixes.

[Answering 8 and 9] This already being implemented in order. 

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

**However**, the current template contains additional category `Misc`. which holds Conventional-Commits's change types `Build`, `Ci`, and `Test`.
This are done **because** [WIP].

```Jinja
{##}
{% if misc %}

### 🔧 Misc

{% for type, changes in entry.changes.items() -%}
  {% if type in ["Build","Ci","Test"] -%}

  #### {{ type }} 
```

