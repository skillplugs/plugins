# Skill Scanner

Security scanner for Claude Code skills. Analyze skills for potential security concerns before installation.

## Features

- **9 Security Checks**: Credential access, supply chain, privilege escalation, persistence, prompt injection, path traversal, command injection, data exfiltration, obfuscation
- **Capability Detection**: Files, commands, network, environment access
- **Multiple Sources**: Scan from GitHub URL, local path, or installed skills

## Installation

In Claude Code, run:

```bash
/plugin marketplace add skillplugs/plugins
/plugin install skill-scanner@skillplugs
```

## Usage

Ask Claude to scan any skill:

**From GitHub:**
```
"Scan https://github.com/user/some-skill"
"Is this skill safe? https://github.com/anthropics/skill-example"
```

**From local path:**
```
"Check security of ./my-local-skill"
```

**Installed skills:**
```
"Is the pdf skill I installed safe?"
"Scan my installed docx skill"
```

## Example Output

```
## Skill Security Scan
*Powered by Skillplugs • Scanner v2.5.0*

**Status:** Passed

**Capabilities:**
- Files: Yes
- Commands: No
- Network: No
- Environment: No

**Security Checks:** 9/9 passed

**Summary:** Document processing skill with appropriate file access.
```

## Security Checks

| Check | Description |
|-------|-------------|
| Credential Access | ~/.ssh, ~/.aws, tokens, secrets |
| Supply Chain | curl\|bash, untrusted registries |
| Privilege Escalation | sudo, chmod 777, setuid |
| Persistence | cron, launchd, shell profiles |
| Prompt Injection | "ignore instructions", bypass |
| Path Traversal | ../../../, system paths |
| Command Injection | shell=True with variables |
| Data Exfiltration | POST to unknown endpoints |
| Obfuscation | base64 decode, eval patterns |

## License

MIT

## Links

- [Skillplugs](https://skillplugs.com)
- [Issues](https://github.com/skillplugs/plugins/issues)
