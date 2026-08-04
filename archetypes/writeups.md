+++
title = "Challenge Name"
date = {{ .Date }}
draft = true
toc = true
tags = ["category", "technique"]        # e.g. ["web", "sqli"], ["pwn", "rop"], ["crypto", "rsa"]
categories = ["writeups"]

# Optional metadata — delete any you don't use
[params]
  event      = "CTF Name 2026"          # competition/event this was from, if any
  difficulty = "medium"                 # easy / medium / hard / insane
  points     = 250
  solves     = 0                        # fill in after, if known
+++

## Challenge

Brief description of the challenge as given — what you were told, what files
or endpoints you were handed, what the goal was (get a flag, RCE, read a file,
etc).

## Recon

What you found before touching anything: service versions, exposed endpoints,
file structure, anything `file`, `strings`, `nmap`, a directory brute-force,
or just reading the source turned up.

## Exploitation

The actual walkthrough. Keep it in the order you solved it, not necessarily
the order that would be obvious in hindsight — the dead ends are often the
useful part for a reader in the same spot.

```python
# exploit code, payloads, requests — whatever got you there
```

## Flag

## Takeaways

What you'd do differently, what the underlying bug/technique actually was
in general terms, and any tools or references worth remembering for next
time.
