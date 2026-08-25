Vim is a command line editor which is super powerful and typically it or Vi (older version) are installed on most systems by default. As it is command line based, there are no mouse movements which is super useful but also takes some getting used to open Vim you run the vim command followed by the path to the file you want to edit ie `vim /home/n00blyfe/.bashrc`
**_TO EXIT VIM_**:
- press `esc` to get back into normal mode
- press `:` so that you can enter a command mode
- type `q` 
- to exit and discard changes type `q!`
- to exit and save changes type `wq`
at the bottom of the file Vim will display the mode you are in. If nothing is displayed you are in normal mode
`-- INSERT --` mode is for basic editing enter by typing `i` in normal mode. To go back to normal mode press `esc` below is a table of shortcuts

| Key Binding | Description               |
| ----------- | ------------------------- |
| `x`         | cut character             |
| `dw`        | cut word                  |
| `dd`        | cut full line             |
| `yw`        | copy word                 |
| `yy`        | copy full line            |
| `p`         | paste                     |
| `0`         | move to beginning of line |
| `$`         | move to end of line       |
you can multiply any command to run multiple times by adding a number before it. for example `4yw` would copy 4 words instead of one etc
pressing `:` puts us in command mode below are some commands to keep in mind

| Command | Description          |
| ------- | -------------------- |
| `:1`    | go to line number 1  |
| `:w`    | write to file (save) |
| `:q`    | quit                 |
| `:q!`   | quit without saving  |
| `:wq`   | write and quit       |
[Cheatsheet](https://vimsheet.com)
