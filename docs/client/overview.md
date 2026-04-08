# Client Overview

  `Client` is the main entry point for LuaCord.
  It handles login, gateway lifecycle, event dispatch, caching, and command helpers.

  ## Create a Client

  ```lua
  local luacord = require("luacord")
  local enums = luacord.enums

  local client = luacord.Client.new({
    intents = enums.GatewayIntentBits.GUILDS
      + enums.GatewayIntentBits.GUILD_MESSAGES
      + enums.GatewayIntentBits.MESSAGE_CONTENT
  })

  ## What Client Does

  - Starts and manages the Discord gateway connection
  - Handles identify, heartbeat, reconnect, and session resume
  - Emits high-level events (ready, messageCreate, interactionCreate, etc.)
  - Stores cache for guilds, channels, users, members, roles, and messages
  - Exposes REST-backed helpers for command registration and guild fetches

  ## Core Methods

  ### Client.new(options)

  Create a new client instance.

  Common options:

  - intents (number): gateway intents bitfield
  - shard (table): shard tuple
  - presence (table): initial presence payload
  - rest (table): RESTClient options
  - logger (function): internal gateway log callback

  ### client:login(token)

  Sets token for REST + gateway and starts the gateway loop task.

  client:login(os.getenv("DISCORD_BOT_TOKEN"))

  ### client:run()

  Runs the cqueues loop (blocking).

  client:run()

  ### client:stop()

  Stops gateway and exits loop on next cycle.

  client:stop()

  ### client:fetchGuild(guildId, withCounts)

  Fetches a guild from REST and caches it.

  local guild, err = client:fetchGuild("123456789012345678", true)

  ### client:createCommand(payload, guildId)

  Creates a global command or a guild command.

  client:createCommand({
    name = "ping",
    description = "Ping command",
    type = luacord.enums.ApplicationCommandType.CHAT_INPUT
  })

  ### client:syncCommands(payload, guildId)

  Bulk overwrites global or guild commands.

  client:syncCommands({
    {
      name = "ping",
      description = "Ping command",
      type = luacord.enums.ApplicationCommandType.CHAT_INPUT
    }
  })

  ## Event Registration

  ### client:on(event, fn)

  Register a listener.

  client:on("ready", function()
    print("Bot is online")
  end)

  ### client:once(event, fn)

  Register a one-time listener.

  ### client:off(event, fn)

  Remove listener (or all listeners for event if fn is omitted).

  ## Cache Layout

  client.cache collections:

  - guilds
  - channels
  - users
  - members
  - roles
  - messages

  Each is a collection with get, set, has, delete, values, and size.

  ## Typical Startup Pattern

  local luacord = require("luacord")
  local enums = luacord.enums

  local client = luacord.Client.new({
    intents = enums.GatewayIntentBits.GUILDS
      + enums.GatewayIntentBits.GUILD_MESSAGES
      + enums.GatewayIntentBits.MESSAGE_CONTENT
  })

  client:on("ready", function()
    print("Ready as " .. client.user:displayName())
  end)

  client:on("messageCreate", function(message)
    if message.author and message.author.bot then return end
    if message.content == "!ping" then
      message:reply("Pong!")
    end
  end)

  client:login(os.getenv("DISCORD_BOT_TOKEN"))
  client:run()