# Aliases
alias hx="helix"
alias hxconf="helix ~/.config/helix/"
alias hxtmp="helix /tmp/helix/"
alias cp="cp -i"                                                # Confirm before overwriting something

# Add PATH
export PATH="$PATH:~/.cargo/bin"       # Rust cargo bin
export PATH="$PATH:/usr/local/bin"

# Use helix editor
export EDITOR="helix"
export VISUAL="helix"

# Fzf inits
export FZF_DEFAULT_OPTS="
--info=inline
--height=80%
--multi
--preview-window=:hidden
--preview '([[ -f {} ]] && (bat --style=numbers --color=always {} || cat {})) || ([[ -d {} ]] && (tree -C {} | less)) || echo {} 2> /dev/null | head -200'
--color='hl:148,hl+:154,pointer:032,marker:010,bg+:237,gutter:008'
--prompt='∼ ' --pointer='▶' --marker='✓'
--bind '?:toggle-preview'
--bind 'ctrl-a:select-all'
--bind 'ctrl-y:execute-silent(echo {+} | pbcopy)'
--bind 'ctrl-e:execute(echo {+} | xargs -o vim)'
--bind 'ctrl-v:execute(code {+})'
"

# Overwrite ls with exa
unalias ls 2>/dev/null
ls() {
  if command -v exa &> /dev/null; then
    DEFAULT_EXA_ARGS="-F --icons --group-directories-first"
    exa -F --icons --group-directories-first $@;
  else
    echo "exa required but not installed. Please install exa (replacement for ls)";
  fi
}

# Overwrite cat with bat
unalias cat 2>/dev/null
cat() {
  if command -v bat &> /dev/null; then
    bat $@;
  else
    echo "bat required but not installed. Please install bat (replacement for cat)";
  fi
}

# Custom cdh to workspace directory, else home
unalias cdh 2>/dev/null
cdh() {
  if [[ -n $ZSH_INIT_CDH_ALIAS ]]; then
    cd "${ZSH_INIT_CDH_ALIAS//[\'\"]*}";
  elif [ "$(git rev-parse --is-inside-work-tree 2>/dev/null)" = "true" ]; then
    cd "$(git rev-parse --show-toplevel)";
  else
    cd;
  fi
}

# Simultaneous cd and ls
unalias cdls 2>/dev/null
cdls() {cd $1; ls};

## Options
# setopt correct                                                  # Auto correct mistakes
setopt extendedglob                                             # Extended globbing. Allows using regular expressions with *
setopt nocaseglob                                               # Case insensitive globbing
setopt rcexpandparam                                            # Array expension with parameters
setopt nocheckjobs                                              # Don't warn about running processes when exiting
setopt numericglobsort                                          # Sort filenames numerically when it makes sense
setopt nobeep                                                   # No beep
setopt appendhistory                                            # Immediately append history instead of overwriting
setopt histignorealldups                                        # If a new command is a duplicate, remove the older one
# setopt autocd                                                   # if only directory path is entered, cd there.
setopt inc_append_history                                       # save commands are added to the history immediately, otherwise only when shell exits.
setopt histignorespace                                          # Don't save commands that start with space

# Completions
zstyle ':completion:*' matcher-list 'm:{[:lower:][:upper:]}={[:upper:][:lower:]}' # Case insensitive tab completion
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"         # Colored completion (different colors for dirs/files/etc)
zstyle ':completion:*' rehash true                              # automatically find new executables in path 
# Speed up completions
zstyle ':completion:*' accept-exact '*(N)'
zstyle ':completion:*' use-cache on
zstyle ':completion:*' cache-path ~/.zsh/cache
HISTFILE=~/.zhistory
HISTSIZE=10000
SAVEHIST=10000

## Keybinds
bindkey -v
# Navigate words with ctrl+arrow keys
bindkey '^[Oc' forward-word                                     #
bindkey '^[Od' backward-word                                    #
bindkey '^[[1;5D' backward-word                                 #
bindkey '^[[1;5C' forward-word                                  #
bindkey '^H' backward-kill-word                                 # delete previous word with ctrl+backspace
bindkey '^[[Z' undo                                             # Shift+tab undo last action

# Color man pages
export LESS_TERMCAP_mb=$'\E[01;32m'
export LESS_TERMCAP_md=$'\E[01;32m'
export LESS_TERMCAP_me=$'\E[0m'
export LESS_TERMCAP_se=$'\E[0m'
export LESS_TERMCAP_so=$'\E[01;47;34m'
export LESS_TERMCAP_ue=$'\E[0m'
export LESS_TERMCAP_us=$'\E[01;36m'
export LESS=-R

## Plugins section: Enable fish style features
# Use syntax highlighting
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
# Use history substring search
source /usr/share/zsh/plugins/zsh-history-substring-search/zsh-history-substring-search.zsh
# bind UP and DOWN arrow keys to history substring search
zmodload zsh/terminfo
bindkey "$terminfo[kcuu1]" history-substring-search-up
bindkey "$terminfo[kcud1]" history-substring-search-down
bindkey '^[[A' history-substring-search-up			
bindkey '^[[B' history-substring-search-down

# File and Dir colors for ls and other outputs
eval "$(dircolors -b)"
