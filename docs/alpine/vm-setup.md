# VM Setup

The "normal" workflow to set an Alpine VM up from scratch  

### dowload ISO
[alpine-standard-X.XX.X-x86_64](https://alpinelinux.org/downloads/ "Download ISO")

### setup VM
Use the ISO to set up the VM in "Oracle VM VirtualBox" with reasonable resource settins.  
`Network`  
`Adapter 1` - NAT  
`Adapter 2` - Host-only Adapter  
`Adapter 3` - Bridged Adapter  
Bring the box up.

1. console log in as root, no password.
1. `setup-alpine`, answer ALL questions.
1. `reboot`, meanwhile remove ISO disk.
1. get IP from the console login, `ip a`, ssh to it.
1. `su -` to root, copy this to ` /root/.profile`

        # 99+
        export PS1="\[\e[31m\][\[\e[m\]\[\e[38;5;172m\]\u\[\e[m\]@\[\e[38;5;153m\]\h\[\e[m\] \[\e[38;5;214m\]\w\[\e[m\]\[\e[31m\]]\[\e[m\]\\$ "
        alias rm='rm -fv' ll='ls -al ' gg='grep --color ' hh='history 33' nn='nano -w ' ff='free -m' ww='ps aux|grep -v grep|grep "pts/"' uu='uptime'
        export LS_COLORS=${LS_COLORS}:'zz=04;31'   # ONLY works for ls --color, not for busybox ls.
        export EDITOR=nano
        #eval "$(direnv hook bash)"
        # 99+.

1. `source /root/.profile` to make the profile effective without re-login.
1. `apk update`
1. install these needed.

        apk add curl nano nano-syntax rsync nginx samba tree file bc iproute2

1. configure nano syntax highlight

        nano -w ~/.nanorc
        include /usr/share/nano/*.nanorc

1. enable bash shell, Alpine default shell is Busybox.

        apk add bash
        # you can EASILY switch busybox/ash shell to bash shell by modify the /bin/sh link
        ll /bin/sh
        /bin/sh -> /bin/busybox
        rm /bin/sh
        ln -s /bin/bash /bin/sh
        ll /bin/sh
        /bin/sh -> /bin/bash
        # relog in, and you will see .bash_history is replaced .ash_history

### add ssh id
`cd;mkdir .ssh;cd $_ && nn authorized_keys`
```bash
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDKA+yUNpBGeIJzYKsS3BTjs6M4RIc9bDk2D1Z2lOhmWKciEMf6gi8LQmBIjB6Bf5J9m3Fg1uJE/oNt2MTYjKP4asRcKud1rEkNFf87CsJMX2faTLE3Tnfz/Q8lDGQPkZ2eE5CuAbjP3aUcbPx7tanMh+qe5oTXnL6dmqtcl8jMgCrr8wH6RTLR+KO5yGSuDRAOx7RM4Vz1IbrLUCxicGkDn+dmjbdMOl0HUZbtg4iuGAEsdB94JxTrD+z7IN+95j5FuWfP7ykcKfZQIPC1R7ktwTLI+yRwpOkQAHeqRI1va+AWqz3y645sOfxI+UcH/TwF7cw4dr/octtyN4ISI4F5 root@s08
```
`nn id_rsa`
```bash
THE PRIVATE KEY
```
`chmod 0600 id_rsa`

### configure network
`mv /etc/network/interfaces /etc/network/interfaces.000`
`nn /etc/network/interfaces`
```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
        address 192.168.56.39
        netmask 255.255.255.0

auto eth2
iface eth2 inet static
        address 192.168.100.39
        netmask 255.255.255.0
        gateway 192.168.100.1

# for WiFi interface
#auto eth3
#iface eth3 inet static
#        address 192.168.100.XXX
#        netmask 255.255.255.0
#        gateway 192.168.100.1
```
```bash
# ip a|gg 'inet '
    inet 127.0.0.1/8 scope host lo
    inet 10.0.2.15/24 scope global eth0
    inet 192.168.56.111/24 scope global eth1
    inet 192.168.100.79/24 brd 192.168.100.255 scope global eth2
```
`/etc/init.d/networking restart`
```bash
# ip a|gg 'inet '
    inet 127.0.0.1/8 scope host lo
    inet 10.0.2.15/24 scope global eth0
    inet 192.168.56.39/24 scope global eth1
    inet 192.168.100.39/24 scope global eth2
```
### add direnv binary
```bash
curl -sfL https://direnv.net/install.sh | bash
or
bash /opt/pkg install.sh

nn ~/.profile to uncomment thie line:
#eval "$(direnv hook bash)"

source ~/.profile
```

### configure samba
```bash
cd /etc/samba/;mv smb.conf smb.conf.000
nn smb.conf

# run the following command to add user root with password
# otherwise, no way to connect
# smbpasswd -a root

[s26-39]
    comment = s26-39
    path = /
    #valid users = someusers, somegroup
    force user = root
    force group = root
    #admin users = someusers, somegroup
    writeable = Yes

smbpasswd -a root
New SMB password:
Retype new SMB password:
Added user root.

rc-update add samba
service samba start
```
Test it on Windows box to go `\\192.168.56.39`

### configure nginx
```bash
cd /etc/nginx/http.d;mv default.conf default.conf.000 && nn default.conf

server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;
        autoindex on;
        autoindex_exact_size off;
        autoindex_localtime on;
        charset utf-8;

        index index.html index.htm;

        server_name _;

        # Everything is a 404
        #location / {
        #       return 404;
        #}
        # You may need this to prevent return 404 recursion.
        location = /404.html {
                internal;
        }
}

mkdir -p /var/www/html
rc-update add nginx
service nginx start
```
Test it to go `http://192.168.56.39`

### copy favicon
`rsync -azv 192.168.56.25:/var/www/html/fav* /var/www/html/`  
Pick the favicon by `cp favs/favicon_9.ico favicon.ico`
