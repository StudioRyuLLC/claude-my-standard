---
description: Documents the CLIs available in each environment and when to prefer them over their MCP equivalents. Use when you need to deploy, check deployment status, manage a project, or manage environment variables, or when you are about to call an MCP tool that a CLI also covers.
---

# External CLI Tools

Prefer the CLI over the MCP equivalent whenever you already know which operation you need. CLIs are faster, cheaper in context, and avoid loading hundreds of MCP tool schemas. Fall back to the MCP only when you are exploring, don't know the operation yet, or the CLI lacks it.

## Vercel

Use the Vercel CLI instead of the Vercel MCP for deployment status, project management, and environment configuration.

| Task | Command |
|------|---------|
| Deployment status (list deployments) | `vercel ls` |
| List environment variables | `vercel env ls` |

Use the CLI for:

- **Deployment status:** `vercel ls`
- **Project management:** linking, inspecting, and configuring projects
- **Environment configuration:** `vercel env ls`, plus add, remove, and pull

Use the Vercel MCP only when the CLI cannot do the job or you need to discover what is possible.

## Adding a New CLI

Add one section per CLI, following the Vercel layout:

1. Name the CLI and what it replaces (the MCP server or tools).
2. List the tasks it covers with the exact command for each.
3. State when the MCP is still the right choice.


## Vercel CLI

Prefer Vercel CLI over Vercel MCP when the required operation
is already known and can be executed directly.

### Deployment
- vercel ls
- vercel inspect <deployment>
- vercel logs <deployment>
- vercel deploy
- vercel deploy --prod
- vercel rollback

### Project Management
- vercel project ls
- vercel project inspect <name>
- vercel link
- vercel dev

### Environment
- vercel env ls
- vercel env add
- vercel env rm
- vercel env pull

### Domains
- vercel domains ls
- vercel alias ls

### Safety
- Check project and environment before deployment.
- Never deploy to production without explicit approval.
- Never modify or delete environment variables without approval.
- Never expose environment variable values or credentials.
- Never roll back production without approval.

