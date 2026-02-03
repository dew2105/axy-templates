# Tool Profiles

Tool profiles control what capabilities an agent has access to. They define which tools the agent can use, creating appropriate sandboxes for different roles.

## How Tool Profiles Work

OpenClaw manages agent permissions through tool profiles. When an agent is invoked, its tool profile determines:

- Which tools are available (read, write, exec, web, etc.)
- Which tool groups are enabled
- Specific denials that override allows

## Profile Format

Tool profiles are JSON files with the following structure:

```json
{
  "profile": "base-profile-name",
  "alsoAllow": ["tool1", "group:groupname"],
  "deny": ["tool1", "tool2"]
}
```

### Fields

| Field | Description |
|-------|-------------|
| `profile` | Base profile to inherit from (minimal, coding, messaging, full) |
| `alsoAllow` | Additional tools/groups to enable on top of the base profile |
| `deny` | Tools to explicitly disable (overrides allows) |

## Base Profiles

### `minimal`
Read-only access with limited tools. Safe for untrusted or new agents.

**Includes**: `read`, `glob`, `grep`, `ls`
**Excludes**: `write`, `edit`, `exec`, all external access

### `coding`
Full development access. The default for most technical roles.

**Includes**: `read`, `write`, `edit`, `exec`, `git`, filesystem access
**Excludes**: External services (browser, gateway, nodes)

### `messaging`
Communication-focused access. For agents that coordinate but don't code.

**Includes**: `read`, `messaging`, `notifications`
**Excludes**: `write`, `exec`, filesystem modifications

### `research`
Web access without system modification. For analysts and researchers.

**Includes**: `read`, `group:web`, `image`
**Excludes**: `write`, `edit`, `exec`

### `full`
All tools enabled. Use with caution for highly trusted agents.

**Includes**: Everything
**Excludes**: Nothing

## Tool Groups

Groups bundle related tools for easier configuration:

| Group | Tools Included |
|-------|----------------|
| `group:fs` | read, write, edit, glob, grep, ls |
| `group:web` | fetch, browser, websearch |
| `group:runtime` | exec, shell, script |
| `group:git` | git-status, git-commit, git-push, git-pull |
| `group:messaging` | slack, email, notify |

## Directory Structure

```
tools/
├── profiles/           # Preset access levels
│   ├── minimal.json
│   ├── coding.json
│   ├── messaging.json
│   ├── research.json
│   └── full.json
└── examples/           # Specialized configurations
    ├── secure-dev.json
    └── readonly-analyst.json
```

## Security Considerations

### Principle of Least Privilege
Start with `minimal` and add only what's needed. It's easier to grant access than to revoke it after a security incident.

### High-Risk Tools
These tools require careful consideration:

- **exec/shell**: Arbitrary code execution
- **browser**: Can access external services
- **gateway**: Network access beyond web
- **nodes**: Can spawn subprocesses
- **cron**: Scheduled execution without oversight

### Recommended Restrictions by Role

| Role | Recommended Profile | Typical Denials |
|------|--------------------|--------------------|
| Researcher | research | exec, write, edit |
| Junior Dev | coding | browser, gateway, nodes |
| Senior Dev | coding | (none) |
| Coordinator | messaging | exec, write |
| Security | coding | (none - needs full visibility) |

## Examples

### Research-Only Agent
```json
{
  "profile": "minimal",
  "alsoAllow": ["group:web", "read", "image"],
  "deny": ["exec", "write", "edit"]
}
```

### Secure Development
```json
{
  "profile": "coding",
  "deny": ["browser", "canvas", "nodes", "cron", "gateway"]
}
```

### Read-Only Analyst
```json
{
  "profile": "minimal",
  "alsoAllow": ["group:web"],
  "deny": ["exec", "write", "edit", "shell"]
}
```

## Applying Profiles

### In OpenClaw Config

Add to your agent's configuration in `~/.openclaw/config.json`:

```json
{
  "agents": {
    "agent-name": {
      "soul": "SOUL-NAME.md",
      "tools": {
        "profile": "coding",
        "deny": ["browser"]
      }
    }
  }
}
```

### Via Amber

When onboarding, specify the profile:
> "Use the research profile but also allow image generation"

## Best Practices

1. **Default to minimal**: Expand access as trust is established
2. **Document denials**: Comment why tools are restricted
3. **Review periodically**: Access needs change over time
4. **Test before deploy**: Verify the agent can do its job with the given tools
5. **Audit tool usage**: Monitor which tools agents actually use
