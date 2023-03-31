# Manual pages
Used for help on any command

- To Get help on a command `man <<command_name>>`
- `<<command>> --help` will also useful for getting help
- To find a type of command use `type <<command>>` ex: `type cd`
- for inbuild commands use `help <<inbuild_command>>`
- If command is inbuild `man cd` will not work
- To search in all man files use `man -k "search string"`

## Linux command structure
- General structure is `command option command_argument`, ex: `ping -c 1 8.8.8.8`
-  option with single character will precedes with `-`, long word form with `--`
- Example `ls -a` and `ls --all` will perform the same thing.


General Commands

`date` - to get system time generally utc
`cal` - shows months calendar
`uptime` - total time the machine is up and running
`whoami` - show user

To switch as a root user

```sh
sudo - su
```

`users` - connected user name
`id` - user information
`who` - to get the public ip of a machine
`w` - to get system related info



