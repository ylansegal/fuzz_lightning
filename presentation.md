title: Fuzzy Match 'All The Things'
author:
  name: Ylan Segal
  twitter: ylansegal
  url: http://ylan.segal-family.com
  email: ylan@segal-family.com
controls: false
--

# Fuzzy Match 'All The Things'

## SDRuby - March, 2014

## Ylan Segal

--

# Changing Projects

--

# `fuzz`
## Finding Files

--

# Arguments
## Instead of Autocomplete

--

# How The Fuzz

- Selecta `brew install selecta`
- Percol `pip install percol`

--

# cdp

``` bash
cdp () {
	cd $(find ~/Development ~/Personal -maxdepth 1 -type d | percol)
}
```

--

# fuzz

``` bash
fuzz () {
	search_term=$1
	find . -wholename \*$search_term\* -not -path './.*/*' | percol
}
```

--

# zsh Binding

``` bash
# ^S for fuzzy matching
# By default, ^S freezes terminal output and ^Q resumes it. Disable that so
# that those keys can be used for other things.
unsetopt flowcontrol
# Run Selecta in the current working directory, appending the selected path, if
# any, to the current command.
function insert-fuzzy-path-in-command-line() {
    local selected_path
    # Print a newline or we'll clobber the old prompt.
    echo
    # Find the path; abort if the user doesn't select anything.
    selected_path=$(fuzz) || return
    # Append the selection to the current command buffer.
    eval 'LBUFFER="$LBUFFER$selected_path"'
    # Redraw the prompt since Selecta has drawn several new lines of text.
    zle reset-prompt
}
# Create the zle widget
zle -N insert-fuzzy-path-in-command-line
# Bind the key to the newly created widget
bindkey "^S" "insert-fuzzy-path-in-command-line"
```
