# OverTheWire Bandit — Notes

Free replacement for TryHackMe's paywalled Linux Fundamentals Parts 2 & 3. Bandit is a free SSH wargame (34 levels) that teaches the same skills: remote login over SSH, file navigation, permissions, pipes, and common Linux utilities.

**Connect:** `ssh bandit0@bandit.labs.overthewire.org -p 2220` (password is the level's password; level 0's is `bandit0`)
**Site:** https://overthewire.org/wargames/bandit/

*Notes added level by level as I play.*

## The free path (what this replaces)
- TryHackMe Linux Fundamentals Part 2 (Premium): SSH, flags/arguments, copying & moving files, file permissions
- TryHackMe Linux Fundamentals Part 3 (Premium): grep, find, pipes/redirection, handy day-to-day utilities
- Bandit covers all of it free, level by level — and it's the classic interview talking point for "how did you learn Linux?"

## Level 0
- First SSH login: `ssh bandit0@bandit.labs.overthewire.org -p 2220`, password `bandit0`
- Goal: a file called `readme` sits in the home directory — read it for the level 1 password
- Commands: `ls` (spot the file), `cat readme` (read it)
- Lesson: SSH syntax is `ssh user@host -p port`; the password you find becomes the *next* level's login

## Levels completed
- [ ] Level 0 → 1
