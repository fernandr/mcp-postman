Bring a model context protocol (MCP) server in action, and explain:

- Generate a MCP server from Postman
- Deploy the server
- Test the server in Cursor (LLM orchestrator)

The MCP server connects to the OpenWeather API.

Credits:

- https://javascript.plainenglish.io/i-stopped-building-frontends-now-i-use-mcp-servers-to-let-ai-run-my-apps-178b0d7107ca

Actions as follows.

# Install cursor IDE

https://www.cursor.com/

# Install Postman

    sudo snap install postman

# Start Postman

    postman

Login with an account > free plan.

# Generate MCP server

In Postman:

- API network > MCP Generator
- Search > Openweathermap (by API Evangelist)
- Select APIs > Add Requests
- Generate
- Download ZIP
- Unzip ZIP

The selected API-requests are "tools" that an LLM can use.

# Build MCP server

In src:

    npm install

# Run MCP server

    node mcpServer.js

# Extend MCP server with API key

The MCP server requires an API key to access the underlying API.

- In this example, we use the OpenWeather API

In OpenWeather:

- Create an account or sign-in
- Copy the API key
- https://openweathermap.org/api

In src/.env (not checked in):

- OPENWEATHERMAP_API_KEY=your_copied_key

Restart server:

    node mcpServer.js

# Configure LLM orchestrator

Add MCP server to LLM orchestrator.

- The configured LLMs will receive the MCP server as context

In this example, we use Cursor as LLM orchestrator (for testing purposes)

- In Cursor, select Cursor Settings > MCP tools > New MCP Server
- Add args: "your-dir/mcpServer.js" (where you unzipped the mcpServer)

Observe a green dot, indicating that the MCP-server is ready to use.

- Sometimes selecting the disable/enable switch is required

# Test agent

In cursor, observe models:

- Cursor settings > Models

Ask a question to the models:

- Ctrl-I > "What's the wheather in Amsterdam" > Accept

Based on the question, the LLM reasons and decides which tool to use in order to produce an answer.

![](./Result.png)

# Design

## Development

![](./Development.svg)

## Deployment

![](./Deployment.svg)

## Runtime

![](./Runtime.svg)
