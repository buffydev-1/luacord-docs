 # LuaCord Documentation

  Welcome to the official docs for **LuaCord**.

  LuaCord is a modern async Lua Discord API library and spiritual successor to Discordia.

  - GitHub: https://github.com/buffydev-1/luacord
  - LuaRocks: https://luarocks.org/modules/buffydev-1/luacord

  ## Install

  ```bash
  luarocks install luacord

  ## Quick Start

  local luacord = require("luacord")
  local enums = luacord.enums

  local intents = enums.GatewayIntentBits.GUILDS
    + enums.GatewayIntentBits.GUILD_MESSAGES
    + enums.GatewayIntentBits.MESSAGE_CONTENT

  local client = luacord.Client.new({ intents = intents })

  client:on("ready", function()
    print("Logged in as " .. client.user:displayName())
  end)

  client:on("messageCreate", function(message)
    if message.author and message.author.bot then return end
    if message.content == "!ping" then
      message:reply("Pong!")
    end
  end)

  client:login(os.getenv("DISCORD_BOT_TOKEN"))
  client:run()

  ## What’s Covered

  - Discord API v10 foundation
  - Gateway identify, heartbeat, reconnect, resume
  - Rate-limit-aware REST requests
  - Slash commands and interactions
  - Components (buttons/selects/modals/autocomplete)
  - Caching for guilds, channels, members, roles, messages, users

  ## Docs Map

  - Getting Started: setup, install, first bot
  - Client: lifecycle, login, events
  - REST: endpoint usage patterns
  - Structures: Guild, Channel, Message, User, Member, Role, Interaction
  - Enums: intents, permissions, interaction/component types
  - Examples: practical bot snippets