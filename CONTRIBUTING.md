# Contributing

This plugin uses the [Agent Plugins 1.0](https://agent-plugins.org/) format: `plugin.json` and `mcp.json` at the root.

## Local setup

**Visual Studio Code**

1. Clone this repository.
2. Open your user settings JSON (**Preferences: Open User Settings (JSON)**) and add the repository's absolute path, with forward slashes:

   ```json
   "chat.plugins.enabled": true,
   "chat.pluginLocations": {
     "C:/path/to/play-copilot-plugin": true
   }
   ```

   Adding the folder to `chat.plugins.marketplaces` only registers it as a marketplace. It does not load the plugin.
3. Run **Developer: Reload Window**. Settings changes do not load the plugin into a window that is already open.
4. Run `/plugin list` in Copilot Chat and check that `leapwork-play` is listed.
5. Switch the chat to **Agent** mode. Ask mode runs no tools, so no MCP server starts.
6. Ask for Leapwork Play by name, for example "Use Leapwork Play to create an asset of type test-case named Login smoke", and sign in when asked. Copilot sends requests such as "create a testcase" to its built-in `/tests` command, which answers "To generate tests, open a file and select code to test." If that happens, reference a Leapwork Play tool with `#` in the message, such as `#play_get_skill`.

**Copilot CLI**

```bash
copilot plugin marketplace add ./play-copilot-plugin
copilot plugin install leapwork-play@leapwork
```

## Troubleshooting

- **No tools run**: the saved chat in `%APPDATA%\Code\User\workspaceStorage\<id>\chatSessions\` shows the mode (`"mode":{"id":"ask"}`), the command Copilot chose (`"command":"tests"`) and the MCP servers it started (`"didStartServerIds":[]`).
- **The agent calls another Leapwork server**: turn off other Leapwork Play MCP servers (dev, QA or localhost) while testing. They expose the same tool names as the plugin's `play` server.

## Notes

- `README.md` is the plugin's page for users, so keep it written for them.
- Keep `plugin.json` to the fields in the Agent Plugins schema. Other fields are reported and ignored.
