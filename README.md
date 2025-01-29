# git-branch-zsh-terminal-prompt with time

##  MacOS with zsh
Since macOS Catalina (10.15), released in October 2019, apple has been making the default shell as zsh rather than the previous bash shell. 

<img width="903" alt="Screenshot 2025-01-29 at 20 02 12" src="https://github.com/user-attachments/assets/7a4b680f-2d62-4650-8d3a-820216151cc8" />

### Setup
Open `~/.zshrc` in your favorite editor and add the following content to the bottom.


```sh
function parse_git_branch() {
git_branch() {
    branch=$(git symbolic-ref HEAD 2> /dev/null | awk -F/ '{print $NF}')
    if [ ! -z $branch ]; then
        echo " ($branch)"
    fi
}

export setopt PROMPT_SUBST
export PROMPT='%n@%m-%F{blue}%D{%H:%M:%S}%f %1~%F{green}$(git_branch)%f $ '
export PROMPT='${COLOR_USR}%n ${COLOR_DIR}%~ ${COLOR_GIT}$(parse_git_branch)${COLOR_DEF} $ '
```

Otherwise, you can use append the changes to the end of the `~/.zshrc` file with the single command 

```sh
echo -e " git_branch() {\n branch=$(git symbolic-ref HEAD 2> /dev/null | awk -F/ '{print $NF}')\nif [ ! -z $branch ]; then\necho " ($branch)"\nfi\n}\nexport setopt PROMPT_SUBST\nexport PROMPT='%n@%m-%F{blue}%D{%H:%M:%S}%f %1~%F{green}$(git_branch)%f $ ' \n export PROMPT='${COLOR_USR}%n ${COLOR_DIR}%~ ${COLOR_GIT}$(parse_git_branch)${COLOR_DEF} $ ' " >> ~/.zshrc
```

### Verifications

Open a new shell or on an existing shell, reload and apply formatting adjustments by running  `source ~/.zshrc` in the zsh shell.
