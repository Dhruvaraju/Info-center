## Terminal short cuts

`ctrl+l` instead of clean command
`ctrl+d` for exiting terminal
`ctrl+a` to move cursor to start of line
`ctrl+e` to move to the end of the file
up arrow to see history of commands, similarly down arrow as well.
`ctrl+u` will remove all the characters before the cursor in the current line.
`ctrl+c` to interrupt a command which is running currently running
`ctrl+z` will stop a command and put it to background which can be resumed later.
`bg %1` will retrieve the last task that is suspended

## Bash Command history

- The commands that are run will be stored in a file `.bash_history` under root folder of a user.
- The number of commands that will be stored will be identified by an environment variable `HISTFILESIZE`
- to print variables `echo $<variable name>`, example `echo $HISTFILESIZE`
- All history commands can be printed by running `history` in terminal.
- `HISTSIZE` environment variable will have the number of commands that can be stored in history
- To run a command from history use `!<history-number>` example `!17`
- use `!!` to run the last run command
- `!-<number>` will run the last executed command based on the number. Example `!-3` will run the command that is executed 3 commands before.
- `!<command_name>` will run the last execution of the command provided example `!cat` will run the last cat command that is run.
- `!<command:p>` will print the last execution of the command provided to console without running it. example `!ping:p` will print the last ping command that is used.
- `ctrl+p` or up arrow to check previous commands
- `ctrl+n` or down arrow to traverse next commands
- `ctrl+r` for searching the bash history (`ctrl+r` and start typing the command to search for it) press enter or `ctrl+p` to execute it or `ctrl+g` to leave search and clear.
- To delete a command from command history use `history -d <line-number>` eg: `history -d 10`
- To delete complete history `history -c`