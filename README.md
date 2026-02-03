# Axy Templates

A collection of soul and tool provisioning templates for [Axy](https://github.com/anthropics/axy) agents. These templates help you quickly onboard new AI agents with well-defined personas and appropriate tool access.

## Quick Start

### For Axel (Chief of Staff)
When delegating to a new specialist, browse the templates to find a matching role:
1. Check `souls/roles/` for base persona templates
2. Review `tools/profiles/` for appropriate access levels
3. Send requirements to Amber for customization and onboarding

### For Amber (HR)
When onboarding a new agent:
1. Start with a role template from `souls/roles/`
2. Add personality modifiers from `souls/traits/`
3. Select a tool profile from `tools/profiles/`
4. Customize the soul file for the specific agent
5. Save to `~/.openclaw/workspace/SOUL-{NAME}.md`

## Repository Structure

```
axy-templates/
├── souls/              # Personality and expertise definitions
│   ├── roles/          # Base role templates (developer, researcher, etc.)
│   ├── traits/         # Personality modifiers (concise, thorough, etc.)
│   └── examples/       # Complete soul files from the core team
├── tools/              # Tool access configurations
│   ├── profiles/       # Preset access levels (minimal, coding, full, etc.)
│   └── examples/       # Specialized tool configurations
└── agents/             # Complete agent configs (soul + tools combined)
    └── examples/       # Ready-to-use agent definitions
```

## Using Templates

### Soul Templates

Soul files define an agent's personality, expertise, and behavior guidelines. They're written in Markdown and injected via the `axy-personas` hook.

```markdown
# Agent Name - Role Title

You are [Name], the [Role] for Axy. [Core purpose statement].

## Core Responsibilities
- Responsibility 1
- Responsibility 2

## Communication Style
- Trait 1
- Trait 2

## Interaction Guidelines
- Guideline 1
- Guideline 2
```

See `souls/README.md` for complete documentation.

### Tool Profiles

Tool profiles control what capabilities an agent has access to. They're defined in JSON and configure OpenClaw's permission system.

```json
{
  "profile": "minimal",
  "alsoAllow": ["group:web", "read"],
  "deny": ["exec", "write"]
}
```

See `tools/README.md` for complete documentation.

## Applying Templates

### Manual Application

1. Copy the soul template to your workspace:
   ```bash
   cp souls/examples/SOUL-AXEL.md ~/.openclaw/workspace/
   ```

2. Configure tool access in your OpenClaw settings

### Via Amber

Ask Amber to onboard a new agent using a template:
> "Amber, please onboard a new developer using the developer role template with the coding tool profile"

## Contributing

We welcome contributions! To add a new template:

1. Fork this repository
2. Add your template following the existing patterns
3. Include clear documentation in the template
4. Submit a pull request

### Template Guidelines

- Keep templates focused and single-purpose
- Use clear, descriptive names
- Include comments explaining customization points
- Test templates before submitting

## License

MIT License - see LICENSE file for details.

## Related Projects

- [Axy](https://github.com/anthropics/axy) - The Axy agent framework
- [OpenClaw](https://github.com/anthropics/openclaw) - Agent configuration and management
