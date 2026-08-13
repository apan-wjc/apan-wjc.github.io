# Front Matter

## Rule of Thumb

Whenever you're unsure where to put something, ask:

> **Is this page content, or is this site configuration?**

### Page Content
→ Goes in the Markdown file (`docs/*.md`)

Examples:

```yaml
---
title: AWS Notes
description: My AWS learning notes
hide:
  - toc
---
```

```markdown
# AWS Notes

This page contains AWS-related documentation.
```

### Site Configuration
→ Goes in `mkdocs.yml`

Examples:

```yaml
site_name: Alex Pan

nav:
  - Home: index.md
  - Teaching: teaching.md
  - Projects: projects.md

theme:
  name: material

plugins:
  - search
```

---

## Common Front Matter Fields
### Title

Override page title.

```yaml
---
title: Teaching
---
```

---

### Description

Used for SEO and social sharing metadata.

```yaml
---
title: Teaching
description: Courses, workshops and learning materials
---
```

---

### Hide Table of Contents

```yaml
---
hide:
  - toc
---
```

---

### Hide Navigation

```yaml
---
hide:
  - navigation
---
```

---

### Hide Footer

```yaml
---
hide:
  - footer
---
```

---

### Hide Multiple Elements

```yaml
---
hide:
  - toc
  - navigation
  - footer
---
```

---

### Custom Template

Used by some Material pages.

```yaml
---
template: home.html
---
```

---

## Blog Plugin Fields

### Date

```yaml
---
date: 2026-08-13
---
```

---

### Authors

```yaml
---
authors:
  - Alex Pan
---
```

---

### Categories

```yaml
---
categories:
  - AWS
  - Terraform
---
```

---

### Tags

```yaml
---
tags:
  - aws
  - kubernetes
  - terraform
---
```

---

### Draft

```yaml
---
draft: true
---
```

---

## What MkDocs Does NOT Use

The following are common in Jekyll but generally ignored by MkDocs:

```yaml
---
layout: page
permalink: /teaching/
nav: true
nav_order: 6
---
```

MkDocs equivalents:

| Jekyll | MkDocs |
|----------|----------|
| layout | theme/template |
| permalink | filename/path |
| nav | mkdocs.yml |
| nav_order | order in mkdocs.yml |
| _config.yml | mkdocs.yml |

---

## Example Teaching Page

```yaml
---
title: Teaching
description: Courses, workshops and technical learning materials
hide:
  - toc
---
```

```markdown
### Teaching

### AWS

AWS architecture and operations.

### Terraform

Infrastructure as Code examples.

### Kubernetes

EKS deployment and troubleshooting notes.
```

---

## Example Home Page

```yaml
---
title: Alex Pan
description: Cloud Infrastructure Engineer
hide:
  - navigation
  - toc
template: home.html
---
```

```markdown
### Welcome

Welcome to my personal knowledge base.

Topics include:

- AWS
- Azure
- Kubernetes
- Terraform
- GitHub Actions
```

---

## Golden Rule

> **Content belongs in Markdown files.**
>
> **Site behavior belongs in `mkdocs.yml`.**

If you're tempted to add something like:

```yaml
nav_order:
permalink:
layout:
```

it probably belongs in `mkdocs.yml` instead.
