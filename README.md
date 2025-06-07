Bring a model context protocol server (MCP) in action, and explain:

- Generate a MCP server from Postman
- Deploy the server
- Test the server in Cursor (LLM orchestrator)

The MCP server in this example connects to the OpenWeather API:

- [Generate server](#generate-server)
  - [Install Postman](#install-postman)
  - [Start Postman](#start-postman)
  - [Generate](#generate)
- [Build server](#build-server)
- [Run server](#run-server)
  - [Start](#start)
  - [Configure](#configure)
  - [Restart](#restart)
- [Test server](#test-server)
  - [Install orchestrator](#install-orchestrator)
  - [Configure](#configure-1)
  - [Test](#test)
- [Design](#design)
  - [Development](#development)
  - [Deployment](#deployment)
  - [Runtime](#runtime)
- [Credits](#credits)

# Generate server

Generate an MCP server by using Postman as a tool.

## Install Postman

    sudo snap install postman

## Start Postman

    postman

Login with an account > free plan.

## Generate

In Postman:

- API network > MCP Generator
- Search > Openweathermap (by API Evangelist)
- Select APIs > Add Requests
- Generate
- Download ZIP
- Unzip ZIP

The selected API-requests are "tools" that an LLM can use.

# Build server

Build the MCP server.

In src:

    npm install

# Run server

Start the MCP server and add an API key to access the underlying API.

## Start

    node mcpServer.js

## Configure

Extend the MCP server with an API key, in order to access the underlying API.

- In this example, we use the OpenWeather API

In OpenWeather:

- Create an account or sign-in
- Copy the API key
- https://openweathermap.org/api

In src/.env (not checked in):

- OPENWEATHERMAP_API_KEY=your_copied_key

## Restart

    node mcpServer.js

# Test server

Test the MCP server in an LLM orchestrator (Cursor).

## Install orchestrator

Install Cursor:

https://www.cursor.com/

Observe preconfigured models:

- Cursor settings > Models

## Configure

Add MCP server to LLM orchestrator.

- The configured LLMs will receive the MCP server as context

In this example, we use Cursor as LLM orchestrator (for testing purposes)

- In Cursor, select Cursor Settings > MCP tools > New MCP Server
- Add args: "your-dir/mcpServer.js" (where you unzipped the mcpServer)

Observe a green dot, indicating that the MCP-server is ready to use.

- Sometimes selecting the disable/enable switch is required

## Test

Ask a question to the models:

- Ctrl-I > "What's the wheather in Amsterdam" > Accept

Based on the question, the LLM internally reasons and decides which tool to use in order to produce an answer.

![](./Result.png)

# Design

## Development

![](./Development.svg)

## Deployment

![](./Deployment.svg)

## Runtime

![](./Runtime.svg)

# Credits

- https://javascript.plainenglish.io/i-stopped-building-frontends-now-i-use-mcp-servers-to-let-ai-run-my-apps-178b0d7107ca
