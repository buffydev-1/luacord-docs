 # Examples

  Practical LuaCord examples you can copy into your bot.

  ## 1) Basic Ping Command (Prefix)

  ```lua
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

  ## 2) Slash Command Registration

  local luacord = require("luacord")
  local enums = luacord.enums

  local client = luacord.Client.new({
    intents = enums.GatewayIntentBits.GUILDS
  })

  client:on("ready", function()
    local ok, err = client:createCommand({
      name = "ping",
      description = "Check bot latency",
      type = enums.ApplicationCommandType.CHAT_INPUT
    })

    if not ok then
      print("Failed to create command:", err and err.message or err)
    else
      print("Slash command registered")
    end
  end)

  client:login(os.getenv("DISCORD_BOT_TOKEN"))
  client:run()

  ## 3) Slash Command Handling

  local luacord = require("luacord")
  local enums = luacord.enums

  local client = luacord.Client.new({
    intents = enums.GatewayIntentBits.GUILDS
  })

  client:on("interactionCreate", function(interaction)
    if interaction.type ~= enums.InteractionType.APPLICATION_COMMAND then return end
    if not interaction.data or interaction.data.name ~= "ping" then return end

    local ok, err = interaction:reply({
      content = "Pong from slash command!"
    })

    if not ok then
      print("Reply failed:", err and err.message or err)
    end
  end)

  client:login(os.getenv("DISCORD_BOT_TOKEN"))
  client:run()

  ## 4) Deferred Interaction Reply

  client:on("interactionCreate", function(interaction)
    if interaction.type ~= enums.InteractionType.APPLICATION_COMMAND then return end
    if interaction.data.name ~= "heavy" then return end

    interaction:deferReply(true) -- ephemeral defer

    -- do heavy work here...

    interaction:editReply({
      content = "Done processing."
    })
  end)

  ## 5) Send Message to a Channel by ID

  local channel = client.cache.channels:get("123456789012345678")
  if channel then
    channel:send("Hello from LuaCord")
  end

  ## 6) Edit and Delete a Message

  client:on("messageCreate", function(message)
    if message.author and message.author.bot then return end
    if message.content ~= "!editme" then return end

    local reply = message:reply("Temporary text")
    if reply then
      reply:edit("Edited text")
      -- reply:delete()
    end
  end)

  ## 7) Role/Permission Check

  local perms = require("luacord").utils.Permissions
  local enums = require("luacord").enums

  client:on("interactionCreate", function(interaction)
    if not interaction.member then return end

    local p = perms.new(interaction.member.permissions or 0)
    if not p:has(enums.PermissionFlagsBits.MANAGE_MESSAGES) then
      interaction:reply({ content = "Missing permission.", flags = 64 })
      return
    end

    interaction:reply("You have permission.")
  end)

  ## 8) Global Error Listener

  client:on("error", function(err, eventName)
    print("Error in event:", eventName or "unknown")
    print(tostring(err))
  end)

  ## Environment Variable

  Set your token once and keep it out of source code.

  PowerShell:

  $env:DISCORD_BOT_TOKEN="YOUR_TOKEN_HERE"

  Then run your bot script.
