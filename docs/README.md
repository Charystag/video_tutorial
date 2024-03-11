# Video Tutorial

This script allows its user to selectively run a sequence of commands
in order to illustrate a process without having to type all such commands
in a terminal window

# Table of Contents

1.	[How to use this script ?](#How-to-use-this-script-?)
2.	[Why this Script ?](#Why-this-Script-?)

# How to use this script ?

As this Script allows to provide commands and descriptions to show how a given 
process is executed, one needs to provide commands and descriptions to the script
in order to print them.

## A single file that stores the commands and the descriptions (recommended way)

The user can input the commands and the descriptions in a single file that will 
take the form of the following file :
```bash
command 1 | Description 1
command 2
command 3 | Description 3
command 4
@command 5
@command 6
command 7 | Description 7
```

In this example, we can observe that there are 3 ways to run a command in a sequence with 
this script.
1.	command | Description : The command is to be specified alongside the description on the 
same line separated by a separator. The default separator is \`|' but another separator can 
be specified with the option -s separator.

<blockquote>

:bulb: To specify a separator that is an escape sequence (like '\t' for example)<br/>
One can use the special form $'string' (like $'\t') for example, which will ensure the 
translation of the escape sequence by the shell.

You can run bash <(curl -fsSL https://raw.githubusercontent.com/nsainton/man\_reader/master/man\_reader.sh) bash QUOTING

</blockquote>

# Why this Script ?
