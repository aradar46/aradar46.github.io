---
layout: post
title: Supercharge Your Bash History with fuzzy matching and Shared History
date: 2024-11-10 00:32:13
description:  Unlock the full potential of your terminal by supercharging your Bash history and integrating the powerful fzf fuzzy finder.
tags:  terminal fuzzy bash
categories:  Command-Line
tabs: true
---

{% include figure.liquid loading="eager" path="assets/img/bashHistory.jpg" class="img-fluid rounded z-depth-1" %}


*Boost productivity by expanding your command history and adding the power of `fzf` fuzzy search to your terminal.*

## Why Optimize Your Bash History?

The default Bash history is limited, doesn’t sync between sessions, and lacks timestamps. Enhancing it means:

- **Quicker Commands**: Recall past commands faster.
- **Shared Sessions**: Seamless history across all terminals.
- **More Info**: Know when commands were used with timestamps.

## Step 1: Set Up Enhanced Bash History

Let’s expand your history and make it smarter.

### 1.1 Remove Duplicate Entries

Keep your history neat by avoiding duplicates:

```bash
export HISTCONTROL=ignoredups:erasedups
```

### 1.2 Increase History Size

Store more commands for quick recall:

```bash
export HISTSIZE=1000000  # Increase in-memory history
export HISTFILESIZE=1000000  # Increase saved history
```

### 1.3 Add Timestamps

Track when commands were executed:

```bash
export HISTTIMEFORMAT="%F %T: "  # YYYY-MM-DD HH:MM:SS
```

### 1.4 Sync History Across Sessions

Automatically update and share history across all open terminals:

```bash
export PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
```

#### **Add to `.bashrc`**

Place these commands in your `~/.bashrc` file to make the changes permanent, then run:

```bash
source ~/.bashrc
```

## Step 2: Add Fuzzy Search with fzf

`fzf` brings fuzzy searching to your command history, making it easy to find commands even if you only remember parts of them.

### What is Fuzzy Search?

Fuzzy search helps you find results even if you don’t type the exact command. For example, typing "git" and "commit" will find any command with those words in any order.

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


### What is Fuzzy searching ?
Fuzzy searching (or “fuzzy matching”) is a technique that allows you to search even when you only partially remember what you're looking for. It’s not an exact match search; instead, it finds the closest match based on your input and ranks the results by how well they match.


Fuzzy matching takes the characters you type and tries to find any results containing those characters in order, but they don’t need to be consecutive. Here’s how it works under the hood:

1. **Partial Matching**:
   - Let’s say you type "gr com" when searching for the command `git commit`. The fuzzy search algorithm will still find `git commit` because it recognizes that "g", "r", "c", "o", "m" appear in the command in that order.

2. **Ranking Matches**:
   - Fuzzy search algorithms assign scores to matches. Commands that match all your typed characters in sequence with fewer gaps or extra characters get a higher score and appear higher in the list.

3. **Flexibility with Typos**:
   - Fuzzy search tolerates slight mismatches, so you can find the right command even if you don’t type it perfectly.

### Using `fzf` with Fuzzy Matching
In `fzf`, when you press `Ctrl + r` to search your command history:
   - Start typing keywords or fragments of the command you remember. For example, typing "s r p" could match `ssh root@prod-server`.
   - `fzf` will list matching commands, with the closest matches appearing first.
   - Use the arrow keys to scroll through the list and press `Enter` to execute the selected command.

Fuzzy search is particularly helpful when you can’t recall an exact command but remember a few key parts!

## Conclusion

Optimizing your Bash history with `fzf` means you’ll never have to retype commands or struggle to remember them. Embrace faster, smarter command-line navigation!



### Resources

- [Bash History](https://www.gnu.org/software/bash/manual/html_node/Bash-History-Builtins.html)
- [fzf GitHub](https://github.com/junegunn/fzf)