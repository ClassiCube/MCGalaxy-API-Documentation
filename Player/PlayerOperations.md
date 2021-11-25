### Summary

`PlayerOperations` is a static class that provides higher level operations for manipulating players (both online and offline)

General guidelines:
- Methods do **not check permissions** - these must be checked separately beforehand
- Most methods return a bool for whether the operation succeeded
- When an operation fails, the source player is automatically messaged the reason why
- If an empty string is provided for value argument, the related state will be reset to default for destination player

### Static methods

##### SetLoginMessage

`bool SetLoginMessage(Player p, string target, string message)`

Attempts to change the login message of the destination player

Return value
- true if changing login message succeeded, false if failed

Failure causes:
- Source player is muted

#### SetLogoutMessage

`bool SetLogoutMessage(Player p, string target, string message)`

Attempts to change the logout message of the destination player

Failure causes;
- Source player is muted

#### SetNick

`bool SetNick(Player p, string target, string nick)`

Attempts to change the nickname (name that appears in chat) of the destination player

Failure causes:
- Source player is muted
- Nickname is over 30 characters long

#### SetTitle

`bool SetTitle(Player p, string target, string title)`

Attempts to change the title (what appears in the [] before name in chat) of the destination player

Failure causes:
- Source player is muted
- Title is over 20 characters long

#### SetTitleColor

`bool SetTitleColor(Player p, string target, string color)`

Attempts to change the color of the title of the destination player

Failure causes:
- Source player is muted

#### SetColor

`bool SetColor(Player p, string target, string color)`

Attempts to change the color of the destination player (e.g. name color in chat, color in tablist, etc)

Failure causes:
- Source player is muted

### Examples

