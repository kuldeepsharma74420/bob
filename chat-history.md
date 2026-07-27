# Bob Chat History
**Date:** Today  
**Topic:** Bob Features & Capabilities Deep Dive

---

## 1. Modes

**Q: How many modes do you have?**

Bob has **3 built-in modes**:

- **Plan** — For planning, designing, and strategizing before implementation. Great for breaking down complex problems, creating technical specifications, and designing architecture.
- **Agent** — For writing, modifying, or refactoring code. Ideal for implementing features, fixing bugs, creating new files, or making code improvements.
- **Ask** — For explanations, documentation, and answers to technical questions. Best for understanding concepts, analyzing existing code, or learning about technologies without making changes.

---

## 2. Permissions (Groups) Feature

**Q: What is the permissions feature and how to use it?**

When creating a **custom mode**, you can control exactly what that mode is allowed to do using **permission groups** declared under the `groups` field in the mode's YAML configuration.

### Available Permission Groups

| Group | What It Allows |
|---|---|
| `read` | Reading files and looking up code symbols |
| `edit` | Writing and modifying files |
| `execute` | Running shell commands |
| `mcp` | Using MCP server tools |
| `skill` | Using the `use_skill` tool |
| `todo` | Using the `update_todo_list` tool |
| `subagent` | Using the `spawn_subagent` tool |
| `mode` | Using the `switch_mode` tool |

### Key Rules
- Omitting `groups` gives the mode **NO tool access**
- Use **exact group names** — typos silently grant nothing
- No duplicate group names — duplicates drop the entire file
- You can restrict editing to specific file types using `fileRegex`

---

## 3. Purpose of Custom Modes

**Q: Why do we need to create custom modes?**

### Reasons to Create Custom Modes

1. **Focused Behavior / Persona** — Each mode has its own `roleDefinition` that defines how Bob thinks and behaves (e.g. a Security Reviewer, Docs Writer, DevOps Engineer)
2. **Controlled Tool Access** — Restrict what Bob can do (read-only mode, docs-only mode, no-shell mode)
3. **Context Switching** — Different tasks need different mindsets
4. **Team / Project Standardization** — Workspace-scoped modes can be committed to version control
5. **Custom Instructions Per Mode** — Each mode can enforce project-specific conventions

---

## 4. DevOps Engineer Custom Mode

**Q: Can we create a custom mode for deploying applications in Kubernetes?**

Yes! A DevOps Engineer mode was created globally at `~/.bob/settings/custom_modes.yaml`:

```yaml
customModes:
  - slug: devops-engineer
    name: DevOps Engineer
    roleDefinition: >-
      You are an experienced DevOps engineer specializing in Kubernetes, Docker,
      Helm, and CI/CD pipelines. You help deploy, configure, scale, and monitor
      applications on Kubernetes clusters.
    whenToUse: Use when deploying, configuring, or managing applications on Kubernetes.
    customInstructions: >-
      Always validate Kubernetes manifests before applying. Prefer Helm charts
      for deployments. Use namespaces to isolate environments. Always set
      resource limits and requests. Follow the principle of least privilege
      for RBAC. Prefer rolling updates over recreate strategies.
    groups:
      - read
      - edit
      - execute
      - mcp
```

---

## 5. How to Create a Custom Mode Manually

**Q: Can I create the mode manually? Give the steps.**

### Steps

1. **Decide the Scope** — Global (`~/.bob/settings/custom_modes.yaml`) or Workspace (`.bob/custom_modes.yaml`)
2. **Open or Create the File** — Navigate to the file path and open or create it
3. **Write Your Mode Entry** — Use the YAML template with `slug`, `name`, `roleDefinition`, `groups`
4. **Choose Permission Groups** — Only include groups your mode actually needs
5. **Optionally Restrict File Editing** — Use `fileRegex` for specific file types
6. **Ensure Slug is Unique** — Letters, numbers, dashes only. No duplicates!
7. **Append to Existing File** — Never overwrite, always append under `customModes:`
8. **Save the File** — Hot-reloads automatically, no restart needed

