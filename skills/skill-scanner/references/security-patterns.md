# Security Patterns Reference

> Auto-generated from `@skillplugs/security-patterns`. Do not edit directly.

Detailed patterns for security analysis.

## Capability Detection Patterns

### Files Access

```
open\(
read\(
write\(
Path\(
os\.path
shutil
fs\.
readFile
writeFile
readdir
```

### Command Execution

```
subprocess
os\.system
Popen
exec\(
spawn\(
execSync
child_process
```

### Network Access

```
http://
https://
requests\.
urllib
httpx
aiohttp
fetch\(
axios
curl
wget
```

### Environment Variables

```
os\.environ
os\.getenv
dotenv
process\.env
import\.meta\.env
\$\{?[A-Z_]+\}?
```

## Dangerous Patterns (Security Concern)

### Credential Access

*Access to credential files or secrets*

```
~/.ssh/
~/.aws/
~/.config/
~/.gnupg/
~/.kube/
\.env
credentials
secrets
API_KEY
TOKEN
PASSWORD
SECRET
id_rsa
id_ed25519
PRIVATE_KEY
```

### Supply Chain

*Supply chain attack vectors*

```
curl.*\|.*bash
curl.*\|.*sh
wget.*&&.*sh
wget.*&&.*bash
wget.*\|.*sh
--index-url(?!.*pypi)
registry(?!.*npmjs)
pip install.*--extra-index
```

### Privilege Escalation

*Privilege escalation attempts*

```
sudo(?!.*apt)(?!.*brew)
doas
su\s+-
runas\s+/user:Administrator
chmod\s+777
chmod\s+\+s
chown\s+root
setcap
getcap
```

### Persistence

*System persistence mechanisms*

```
crontab
cron\.d
/etc/cron
launchd
launchctl
systemctl\s+enable
/etc/init\.d
/etc/rc\.local
~/.bashrc
~/.zshrc
~/.profile
~/.bash_profile
schtasks
HKEY_.*\Run
```

### Prompt Injection

*Prompt injection attempts targeting Claude*

```
ignore\s+(previous|all)\s+instructions
forget\s+(your|all)\s+rules
you\s+are\s+now
disregard\s+safety
pretend\s+you\s+can
act\s+as\s+if
bypass
override\s+(your|all)
SYSTEM:
\[INST\]
<\|im_start\|>
<\|system\|>
```

### Path Traversal

*Path traversal attacks*

```
\.\./\.\./\.\./
\.\.\\.\.\\.\.
/etc/passwd
/etc/shadow
/etc/hosts
C:\Windows\System32
/root/
/home/\*/
```

### Command Injection

*Command injection vulnerabilities*

```
os\.system\(f["']
subprocess\.run\(f["'].*shell=True
subprocess.*shell=True.*\{
exec\(f["']
`\$\{
eval\(["'].*\+
```

### Data Exfiltration

*Data exfiltration attempts*

```
curl.*-X\s*POST
curl.*--data
requests\.post\(
fetch\(.*method:\s*["']POST
webhook
```

### Obfuscation

*Code obfuscation*

```
eval\(atob
eval\(Buffer\.from
eval\(base64
atob\(
btoa\(
b64decode\(
b64encode\(
base64\.b64decode
base64\.b64encode
Buffer\.from.*base64
rot13
\x[0-9a-fA-F]{2}\x[0-9a-fA-F]{2}
```

## Review Patterns (Worth Noting)

### Unknown package dependencies

```
requirements\.txt
package\.json
Gemfile
go\.mod
```

### Non-standard external services

```
webhook
:\d{4,5}/
```

### Sudo usage (may be legitimate)

```
sudo\s+apt
sudo\s+brew
sudo\s+pip
```

### Limited path traversal

```
\.\./[^.]
```

## Safe Patterns (Passed)

### Trusted External APIs

```
api.github.com
registry.npmjs.org
pypi.org
api.openai.com
api.anthropic.com
cdn.jsdelivr.net
unpkg.com
raw.githubusercontent.com
```

### Known Safe Packages

**Python:**
```
pypdf, pdfplumber, reportlab, requests, httpx, aiohttp, pandas, numpy, scipy, pillow, opencv-python, pytest, unittest, black, ruff
```

**JavaScript:**
```
react, vue, angular, svelte, express, fastify, hono, axios, node-fetch, jest, mocha, vitest, typescript, eslint, prettier
```

### Standard Tools

```
pdftotext, pandoc, imagemagick, ghostscript, tesseract, git, npm, pnpm, yarn, pip, cargo, go, make, cmake, webpack, vite, esbuild, jq, yq, grep, find, ls, cat
```

## Severity Summary

| Risk | Severity | Action |
|------|----------|--------|
| Credential Access | Concern | Block unless justified |
| Supply Chain | Concern | Block unless justified |
| Privilege Escalation | Concern | Block unless justified |
| Persistence | Concern | Block unless justified |
| Prompt Injection | Concern | Block unless justified |
| Path Traversal | Concern | Block unless justified |
| Command Injection | Concern | Block unless justified |
| Data Exfiltration | Concern | Block unless justified |
| Obfuscation | Concern | Block unless justified |
| Unknown package dependencies | Review | Warn user |
| Non-standard external services | Review | Warn user |
| Sudo usage (may be legitimate) | Review | Warn user |
| Limited path traversal | Review | Warn user |