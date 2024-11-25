---
layout: post
title: Supercharge Your Bash History with fuzzy matching and Shared History
date: 2024-11-10 00:32:13
description:  Unlock the full potential of your terminal by supercharging your Bash history and integrating the powerful fzf fuzzy finder.
tags:  terminal fuzzy bash
categories:  Command-Line
tabs: true
---



*Boost productivity by expanding your command history and adding the power of `fzf` fuzzy search to your terminal.*

## Why Optimize Your Bash History?

The default Bash history is limited, doesn’t sync between sessions, and lacks timestamps. Enhancing it means:

- **Quicker Commands**: Recall past commands faster.
- **Shared Sessions**: Seamless history across all terminals.
- **More Info**: Know when commands were used with timestamps.

## Step 1: Set Up Enhanced Bash History

Let’s expand your history and make it smarter.
In terminal, open your `~/.bashrc` file:

```bash
nano ~/.bashrc
```
add the following lines to your `~/.bashrc` file:

```bash
# 1 Remove Duplicate Entries
export HISTCONTROL=ignoredups:erasedups
#2 Increase History Size and store more commands for quick recall:
export HISTSIZE=1000000  # Increase in-memory history
export HISTFILESIZE=1000000  # Increase saved history
#3 Add Timestamps to track when commands were executed:
export HISTTIMEFORMAT="%F %T: "  # YYYY-MM-DD HH:MM:SS
# 4 Sync History Across Sessions and automatically update and share history across all open terminals:
export PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
```
Now, save and close the file. Source your `~/.bashrc` to apply the changes:

```bash
source ~/.bashrc
```

## Step 2: Add Fuzzy Search with fzf

`fzf` brings fuzzy searching to your command history, making it easy to find commands even if you only remember parts of them.

>### What is Fuzzy Search?
>Fuzzy searching (or “fuzzy matching”) is a technique that allows you to search even when you only partially remember what you're looking for. It’s not an exact match search; instead, it finds the closest match based on your input and ranks the results by how well they match.
>Fuzzy matching takes the characters you type and tries to find any results containing those characters in order, but they don’t need to be consecutive. Here’s how it works under the hood:
>1. **Partial Matching**:
>   - Let’s say you type "gr com" when searching for the command `git commit`. The fuzzy search algorithm will still find `git commit` because it recognizes that "g", "r", "c", "o", "m" appear in the command in that order.
>2. **Ranking Matches**:
>   - Fuzzy search algorithms assign scores to matches. Commands that match all your typed characters in sequence with fewer gaps or extra characters get a higher score and appear higher in the list.
> 3. **Flexibility with Typos**:
>   - Fuzzy search tolerates slight mismatches, so you can find the right command even if you don’t type it perfectly.
> 4. **Speed and Efficiency**:
>  - Fuzzy search is fast and efficient, making it a powerful tool for finding commands in your history.



### 2.1 Install fzf

On Ubuntu/Debian:

```bash
sudo apt-get update
sudo apt-get install fzf
```

### 2.2 Enable fzf Key Bindings

Add to your `~/.bashrc`:

```bash
if [ -f /usr/share/doc/fzf/examples/key-bindings.bash ]; then
    source /usr/share/doc/fzf/examples/key-bindings.bash
fi
```

Reload your configuration:

```bash
source ~/.bashrc
```

### 2.3 Use fzf to Search History

Now, press `Ctrl + R` to open `fzf` for an interactive history search. Type any part of a command, and `fzf` will find it, even if the words aren’t in the correct order.


### Resources

- [Bash History](https://www.gnu.org/software/bash/manual/html_node/Bash-History-Builtins.html)
- [fzf GitHub](https://github.com/junegunn/fzf)