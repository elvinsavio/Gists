---
title: "Github SSH Setup"
date: 2026-01-22T06:40:48+05:30
weight: 1
tags: ["github", "ssh", "setup", "security"]
---

## How to Setup Single SSH keys for github. [Linux]

1. CD into .ssh
```bash
cd ~/.ssh/
```

2. Generate keys and save
> ~/.ssh/id_ed25519
```bash
ssh-keygen -t ed25519 -C "email@example.com"
```

3. Start ssh-agent
```bash
eval "$(ssh-agent -s)"
```


4. Add the key to the ssh-agent
```bash
ssh-add ~/.ssh/id_ed25519
```


5. Open [github](https://github.com/settings/keys)
- Navigate to Profile > Setting > SSH and GPG Keys.
- Click on New SSH Key
- Paste the Public Key Content in the "Key field"
- Click on ADD


---

## Setup Two or More Different SSH Keys for Different GitHub Accounts [Linux]

This setup is useful when you have, for example, personal and work GitHub accounts on the same machine.


1. Generate separate SSH keys
Create one key per account with clear names.

    Personal
    ```bash
    ssh-keygen -t ed25519 -C "personal@email.com" -f ~/.ssh/id_ed25519_personal
    ```

    Work
    ```bash
    ssh-keygen -t ed25519 -C "work@email.com" -f ~/.ssh/id_ed25519_work
    ```

2. Start ssh-agent and add both keys
```bash
eval "$(ssh-agent -s)"
```

3. Add the key to the ssh-agent
```bash
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

4. Open the SSH Config

```bash
vim ~/.ssh/config
```

5. Add the keys to config

```bash
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes

```