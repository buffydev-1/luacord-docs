 # Structures

  LuaCord converts Discord payloads into structure objects with methods and cached state.

  ## Available Structures

  - `Guild`
  - `Channel`
  - `Message`
  - `User`
  - `Member`
  - `Role`
  - `Interaction`

  Most objects are created internally from gateway/REST payloads and cached by `Client`.

  ---

  ## Guild

  Represents a Discord guild (server).

  Common fields:

  - `id`
  - `name`
  - `icon`
  - `owner_id`
  - `features`
  - `member_count`
  - `channels` (collection)
  - `roles` (collection)
  - `members` (collection)

  Common methods:

  - `guild:fetchMember(userId)`
  - `guild:createChannel(payload, reason)`
  - `guild:createRole(payload, reason)`
  - `guild:ban(userId, deleteMessageSeconds, reason)`

  Example:

  ```lua
  local guild = client.cache.guilds:get("123456789012345678")
  if guild then
    guild:createChannel({ name = "new-channel", type = 0 })
  end

  ———

  ## Channel

  Represents a channel or thread.

  Common fields:

  - id
  - type
  - guild_id
  - name
  - topic
  - parent_id
  - thread_metadata

  Common methods:

  - channel:send(contentOrPayload, options)
  - channel:edit(payload, reason)
  - channel:delete(reason)
  - channel:startTyping()
  - channel:createThread(payload, reason)

  Example:

  channel:send("Hello from LuaCord")

  ———

  ## Message

  Represents a message.

  Common fields:

  - id
  - channel_id
  - guild_id
  - author
  - member
  - content
  - embeds
  - attachments
  - reactions
  - poll

  Common methods:

  - message:reply(contentOrPayload, options)
  - message:edit(payloadOrString)
  - message:delete(reason)
  - message:react(emoji)
  - message:pin(reason)
  - message:unpin(reason)

  Example:

  message:reply("Pong!")

  ———

  ## User

  Represents a Discord user.

  Common fields:

  - id
  - username
  - discriminator
  - global_name
  - avatar
  - bot
  - system

  Common methods:

  - user:mention()
  - user:displayName()
  - user:avatarURL(size, extension)

  ———

  ## Member

  Represents a guild member.

  Common fields:

  - guild_id
  - user
  - nick
  - roles
  - joined_at
  - permissions
  - communication_disabled_until

  Common methods:

  - member:id()
  - member:mention()
  - member:displayName()
  - member:avatarURL(size, extension)
  - member:permissionsObject()
  - member:kick(reason)

  ———

  ## Role

  Represents a guild role.

  Common fields:

  - id
  - guild_id
  - name
  - color
  - position
  - permissions
  - mentionable

  Common methods:

  - role:mention()

  ———

  ## Interaction

  Represents an interaction payload (slash, component, modal, autocomplete).

  Common fields:

  - id
  - application_id
  - type
  - data
  - guild_id
  - channel_id
  - token
  - member
  - user

  Common methods:

  - interaction:reply(payloadOrString, responseType)
  - interaction:deferReply(ephemeral)
  - interaction:editReply(payloadOrString)
  - interaction:followUp(payloadOrString)
  - interaction:deleteReply()

  Example:

  interaction:reply({ content = "Handled." })

  ———

  ## Notes

  - Structures are mutable and patched by new payloads.
  - Cache keys are based on Discord IDs.
  - For permission checks, use luacord.utils.Permissions.
  - For constants, use luacord.enums.