### Common Mistakes to Avoid
- Duplicate slug → entire file is dropped
- Wrong group name (`write`, `command`) → silently grants nothing
- Invalid `fileRegex` → entire file is dropped
- Global mode in wrong path → mode never loads
- Smart/curly quotes → YAML parsing fails

---

## 6. MCP Tools

**Q: What is the MCP tool and what is its purpose?**

**MCP = Model Context Protocol** — an open protocol that allows Bob to connect to external tools and services through a standardized interface.

### Without MCP
Bob can only run AWS CLI commands via shell. It cannot:
- Connect to RDS databases directly
- Call Bedrock APIs directly
- Get structured, real-time data from AWS services

### With MCP
Full programmatic access — like a developer using the AWS SDK:
- Query RDS databases, run SQL
- Invoke Bedrock foundation models
- Browse S3 buckets, read/write objects
- Query EKS cluster state
- Fetch CloudWatch logs and metrics

### MCP Config Example
```json
{
  "mcpServers": {
    "aws-rds": {
      "command": "npx",
      "args": ["-y", "@aws/amazon-rds-mcp-server"],
      "env": { "AWS_REGION": "us-east-1" }
    }
  }
}
```

### Config File Locations
| Scope | Path |
|---|---|
| Global | `~/.bob/settings/mcp.json` |
| Workspace | `.bob/mcp.json` |

---

## 7. AWS RDS MCP Server

**Q: Configure AWS RDS MCP server (workspace-scoped, IAM Role auth)**

Configured at `.bob/mcp.json` using IAM Role (no keys needed):

```json
{
  "mcpServers": {
    "aws-rds": {
      "command": "npx",
      "args": ["-y", "@aws/amazon-rds-mcp-server"],
      "env": { "AWS_REGION": "us-east-1" }
    }
  }
}
```

**Prerequisites:**
- Node.js installed (`node --version`)
- Update `AWS_REGION` to match your actual region
- IAM Role needs: `rds:DescribeDBInstances`, `rds-data:ExecuteStatement`

---

## 8. Skills (`use_skill`)

**Q: What is the use_skill tool and how does it work?**

Skills are **specialized instruction sets** (SKILL.md files) that Bob loads before tackling specific tasks — like reading a procedure manual before performing an operation.

### Available Skills
| Skill | Activates When |
|---|---|
| `create-skill` | User wants to create a new Bob skill |
| `create-mode` | User wants to create a new custom mode |
| `configure-mcp` | User wants to add or troubleshoot an MCP server |
| `build-mcp-server` | User wants to build a custom MCP server |
| `xlsx-insights` | User wants to analyze Excel files |

### Skill File Locations
| Scope | Path |
|---|---|
| Global | `~/.bob/skills/<skill-name>/SKILL.md` |
| Workspace | `.bob/skills/<skill-name>/SKILL.md` |

---

## 9. k8s-deploy Skill (Created)

**Q: Create a skill for deploying applications to Kubernetes**

Created globally at `~/.bob/skills/k8s-deploy/SKILL.md`:

- **Activation:** Manual — type `/k8s-deploy`
- **Scope:** Global (all workspaces)

### Workflow Steps
1. Gather app details (name, image, port, replicas, namespace)
2. Choose deployment method (plain manifests or Helm chart)
3. Generate Kubernetes manifests OR Helm chart
4. Validate using `kubectl dry-run` or `helm lint`
5. Apply the deployment
6. Verify pods are running
7. Provide summary and next steps

---

## 10. Todo List (`update_todo_list`)

**Q: What is the todo tool?**

Bob's built-in task management system for tracking progress of complex, multi-step work.

### Status Symbols
| Symbol | Meaning |
|---|---|
| `[x]` | Completed |
| `[-]` | In Progress |
| `[ ]` | Pending |

### When Bob Uses It
- Complex tasks with multiple steps
- Tasks involving multiple files
- Tasks that benefit from step-by-step tracking
- When new steps are discovered mid-task

### Rules
- Always provides the full list on every update
- Marks completed immediately after each task
- Never removes unfinished tasks
- Adds new todos dynamically when discovered

