# yubikey conf

Configuration to use yubikey (5 NFC) to authenticate SSH connections and GPG signatures in Gentoo Linux with OpenRC (KDE) for Git.

# System config

Must enable `USE=security-key` in the `net-misc/openssh` package.  
Must install the package `dev-libs/pcsc-lite`.  
Must install the packages `dev-libs/openct` and `dev-libs/opensc` with the `USE=pcsc-lite` flag.  
Must install the package `app-crypt/yubikey-manager`.

Must enable `gpg-agent` in Plasma Workspace:
  Edit the file `/etc/xdg/plasma-workspace/env/10-agent-startup.sh` and uncomment `GPG_AGENT=true` and `SSH_AGENT=gpg`

Must set the following in `~/.gnupg/gpg-agent.conf` (with the quote marks):  
  `"pinentry-program /usr/bin/pinentry-qt"`
  `"enable-ssh-support"`  

# User config

Must import the ssh key by putting it into `~/.ssh/` and running `ssh-add`.  
Should test the connection with `ssh -vT git@github.com`.  
Must import private key with `gpg --import path/to/key`.  
Must change key's trust to ultimate (set as own key).  

# Git config

Must set `user.name` to the same in the GPG key.  
Must set `user.email` to the same in the GPG key.  
Must set `user.signingKey` to the last 16 characters of the GPG key (consult with `gpg --list-secret-keys`).
