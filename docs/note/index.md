### MkDocs Features
```md
  features:
    - navigation.tabs
    - navigation.tabs.sticky   # keeps tabs visible when scrolling
    - navigation.indexes       # lets a folder's index.md serve as its landing page
    # - navigation.sections      # groups sidebar items into labeled sections
    - navigation.top           # adds a "back to top" button
```
`navigation.sections`

Without `navigation.sections` → nested groups are collapsible/expandable, arrow-based (what we want)

With `navigation.sections` → nested groups become permanently-expanded static headers, useful for docs where we always want everything visible at once (not what we want here)

