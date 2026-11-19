# nxcspray

Multi-protocol credential spray and validator built on top of [NetExec (nxc)](https://github.com/Pennyw0rth/NetExec).

> Derived from tools originally authored by **NTHSec** and **TheHuskyHacker**.

---

## Usage

```
nxcspray <protocols|all> <target> -u <user> -p <pass> [options]
```

Syntax mirrors nxc — if you know nxc, you already know nxcspray.

---

## Examples

```bash
# Spray all protocols against a single host
nxcspray all 10.10.10.10 -u admin -p Password123

# Spray specific protocols against a subnet
nxcspray smb,ldap,winrm 192.168.1.0/24 -u admin -p Password123

# Spray from target and user/pass lists with a domain
nxcspray all hosts.txt -u users.txt -p passes.txt -d corp.local

# Pass-the-hash against SMB
nxcspray smb 10.10.10.10 -u administrator -H aad3b435b51404ee:deadbeef1234

# Local auth against MSSQL
nxcspray mssql 10.10.10.10 -u sa -p Password123 --local-auth
```

---

## Options

| Flag | Description |
|------|-------------|
| `-u USER\|FILE` | Username or file of usernames |
| `-p PASS\|FILE` | Password or file of passwords |
| `-H HASH\|FILE` | NTLM hash or file of hashes (pass-the-hash) |
| `-d DOMAIN` | Domain for authentication |
| `--local-auth` | Force local authentication |
| `-o DIR` | Output directory (default: `./nxcspray_results`) |
| `--no-enum` | Skip auto-enumeration on successful auth |
| `-q` | Quiet mode — only show hits |
| `--help` | Show help |

---

## Supported Protocols

`smb` `ldap` `mssql` `rdp` `winrm` `ftp` `ssh` `vnc` `wmi`

---

## Features

- **Parallel spraying** — all selected protocols run concurrently
- **Auto-enumeration** — on a successful auth, automatically runs deeper enumeration:
  - SMB: shares, sessions, users, groups, disks, password policy
  - LDAP: users, groups, GMSA, delegation, ASREPRoast, Kerberoast
  - MSSQL: privilege check
- **Hit tracking** — results saved per-protocol to the output directory
- **Next-step hints** — summary suggests follow-on tools based on what authenticated

---

## Requirements

- [`nxc`](https://github.com/Pennyw0rth/NetExec) (NetExec)
- `timeout` (GNU coreutils)

---

## Credits

Derived from tools originally authored by **NTHSec** and **TheHuskyHacker**.
