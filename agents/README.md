# Agent Configurations

Complete agent configurations combine a soul (personality/expertise) with a tool profile (capabilities). These ready-to-use configs can be directly applied to onboard new agents.

## Agent Config Format

```json
{
  "name": "agent-name",
  "description": "Brief description of the agent's purpose",
  "soul": "path/to/SOUL-NAME.md",
  "tools": {
    "profile": "profile-name",
    "alsoAllow": ["additional-tools"],
    "deny": ["restricted-tools"]
  },
  "metadata": {
    "role": "role-category",
    "team": "team-name",
    "clearance": "access-level"
  }
}
```

## Fields

| Field | Description |
|-------|-------------|
| `name` | Unique identifier for the agent |
| `description` | What this agent does |
| `soul` | Path to the soul file (relative to workspace) |
| `tools` | Tool access configuration |
| `tools.profile` | Base profile (minimal, coding, research, messaging, full) |
| `tools.alsoAllow` | Additional tools beyond the profile |
| `tools.deny` | Tools to restrict from the profile |
| `metadata` | Optional metadata for organization |

## Using Agent Configs

### Apply to OpenClaw

Add the agent configuration to `~/.openclaw/config.json`:

```json
{
  "agents": {
    "junior-dev": {
      "soul": "SOUL-JUNIOR-DEV.md",
      "tools": {
        "profile": "coding",
        "deny": ["browser", "gateway"]
      }
    }
  }
}
```

### Via Amber

Reference an example when onboarding:
> "Amber, onboard a new agent similar to the junior-dev example, but specialized in Python"

## Choosing the Right Config

### By Experience Level

| Level | Recommended Config | Tool Profile |
|-------|-------------------|--------------|
| Junior/New | junior-dev | coding (restricted) |
| Senior | senior-engineer | coding |
| Lead | senior-engineer | coding or full |

### By Function

| Function | Recommended Config | Tool Profile |
|----------|-------------------|--------------|
| Development | junior-dev, senior-engineer | coding |
| Research | security-auditor (read-only) | research |
| Coordination | (use coordinator role) | messaging |
| Security | security-auditor | coding |

## Customizing Configs

Start with an example that's close to your needs, then:

1. **Copy the soul template** and customize identity/expertise
2. **Adjust tool permissions** based on trust level and needs
3. **Add domain-specific sections** to the soul
4. **Test the configuration** before full deployment

## Security Considerations

- New agents should start with restricted tool access
- Expand permissions as trust is established
- Review tool usage periodically
- Document why specific tools are denied

## Examples

See the `examples/` directory for complete configurations:

- **junior-dev.json**: Entry-level developer with restricted access
- **senior-engineer.json**: Experienced developer with full coding access
- **security-auditor.json**: Security specialist with read + analysis focus
