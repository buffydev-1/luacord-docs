# Enums

  LuaCord exposes Discord constants through:

  ```lua
  local enums = require("luacord").enums

  Use these values to avoid hardcoded numbers in your bot code.

  ## ChannelType

  enums.ChannelType

  Common values:

  - GUILD_TEXT
  - DM
  - GUILD_VOICE
  - GUILD_CATEGORY
  - GUILD_ANNOUNCEMENT
  - ANNOUNCEMENT_THREAD
  - PUBLIC_THREAD
  - PRIVATE_THREAD
  - GUILD_STAGE_VOICE
  - GUILD_FORUM
  - GUILD_MEDIA

  Example:

  if channel.type == enums.ChannelType.GUILD_TEXT then
    -- text channel logic
  end

  ## GatewayIntentBits

  enums.GatewayIntentBits

  Common values:

  - GUILDS
  - GUILD_MEMBERS (privileged)
  - GUILD_PRESENCES (privileged)
  - GUILD_MESSAGES
  - MESSAGE_CONTENT (privileged)
  - DIRECT_MESSAGES
  - GUILD_VOICE_STATES
  - GUILD_SCHEDULED_EVENTS

  Example:

  local intents = enums.GatewayIntentBits.GUILDS
    + enums.GatewayIntentBits.GUILD_MESSAGES
    + enums.GatewayIntentBits.MESSAGE_CONTENT

  ## GatewayOpcode

  enums.GatewayOpcode

  Key opcodes:

  - DISPATCH
  - HEARTBEAT
  - IDENTIFY
  - RESUME
  - RECONNECT
  - INVALID_SESSION
  - HELLO
  - HEARTBEAT_ACK

  ## InteractionType

  enums.InteractionType

  Values:

  - PING
  - APPLICATION_COMMAND
  - MESSAGE_COMPONENT
  - APPLICATION_COMMAND_AUTOCOMPLETE
  - MODAL_SUBMIT

  Example:

  if interaction.type == enums.InteractionType.APPLICATION_COMMAND then
    -- command logic
  end

  ## ApplicationCommandType

  enums.ApplicationCommandType

  Values:

  - CHAT_INPUT
  - USER
  - MESSAGE

  ## InteractionResponseType

  enums.InteractionResponseType

  Common values:

  - PONG
  - CHANNEL_MESSAGE_WITH_SOURCE
  - DEFERRED_CHANNEL_MESSAGE_WITH_SOURCE
  - DEFERRED_UPDATE_MESSAGE
  - UPDATE_MESSAGE
  - APPLICATION_COMMAND_AUTOCOMPLETE_RESULT
  - MODAL

  ## ComponentType

  enums.ComponentType

  Values:

  - ACTION_ROW
  - BUTTON
  - STRING_SELECT
  - TEXT_INPUT
  - USER_SELECT
  - ROLE_SELECT
  - MENTIONABLE_SELECT
  - CHANNEL_SELECT

  ## ButtonStyle

  enums.ButtonStyle

  Values:

  - PRIMARY
  - SECONDARY
  - SUCCESS
  - DANGER
  - LINK
  - PREMIUM

  ## TextInputStyle

  enums.TextInputStyle

  Values:

  - SHORT
  - PARAGRAPH

  ## MessageType

  enums.MessageType

  Contains Discord message system types like:

  - DEFAULT
  - REPLY
  - CHAT_INPUT_COMMAND
  - CONTEXT_MENU_COMMAND
  - THREAD_CREATED
  - ROLE_SUBSCRIPTION_PURCHASE

  ## PermissionFlagsBits

  enums.PermissionFlagsBits

  Bit flags for permission math. Common flags:

  - VIEW_CHANNEL
  - SEND_MESSAGES
  - MANAGE_MESSAGES
  - MANAGE_CHANNELS
  - MANAGE_ROLES
  - KICK_MEMBERS
  - BAN_MEMBERS
  - ADMINISTRATOR
  - MANAGE_EVENTS
  - MANAGE_THREADS
  - SEND_MESSAGES_IN_THREADS
  - SEND_POLLS

  Example with Permissions helper:

  local luacord = require("luacord")
  local perms = luacord.utils.Permissions.new(member.permissions)

  if perms:has(luacord.enums.PermissionFlagsBits.MANAGE_MESSAGES) then
    -- moderator logic
  end

  ## Notes

  - Enum values are numeric constants that mirror Discord API values.
  - Prefer enums over raw numbers for readability and future maintenance.