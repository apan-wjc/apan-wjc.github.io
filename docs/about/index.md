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
ssh 192.168.56.39   # s26-39
cd /opt/apan-wjc.github.io

source venv/bin/activate
mkdocs serve -a 192.168.56.39:8000   # bring up a live site, any change shows lively.

deactivate
```
