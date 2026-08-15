### using termynal
```bash
pip install termynal
```
Then add this `<!-- termynal -->` before ANY  
<!-- termynal -->
```bash
$ ls -al
```
### using Github workflow
Instead of using local environment to run `mkdocs gh-deploy --force`  
to deploy Mkdocs site at Github, one can do the following:
<!-- termynal -->
```
$ cd /opt/apan-wjc.github.io
$ source venv/bin/activate
$ pip freeze > requirements.txt
```
And adding this file:  
`.github/workflows/deploy.yml`
```yaml
name: Deploy MkDocs site

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0   # full history, needed for git-revision-date plugin

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Configure Git user
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"

      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force
```
### add page live render
Add plugin `pip install mkdocs-macros-plugin`
```yaml
plugins:
  - search:
      lang:
        - en
        - zh
  ... ...
  - macros:   # pip install mkdocs-macros-plugin, to make md file live replacement working
      include_yaml:
        - cc: docs/dushu/ChineseCultrure.yml   # specify the data file, yaml
```
Sample data yaml file:
```yaml
tian_gan:
  tg_title: "天干 (Ten Heavenly Stems)"
  tg_message: "天干通常用拼音表示，因为它们本身是中文字符，翻译成英文单词没有实际意义。"
  tg_items:
    - "甲 - Jia"
    - "乙 - Yi"
    - "丙 - Bing"
    - "丁 - Ding"
    - "戊 - Wu"
    - "己 - Ji"
    - "庚 - Geng"
    - "辛 - Xin"
    - "壬 - Ren"
    - "癸 - Gui"
```
Smaple live page md file:
```md
{% if cc.tian_gan %}
  <h3>{{ cc.tian_gan.tg_title }}</h3>
  <p>{{ cc.tian_gan.tg_message }}</p>
  <ol>
    {% for tg_item in cc.tian_gan.tg_items %}
      <li>{{ tg_item }}</li>
    {% endfor %}
  </ol>
{% endif %}
```
### from scratch
```bash
nn /root/.ssh/config

ssh -T git@github-apan-wjc   # test
Hi apan-wjc! You've successfully authenticated, but GitHub does not provide shell access.

git clone git@github.com:apan-wjc/apan-wjc.github.io.git
cd apan-wjc.github.io.git

apk add git python3 py3-pip py3-virtualenv build-base libffi-dev

virtualenv venv
source venv/bin/activate

pip install --upgrade pip
pip install mkdocs mkdocs-material mkdocs-git-revision-date-localized-plugin tzdata

mkdocs serve -a 192.168.56.39:8000   # live local MkDocs site

mkdocs build   # will update site directory
ln -s /opt/apan-wjc.github.io/site /var/www/html/Local-MkDocs-Site   # then this site can be seen under Nginx server, port 80

mkdocs gh-deploy   # --force   # will update and deploy the gh-deploy branch at GitHub.
```
### customize md file font
add the following into ANY md file  
```html
<style>
.small-font {
  font-size: 0.7em;
}
</style>

<div class="small-font">

This text should look noticeably smaller than your other pages.

</div>
```
### add timestamp
Install these pacages:
```bash
pip install mkdocs-git-revision-date-localized-plugin
pip install tzdata
```
Then add the following into `mkdocs.yml`
```yaml
plugins:
  - search:
      lang:
        - en
        - zh
  - git-revision-date-localized:
      # type: timeago       # e.g. "3 days ago"
      # type: date          # e.g. "August 4, 2026"
      type: datetime        # e.g. "August 4, 2026 14:30"
      timezone: America/Vancouver
      locale: en
      fallback_to_build_date: true   # avoids errors on files not yet committed to git
```
it's not a single global timestamp, each page shows that specific file's last Git commit date.

### add picture
The following HTML code can be added in md file directly to show a picture
```html
<p align="center">
  <img src="assets/2010-08-15_REO.rafting.by.REO.31.jpg" alt="Rafting" width="800">
</p>
```

### MkDocs features
```md
  features:
    - navigation.tabs
    - navigation.tabs.sticky   # keeps tabs visible when scrolling
    - navigation.indexes       # lets a folder's index.md serve as its landing page
    # - navigation.sections      # groups sidebar items into labeled sections
    - navigation.top           # adds a "back to top" button
```
`navigation.sections`

*Without `navigation.sections` → nested groups are collapsible/expandable, arrow-based (what we want)*{: .small-text}

*With `navigation.sections` → nested groups become permanently-expanded static headers, useful for docs where we always want everything visible at once (not what we want here)*{: .small-text}

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
