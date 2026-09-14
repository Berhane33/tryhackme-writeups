# Offensive Security Intro
- **Link:** https://tryhackme.com/room/offensivesecurityintro
- **Date:** 2026-09-14

## What I learned
- The difference between offensive (red team) and defensive (blue team) security roles
- How attackers find hidden pages on websites using directory brute-forcing
- `dirb` wasn't available in the AttackBox, so I used `gobuster` instead

## Key commands
`gobuster dir -u http://fakebank.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

## Notes
- `.thm` sites use plain http, not https
- Read the two discovered URLs and pick the one that sounds like internal tooling (admin/portal/staff), not static content
