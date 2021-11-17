### Summary

`PlayerOperations` is a static class that provides higher level operations for manipulating players (both online and offline)

General guidelines:
- Methods do **not check permissions** - these must be checked separately beforehand
- Most methods return a bool for whether the operation succeeded
- When an operation fails the source player is automatically messaged the reason why

### Static methods

`bool SetLoginMessage(Player p, string target, string value)`

Attempts to change the login message of the destination player

Failure causes:
- Source player is muted

### Examples

