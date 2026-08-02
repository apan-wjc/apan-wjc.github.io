### MkDocs
1. Using command `mkdocs gh-deploy` will deploy main to branch **gh-pages**, built-in command `mkdocs build`
2. CNAME in the main root should be copied to site/, in order to make customized domain work.
3. CNAME `wjc.ox0.ca` to `apan-wjc.github.io` should be set in DNS beforehand.

### SSH config for GitHub
1. Log in to Github.
1. Go [User/Settings](https://github.com/settings/keys "New SSH key")
1. Generate key pair with `ssh-keygen -t ed25519 -a 100 -C "your-email@example.com" -f /opt/key/apan-wjc`
1. Add public key at Github.
1. Add these to ~/.ssh/config

        Host github-apan-wjc
            HostName github.com
            User git
            IdentityFile /opt/key/apan-wjc
            IdentitiesOnly yes

1. Add these to file `.envrc` in the root directory of the repo

        #!/bin/bash
        
        git config user.email "your-email@example.com"
        git config user.name "alex-wjc"
        
        git remote set-url origin git@github-apan-wjc:apan-wjc/apan-wjc.github.io.git

1. Run `source .envrc` whenever you enter this place, or use `direnv` do so automatically.
1. Test it to verify the result

        ssh -T git@github-apan-wjc
        Hi apan-wjc! You've successfully authenticated, but GitHub does not provide shell access.

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

mkdocs build   # will build/renew local site

git add -A && git commit -a -m "XXXXXXXXX"
git push

mkdocs gh-deploy   # includes `mkdocs build` command, so no need to run it, BUT the deployment is at Github
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
