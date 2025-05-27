# Google Calendar MCP Server

[日本語のREADMEはこちら](README.ja.md)

> This branch (change_to_sse) is a fork of the "Google Calendar MCP Server" in [this repository](https://github.com/101ta28/google-calendar-mcp-server), with customizations that change the transport specification from Stdio to SSE and simplify functionality.

This document explains the steps to set up the environment to use the Google Calendar API to search calendar contents as an MCP server.

## Prerequisites

- [uv](https://github.com/astral-sh/uv) must be installed.
- A Google account.

## Steps

### 1. Create a Google Cloud Project

Enable the Google Calendar API in the Google Cloud Console or via the link below.

[Enable API](https://console.cloud.google.com/flows/enableapi?apiid=calendar-json.googleapis.com&hl=en)

### 2. Set Up the OAuth 2.0 Consent Screen

Navigate to the branding page in the Google Cloud Console menu or via the link below.

[Branding](https://console.cloud.google.com/auth/branding?hl=en)

1. Set the application name.
2. Set the user support email.
3. Select "External" as the available users.
4. Set the developer contact information.

### 3. Set Up Desktop Application Credentials

Navigate to the client page in the Google Cloud Console menu or via the link below.

[Client](https://console.cloud.google.com/auth/clients?hl=en)

1. Click **Create Credentials**.
2. Click Desktop app under Application type.
3. Enter a name for the credentials in the Name field.
4. Click Create.
5. Save the downloaded JSON file as `credentials.json` and move the file to your working directory.

### 4. Create a test user

Navigate to the audience page in the Google Cloud Console menu or via the link below.

[Audience](https://console.cloud.google.com/auth/audience?hl=en)

1. Click **Add User** to add a test user (your account name).

### 5. Set Up the Python Environment

#### Create a Virtual Environment

1. Open a terminal or command prompt.
2. Navigate to your project directory.
3. Set up the virtual environment and download the required libraries.

   ```sh
   uv sync
   ```

#### Generate `token.json`

1. Run the following command to generate the `token.json` file:

   ```sh
   uv run generate_token.py
   ```

2. A browser will open requesting permission to access your Google account. Grant the permission.
3. After the authentication is completed, the `token.json` file will be created in your project directory.

#### Start the MCP server

1. Run the following command to start the MCP server：

   ```sh
   uv run main.py
   ```

### Troubleshooting

- **If an error occurs**: Check the error message and, if necessary, reinstall dependencies or check the settings in the Google Cloud Console.
