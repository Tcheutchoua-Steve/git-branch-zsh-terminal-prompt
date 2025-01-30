# git-branch-zsh-terminal-prompt with time

##  MacOS with zsh
Since macOS Catalina (10.15), released in October 2019, apple has been making the default shell as zsh rather than the previous bash shell. 

<img width="903" alt="Terminal Screen with name time and git branch" src="https://github.com/user-attachments/assets/11e7eaa5-29da-45ce-9b07-7c534e61c2b8" />

### Setup
Open `~/.zshrc` in your favorite editor and add the following content to the bottom.


```sh
git_branch() {
    branch=$(git symbolic-ref HEAD 2> /dev/null | awk -F/ '{print $NF}')
    if [ ! -z $branch ]; then
        echo " ($branch)"
    fi
}

export setopt PROMPT_SUBST
export PROMPT='%n@%m:%F{blue}%D{%H:%M:%S}%f %1~%F{green}$(git_branch)%f $ '
```

### Verifications

Open a new shell or on an existing shell, reload and apply formatting adjustments by running  `source ~/.zshrc` in the zsh shell.
