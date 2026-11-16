---
description: Check the DocFila connection and explain how to connect or disconnect
---

Check whether the DocFila connector works by calling get_account.

- If it works, tell me the account name and plan, and which DocFila tools are available in this session.
- If the DocFila tools are missing or the call says the connection expired, explain how to connect: in Claude Code run /mcp, choose "docfila" and sign in with my DocFila account in the browser; or use a DocFila API key with `claude mcp add --transport http docfila https://api.docfila.com/claude/mcp --header "Authorization: Bearer <key>"`.
- To disconnect everywhere, I can visit https://www.docfila.com/claude/connect. More help: https://www.docfila.com/claude