---

## 11. Subtasks (`start_subtask`)

**Q: What is the start_subtask tool?**

Spins up a **new, focused task instance** with its own title, instructions, and todo list — like opening a dedicated workspace for a specific piece of work.

### Workflow
```
Main Task
  ├── Subtask 1: Implement Feature A  → Review & Approve
  ├── Subtask 2: Write Tests          → Review & Approve
  └── Subtask 3: Update Docs         → Review & Approve
```

### Subtask vs Todo vs Subagent
| Feature | Todo List | Subtask | Subagent |
|---|---|---|---|
| Purpose | Track steps | Separate focused task | Isolated side work |
| Context | Same conversation | New task instance | Isolated context |
| Output | Visual checklist | Full task completion | Summary back to Bob |
| Parallelism | ❌ | ❌ | ✅ |
| User review | ❌ | ✅ | ❌ |

---

## 12. Subagents (`spawn_subagent`)

**Q: What is the spawn_subagent tool?**

Creates an **independent agent** in its own isolated context to handle focused, self-contained work — then automatically returns a summary and is destroyed.

### Lifecycle
```
Bob CREATES subagent → ASSIGNS task → Subagent WORKS independently
→ RETURNS summary → AUTOMATICALLY DESTROYED → Bob USES summary
```

### Two Types
| Type | Name | Best For |
|---|---|---|
| Explorer | `"explore"` | Reading files, researching codebase |
| General | `"general"` | Full implementation work |

### fork_context Option
- `false` — Subagent only needs the description (default)
- `true` — Subagent needs prior conversation history

---

## 13. Mode Switching (`switch_mode`)

**Q: What is the switch_mode tool?**

Allows Bob to **automatically switch between modes** during a task without manual intervention.

### Example from Our Conversation
Bob was in Plan mode, tried to write `custom_modes.yaml`, got blocked (Plan mode only allows `.md`/`.txt`), automatically switched to Agent mode, and completed the task.

### Typical Workflow
```
Plan Mode → (design & plan) → switch_mode("agent") → Agent Mode → (implement)
```

---

## 14. Bob Findings

**Q: What is the Bob Findings feature in the status bar?**

A **dedicated UI panel** that collects and displays important observations, issues, suggestions, or insights Bob notices while working on code — separate from the chat conversation.

### Types of Findings
- 🐛 Bugs detected
- ⚠️ Warnings
- 🔒 Security issues
- 💡 Suggestions
- 📋 Code smells
- ✅ Observations

### The Counter
The `0` next to Bob Findings is a **notification badge** — it increases as Bob flags issues. Click it to open the Findings panel.

---

## 15. Other Bob Features (Not Yet Explored)

| Feature | Purpose |
|---|---|
| `create_html_artifact` | Generate visual HTML reports as saveable tiles |
| `FindSymbol` / `GetSymbolsOverview` | Deep code intelligence — find classes, functions, references |
| `grep` / `glob` | Search codebase by content or file name pattern |
| `read_xlsx` | Read and analyze Excel spreadsheets |
| `read_file` (images/PDF) | Visually analyze images, PDFs, DOCX files |
| `apply_diff` / `search_and_replace` | Surgical, precise code edits |
| `start_workflow` | Pre-defined structured workflows for common tasks |
| `build-mcp-server` skill | Guide to building a custom MCP server from scratch |
| `xlsx-insights` skill | Deep Excel file analysis with auto-generated scripts |

---

## Summary — Complete Bob Feature Map

```
BOB
├── Modes: Plan | Agent | Ask | Custom Modes
├── Task Management: Todo List | Subtasks | Subagents
├── Code Intelligence: FindSymbol | grep | glob
├── File Operations: read | write | apply_diff | insert
├── External Integrations: MCP Tools | execute_command
├── Skills: create-skill | create-mode | configure-mcp | build-mcp-server | xlsx-insights
├── Output: create_html_artifact | Bob Findings
└── Navigation: switch_mode | start_workflow
```

---

*Chat history saved by Bob*
