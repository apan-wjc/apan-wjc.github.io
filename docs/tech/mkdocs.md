### collapsible admonition
( foldable tex box )

Add these to `mkdocs.yml`, root level:
```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```

`admonition` — *base support for callout boxes (note, warning, tip, etc.)*{: .small-text}

`pymdownx.details` — *makes those callout boxes collapsible (adds the > arrow and click-to-expand)*{: .small-text}

`pymdownx.superfences` — *needed if you ever nest code blocks inside admonitions (good to have alongside)*{: .small-text}

### usage
```md
??? info "Overview"
    Since ChatGPT was launched on November 30, 2022, AI has evolved at an incredible pace. More and more AI tools have become available, and today it almost feels unnecessary to maintain a tech website just to collect and organize technical information—the very reason I started this back in 2002.
```

### common admonition types
( each with its own icon/color )

| Type | Icon | Color |
|---|---|---|
| `note` | pencil | blue |
| `abstract` / `summary` | clipboard | light blue |
| `info` | info circle | blue |
| `tip` / `hint` | fire | teal |
| `success` / `check` / `done` | checkmark | green |
| `question` / `help` / `faq` | question mark | teal/green |
| `warning` / `caution` / `attention` | warning triangle | orange |
| `failure` / `fail` / `missing` | X | red |
| `danger` / `error` | lightning bolt | red |
| `bug` | bug | red |
| `example` | list | purple |
| `quote` / `cite` | quote marks | grey |

### customize font
Add these to `mkdocs.yml`, root level:
```yaml
extra_css:
  - stylesheets/extra.css
```
Make file stylesheets/extra.css looks like:
```css
.small-text {
  font-size: 0.8em;
  font-style: normal;
}
```
Use it in ANY text like this one:
```md
This is normal text, but *this part is smaller*{: .small-text} in size.
```
The line above is rendered like this now:

This is normal text, but *this part is smaller*{: .small-text} in size.
