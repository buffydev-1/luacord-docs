# LuaCord Documentation

  Modern async Lua Discord API library for 2026.
  Spiritual successor to Discordia.

  - GitHub: https://github.com/buffydev-1/luacord
  - LuaRocks: https://luarocks.org/modules/buffydev-1/luacord

  ---

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

  ## Status

  LuaCord is live on GitHub and LuaRocks and actively maintained.

  ## Features

  - Discord API v10 foundation
  - Gateway identify, heartbeat, reconnect, resume
  - Rate-limit-aware REST client
  - Slash commands and interactions
  - Components (buttons, selects, modals, autocomplete)
  - Cache for guilds, channels, members, roles, messages, users

  ## Docs Map

  - Getting Started: setup and first bot
  - Client: lifecycle and events
  - REST: endpoint usage patterns
  - Structures: Guild, Channel, Message, User, Member, Role, Interaction
  - Enums: intents, permissions, interaction/component types
  - Examples: practical snippets