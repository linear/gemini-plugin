---
name: linear-workspace
description: Works in the user's Linear workspace through the Linear MCP server, including issues, projects, cycles, initiatives, status updates, and documents. Use when the user asks to "find my Linear issues", "create a Linear issue", "update LIN-123", "how is the project going", "post a project update", or "find the spec in Linear". Don't use for other issue trackers or for work outside Linear.
---

# Linear Workspace

The Linear MCP server's tool descriptions and input schemas are the source of truth for tool names, parameters, and behavior. They change as Linear adds tools. Follow them. Do not ask the user to install anything locally.

## Workflow

1. **Resolve**: Pass human-readable references directly: issue identifiers such as `LIN-123`, project identifiers such as `P-ENG-12`, team names or keys, user names or emails, and `"me"` for the signed-in user. Look up teams or users only when a reference is ambiguous or unknown, and ask the user to choose when it matches more than one item. Never guess an ID.
2. **Read**: Use the narrowest query that answers the question. List results are paged: when more pages exist, fetch them instead of treating the first page as complete, or say that the result is partial.
3. **Check before writing**: Search for an existing item before you create one. Show the planned change and ask the user to confirm first when the request is ambiguous, changes many items, or posts text that you drafted for other people to read, such as a status update.
4. **Verify**: Read the write tool's response. Tell the user what changed and include the link from the response. If a call fails, report the error instead of retrying with guessed values.

If no tool can do what the user asks, say that the capability is not available.

## Linear Conventions

- **Team-scoped values**: Statuses and labels belong to a team and differ between teams. When you are not sure that a value exists, list the statuses or labels for that team before you filter or set it.
- **Comments**: Getting an issue does not return its discussion. Read its comments separately.
- **Images and files**: Descriptions, comments, and documents can embed images as Markdown. Use the image extraction tool to view them. Linear upload URLs expire after a few minutes, so fetch them again instead of reusing old URLs.
- **Create or update**: Tools named `save_*` create an item when you omit `id` and update it when you pass `id`. When you update, send only the fields that change. To edit part of a long description or document, use `patch` instead of resending the full content.
- **Labels**: Setting `labels` replaces every label on the item. To add or remove one label, use `addLabels` or `removeLabels`.
- **Text**: Send Markdown with real line breaks, not escaped `\n` sequences. Mention people as `@displayName`. Upload files with the upload tool and insert the Markdown it returns; do not inline base64 data.
- **Issue descriptions**: Write for people. Keep sentences short and use one term for one concept. Put long agent-specific detail, such as plans or logs, at the end in a collapsible section that opens with `+++ Agent notes` and closes with `+++` on its own line.
