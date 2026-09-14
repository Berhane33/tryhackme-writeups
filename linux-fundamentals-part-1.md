# Linux Fundamentals Part 1 — TryHackMe Notes

Hands-on notes from the TryHackMe Linux Fundamentals Part 1 room (linuxfundpart1v3). Commands, methods, and lessons — worked through on the in-browser lab machine as user `tryhackme`.

*In progress — notes added as I work through the room.*

## Navigation basics
- `pwd` — prints the current directory (present working directory); answers "where am I?"
- `ls` — lists files and folders in the current directory
- `ls -R` — recursive listing: shows the current directory *and* the contents of every subfolder in one shot. Fast way to see which folders actually contain files
- `cd` — change directory; bare `cd` with no argument returns you to the home directory
- `echo` — prints text (bare `echo` prints a blank line); `whoami` — shows the current user

## Reading files
- `cat <file>` — prints a file's contents, e.g. `cat folder1/passwords.txt`
- `cat` with **no filename** doesn't fail — it waits for keyboard input (stdin). Escape with **Ctrl+C**
- Stuck terminal rule of thumb: Ctrl+C interrupts the running command and returns the prompt

## Finding things
- When a task says "one of these folders contains a file," run `ls -R` instead of opening folders one by one — the folder with contents stands out immediately
- Then read the file with its path: `cat folder1/passwords.txt`

## Lessons
- The shell tells you a lot if you read it: the prompt `tryhackme@linux1:~$` shows user, machine, and current directory (`~` = home)
- Small commands compose: `ls -R` + `cat <path>` is a complete "find and read" workflow with no extra tooling
- When a command hangs, don't close the terminal — Ctrl+C first. Closing loses your session history
