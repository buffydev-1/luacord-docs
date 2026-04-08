 # Getting Started

  This guide helps you run your first LuaCord bot quickly.

  ## 1) Requirements

  - Lua 5.1, 5.2, or 5.3
  - LuaRocks
  - Discord bot token from the Discord Developer Portal

  ## 2) Install LuaCord

  ```bash
  luarocks install luacord

  ## 3) Create a Bot Script

  Create bot.lua:

  local luacord = require("luacord")
  local enums = luacord.enums

  local intents = enums.GatewayIntentBits.GUILDS
    + enums.GatewayIntentBits.GUILD_MESSAGES
    + enums.GatewayIntentBits.MESSAGE_CONTENT

  local client = luacord.Client.new({
    intents = intents
  })

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

  ## 4) Set Your Token

  PowerShell:

  $env:DISCORD_BOT_TOKEN="YOUR_BOT_TOKEN"

  ## 5) Run the Bot

  lua bot.lua

  ## 6) Invite Bot to Your Server

  In Discord Developer Portal:

  1. Open your application
  2. Go to OAuth2 > URL Generator
  3. Scopes:
      - bot
      - applications.commands (for slash commands)
  4. Bot Permissions (minimum for this example):
      - View Channels
      - Send Messages
      - Read Message History

  Open generated URL and invite bot.

  ## 7) Privileged Intents

  If you use these, enable them in Developer Portal:

  - GUILD_MEMBERS
  - GUILD_PRESENCES
  - MESSAGE_CONTENT

  Then include them in your intents bitfield.

  ## 8) Next Steps

  - Read Client Overview
  - Add slash commands from Examples
  - Explore Structures and Enums