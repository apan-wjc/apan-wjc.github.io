### Code
This site has code at:
[apan-wjc.github.io](https://github.com/apan-wjc/apan-wjc.github.io "Github Repo - apan-wjc.github.io")

### Site 1
The actual site is hosted by Github static page at:
[apan-wjc.github.io](https://apan-wjc.github.io "apan-wjc.github.io")

### Site 2
It has customized DNS name site at:
[wjc.ox0.ca](https://wjc.ox0.ca/ "wjc.ox0.ca")

### Site 0
The internal site is located at:
[Internal](http://192.168.56.25:8000 "Internal Live Site")

> s25-25:/opt/apan-wjc.github.io

The following command can bring it up:
```bash
ssh 192.168.56.25   # s25-25
cd /opt/apan-wjc.github.io

source venv/bin/activate
mkdocs serve -a 0.0.0.0:8000   # bring up a live site, any change shows lively.

deactivate
```
### Setup
```bash
cd /opt/apan-wjc.github.io
\rm -rf venv   # if venv already exists and need to redo

source venv/bin/activate
pip --version
pip install --upgrade pip
pip install mkdocs
pip install mkdocs-material
mkdocs --version
mkdocs new .   # ONLY for the first time
mkdocs serve -a 0.0.0.0:8000
```

### Publish
After all change looks good, the following command will launch a deployment and update the site
```bash
cd /opt/apan-wjc.github.io

git status
git diff

mkdocs build

git add -A && git commit -a -m "XXXXXXXXX"
git push

mkdocs gh-deploy
or
mkdocs gh-deploy --force
```

### Source
[MkDocs documentation](https://www.mkdocs.org "Official MkDocs site")

##### Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

##### Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
