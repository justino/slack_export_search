# Slack Export Search

This is a basic CLI tool for searching through the Slack Export dump.

## Purpose

I had a need to look through an export for legal discovery and couldn't find a tool I liked. So I spent a very small amount of time and whipped this up. It's not perfect by any stretch, but it solved my need.

## Future Updates

I'll probably add features to this as the need arrises. If you find it useful and want to add more features, by all means, fork and send a pull request.

## Warranty 

Provided as is.

It's full of bugs and does little to no checking to see if it can or should do things.
It will die horribly if it comes across something it doesn't know what to do with.
There is basically no security built into it either so...

Use at your own risk.

# Installation

This is a standalone script written in NodeJS.

Put it somewhere in your `PATH`, or call it direct with full pathname.

Tested with NodeJS v11.3.0

# Basic Usage

1. Unzip Slack Export into it's own directory
2. Descend into the export directory
3. Run this tool

Pretty simple

# Output

All output is to STDOUT

IRC Style output is meant to be opened in something else with a ctrl+f find.

# CLI Usage

```
slack_export_tool <command> [args]
```

## Commands

#### `list_users`

Takes no arguments. Outputs a TSV of id, user, name, email

Example
```
U123456AB        user1        Cool Person        coolperson@example.com
U234567CD        user2        New Person         newperson@example.com
U345678EF        dumbo        Dumb Person        dumbperson@example.com
```

#### `user_conversation`

This command takes a user (see `list_users` above) arg. It will find all conversations that user has made with anyone. If that person was part of a channel with a billion messages sent within the export time frame, then all billion messages will be output.

It doesn't try to put context around anything, you get everything for you to put context around.

Output will be in IRC style (see `IRC Style Example` below).

#### `conversation_grep`

This command takes a keyword arg. It will find all conversations that included that keyword.

Output will be in IRC style (see `IRC Style Example` below).

# IRC Style Example

```
****************************************************
***** Private Channel: email_marketing
***** Between: @user1, @user2, @dumbo
****************************************************
01/01/2019 08:00:00: @user1: hey everyone, i'm new around here
01/01/2019 08:00:34: @user2: hey @user1, welcome, be careful what you say around here, we log everything
01/01/2019 08:01:12: @user1: wow, god to know, thx
        (edited by @user1: wow, good to know, thanks)
01/02/2019 23:10:13: @dumbo: my password is `socrackable`
        (deleted by @dumbo)
****************************************************
***** Private Direct Message
***** Between: @user1, @user2
****************************************************
01/03/2019 08:45:00: @user2: wow, did you see what happened?
01/03/2019 08:46:12: @user1: hmm, no, didnt see it, what was it?
        (edited by @user1: hmm, no, didn't see it, what was it?)
01/03/2019 08:46:44: @user2: yeah, they deleted it, it was `socrackable` can you believe it?
        (edited by @user2: i saw it, but i shouldn't say what it was)
01/03/2019 08:47:12: @user1: yeah, smart, this place is watching you
```
