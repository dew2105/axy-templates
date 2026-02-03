# Soul Templates

Soul files define an agent's identity, personality, expertise, and behavior guidelines. They're the "personality injection" that transforms a base AI model into a specialized team member.

## How Souls Work

When an agent is invoked, the `axy-personas` hook injects the appropriate soul file into the system prompt. This gives the agent:

- **Identity**: Name, role, and purpose
- **Expertise**: Domain knowledge and skills
- **Personality**: Communication style and traits
- **Guidelines**: How to approach tasks and interactions

## Soul File Format

Soul files are Markdown documents with a specific structure:

```markdown
# [Name] - [Role Title]

You are [Name], the [Role] for Axy. [One-sentence purpose].

## Core Responsibilities

- **[Area]**: [Description of responsibility]
- **[Area]**: [Description of responsibility]

## Communication Style

- [Trait description]
- [Trait description]

## [Domain-Specific Section]

[Relevant details for this role's expertise area]

## Team Interactions

- **With [Role]**: [How to interact]
- **With [Role]**: [How to interact]

## Interaction Guidelines

- [Guideline]
- [Guideline]
```

## Directory Structure

```
souls/
├── roles/          # Base role templates
│   ├── developer.md
│   ├── researcher.md
│   ├── coordinator.md
│   ├── writer.md
│   └── security.md
├── traits/         # Personality modifiers
│   ├── concise.md
│   ├── thorough.md
│   └── creative.md
└── examples/       # Complete soul files
    ├── SOUL-AXEL.md
    ├── SOUL-AMBER.md
    └── SOUL-ZEPHYR.md
```

## Using Role Templates

Role templates provide a starting point. To create a new agent:

1. **Choose a base role** from `roles/`
2. **Customize the identity** (name, specific title)
3. **Add domain specifics** relevant to their expertise
4. **Apply trait modifiers** from `traits/` if desired
5. **Save as** `SOUL-{NAME}.md` in `~/.openclaw/workspace/`

## Customization Points

When adapting a template, focus on:

### Identity Section
- Choose a memorable, appropriate name
- Refine the role title for specificity
- Adjust the purpose statement

### Responsibilities
- Add or remove based on actual scope
- Be specific about what they handle vs. delegate

### Communication Style
- Match the team's culture
- Consider the role's needs (technical vs. user-facing)

### Domain Sections
- Add expertise areas specific to their focus
- Include relevant methodologies or frameworks
- List tools or technologies they specialize in

## Trait Modifiers

Trait files in `traits/` are snippets you can incorporate into a soul. They modify communication style or approach:

- **concise.md**: Emphasizes brevity and efficiency
- **thorough.md**: Prioritizes completeness and detail
- **creative.md**: Encourages innovative thinking

To apply a trait, incorporate its guidelines into the Communication Style or Interaction Guidelines sections.

## Best Practices

1. **Be specific**: Vague souls produce vague behavior
2. **Stay focused**: One role per agent, delegate other concerns
3. **Define boundaries**: What they handle vs. escalate
4. **Include team context**: Who they work with and how
5. **Test and iterate**: Refine based on actual interactions

## Examples

See the `examples/` directory for complete soul files from the Axy core team:

- **SOUL-AXEL.md**: Chief of Staff - orchestration and delegation
- **SOUL-AMBER.md**: HR + Recruiting - agent onboarding
- **SOUL-ZEPHYR.md**: Chief of Security - security oversight
