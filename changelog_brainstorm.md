```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

[optional footer(s)] = BREAKING CHANGE: if any

The category must be one of (in order):

Changed for changes in existing functionality
Added for new functionality
Removed for removed functionality
Fixed for bug fixes.
The word functionality here can also mean documentation, supported runtime environments and so forth.

### fields
```
<item> = <changes (description which starts with imperative mood)> (<issue|delimited by ,>;<commit author|delimited by ,>)

<list> = 
- **Breaking:** <commit message>
- **<scope> (breaking):** <commit message> 
- **<scope>:** <commit message>


```

```
## <version without v> - <YYYY-MM-DD>

_<notices>_

### Changed {# all changes with type `perf`, `refactor`, and changes with type `style` only if has specific keywords #}
<list>

### Added {# all changes with type `feat`, and all change types only if has specficic keywords, except that already been labeled with `Changed` `Removed`, and `Fixed` #}
<list>

### Removed (all description/imperative mood with remove and deprecate)
<list>

### Fixed (all change type `fix`)
<list>

### Misc (contains heading level 4 for `build`,`ci`, and `test`, except that already been labeled with `Changed` `Added` `Removed`, and `Fixed`)

#### <change type>
<list>
```