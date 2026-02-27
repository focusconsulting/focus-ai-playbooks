---
title: "MCP Server: SQL Database"
description: "Connect Claude to a SQL database so it can query data directly during conversations."
tags:
  - tooling
---

## What This Does

An MCP (Model Context Protocol) server acts as a bridge between Claude and an external tool or data source. In this case, you're connecting Claude to a SQL database so it can run queries, explore schemas, and pull data without you copying and pasting results back and forth.

Once set up, you can ask Claude things like "what were our top ten customers by revenue last quarter" and it will write the SQL, run it against your database, and work with the results — all within the conversation. You stay in control of what it has access to and can review queries before they execute.

## When to Set This Up

- You regularly pull data from a SQL database as part of your work and want Claude to query it directly.
- You're doing analysis or reporting where the bottleneck is writing queries and wrangling results, not the thinking itself.
- You want Claude to explore a database schema to help you understand what's available or how tables relate.
- You're building briefings, reports, or documents that need live data rather than stale exports.

## What You'll Need

- A SQL database you can connect to (PostgreSQL, MySQL, SQLite, etc.)
- Connection credentials (host, port, database name, username, password)
- Node.js installed on your machine (required to run MCP servers)
- Claude Desktop (MCP servers don't work in the web interface)

## Setup

### Pick an MCP server package

There are community-maintained MCP servers for most popular databases. The common ones:

- **PostgreSQL** — `@modelcontextprotocol/server-postgres`
- **SQLite** — `@modelcontextprotocol/server-sqlite`
- **MySQL** — `@modelcontextprotocol/server-mysql` (community package, check for the most current option)

You can find these on npm or in the [MCP servers repository](https://github.com/modelcontextprotocol/servers). If your database isn't covered by an existing package, the MCP spec is open and there are templates for building your own.

### Configure Claude Desktop

MCP servers are configured in Claude Desktop's config file. Open it at:

- **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Add your database server to the `mcpServers` section. Here's an example for PostgreSQL:

```json
{
  "mcpServers": {
    "my-database": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "postgresql://username:password@host:port/database_name"
      ]
    }
  }
}
```

For SQLite, point it at a file path instead:

```json
{
  "mcpServers": {
    "my-database": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sqlite",
        "/path/to/your/database.db"
      ]
    }
  }
}
```

Replace the connection details with your own. Save the file and restart Claude Desktop.

### Verify the connection

After restarting, you should see a hammer icon in the Claude Desktop input area indicating MCP tools are available. Click it to confirm your database server is listed.

Start a conversation and ask Claude something simple like "what tables are available in the database?" or "describe the schema." If it returns results, you're connected.

If it doesn't work, check the Claude Desktop logs for errors. Common issues: wrong credentials, the database isn't reachable from your machine, or Node.js isn't installed.

## Usage Tips

**Start conversations by asking Claude to explore the schema.** Before querying, have it look at what tables and columns exist. This grounds the conversation in what's actually available rather than what Claude assumes might be there.

**Be specific about what you want.** "Show me revenue data" will produce something, but "show me monthly revenue by product line for Q3 2025, excluding internal test accounts" gets you something useful on the first try.

**Review queries before trusting results.** Claude will show you the SQL it's running. Glance at it — especially joins and filters. A query that returns results isn't necessarily a query that returns the *right* results.

**Use read-only credentials.** If you're connecting to a production database or anything you don't want accidentally modified, use a database user with read-only access. MCP servers will execute whatever SQL Claude generates, including writes if the credentials allow it.

**Consider a replica or export for heavy exploration.** If you're planning an extended session of data exploration, pointing at a read replica or a recent export avoids any load concerns on your production database.

## Limitations

- MCP servers run locally on your machine. If you can't reach the database from your laptop, Claude can't either.
- Large result sets can hit context limits. If a query returns thousands of rows, ask Claude to aggregate or limit the results in the query itself rather than pulling everything back.
- Claude generates SQL based on the schema it sees and your description. It can write incorrect queries, especially for databases with unusual naming conventions or complex relationships. Always sanity-check the output.
- MCP isn't available in the Claude web interface — Claude Desktop only.

## Security Notes

Your database credentials live in the local config file on your machine. They aren't sent to Anthropic. The MCP server runs locally and connects directly from your machine to the database.

That said, the data Claude sees during a conversation is sent to Anthropic's API as part of the conversation. If your database contains sensitive data, make sure that's acceptable under your organization's data policies. Scoping the database user to only the tables and schemas you want Claude to access is a reasonable precaution.