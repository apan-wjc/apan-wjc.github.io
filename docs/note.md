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

