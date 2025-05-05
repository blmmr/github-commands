# Cheatsheet of GitHub commands

## How to set up the second GitHub account

~~~zsh
ssh-keygen -t ed25519 -C "emailconnectedtogithub@gmai.com"
# generates ssh for the second account
# -c adds a comment (could be any), but the convention is using an email
# should be saved as /Users/yourname/.ssh/id_ed25519_second

eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519_second
# starts the ssh key manager in the background 
# registers the new key with the agent so that it can be used automatically

pbcopy < ~/.ssh/id_ed25519_second.pub
# copies the public key to the clipboard

# On GitHub:
# settings -> SSH and GPG keys -> new SSH key -> (name it) -> (paste the key)
# links the public SSH key with the account

vim ~/.ssh/config
# ssh config

# Default GitHub account
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Second GitHub account
Host github-second
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_second
~~~

### To clone repo from the second account
~~~zsh
git clone git@github-second:your-username/your-repo.git

git config user.name "Second Username"
git config user.email "you@example.com"
# to be set from within the repo

git config user.name
git config user.email
# to check what identity is connected to the repo
~~~

## Shortcuts
~~~zsh
vim ~/.zshrc

alias ga="git add ."
alias gc="git commit -m "
alias gp="git push"
alias gst="git status"

wq

source ~/.zshrc
~~~