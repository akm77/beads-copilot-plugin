---
description: Manage issue templates for streamlined issue creation
argument-hint: list|show|create [template-name]
---

Manage issue templates for streamlined issue creation.

## Commands

### list
List all available templates (built-in and custom).
```bash
bd template list
bd template list --json
```

### show
Show detailed structure of a specific template.
```bash
bd template show <template-name>
bd template show <template-name> --json
```

### create
Create a custom template in `.beads/templates/` directory.
```bash
bd template create <template-name>
```

## Using Templates with `bd create`

Use the `--from-template` flag to create issues from templates:
```bash
bd create --from-template <template-name> "Issue title"
```

Template values can be overridden with explicit flags:
```bash
bd create --from-template bug "Login crashes on special chars" -p 0
bd create --from-template epic "Q4 Infrastructure" -l infrastructure,ops
```

## Built-in Templates

- **epic**: Large features (type: epic, priority: P1)
- **bug**: Bug reports (type: bug, priority: P1)
- **feature**: Feature requests (type: feature, priority: P2)

## Custom Templates

Custom templates in `.beads/templates/` override built-in templates with the same name. Templates are YAML files with: name, description, type, priority, labels, design, acceptance_criteria.
