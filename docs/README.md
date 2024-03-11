# Video Tutorial

> :fr: French documentation available [here](/docs/README.fr.md)

This script allows its user to selectively run a sequence of commands
in order to illustrate a process without having to type all such commands
in a terminal window

# Table of Contents

1.	[How to use this script ?](#how-to-use-this-script-)
2.	[Why this Script ?](#why-this-Script-)
3.	[Technical Considerations](#Technical-Considerations)
4.	[Contributing](#Contributing)
5.	[Demo Video](#Demo-Video)

# How to use this script ?

As this Script allows to provide commands and descriptions to show how a given 
process is executed, one needs to provide commands and descriptions to the script
in order to print them.

## Invocation

There are two ways to run this script : 
1.	You can run the script running the following command :
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/nsainton/video_tutorial/master/video.sh)
```
which will allow you to run the script with its arguments but without any installation required.

2.	You can install the script in the required location by replacing the path "$HOME/.local/bin/video.sh" by the path 
to the file you want to install the script in. This command line will also add the target directory to the path

```bash
if [ ! -f "$HOME/.local/bin/video.sh" ]
	then curl -fsSL --connect-timeout 10 https://raw.githubusercontent.com/nsainton/video_tutorial/master/video.sh -o "$HOME/.local/bin/video.sh" \
	&& { if { echo "$PATH" | grep "$HOME/.local/bin" ; }
		then echo "PATH=\"$HOME/.local/bin:$PATH\"" >> "$HOME/.$(basename $SHELL)rc"; echo "Path : \`$HOME/.local/bin added to path'" ; . "$HOME/.$(basename $SHELL)rc" ; fi ; } \
	&& echo "Script installed at : $HOME/.local/bin/video.sh"
else
	echo "Script already installed at : $HOME/.local/bin/video.sh"
fi
```

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

2.	command : The command will be printed and run but without any descriptive message
3.	@command : The command will be run without being printed (useful for configuration/cleanup commands)

An example of the configuration with the single file for commands and descriptions is available 
[here](/tests_commands/commands_and_descriptions.txt)

> :bulb: To test this file you can run : `./video.sh commands_file`

## Commands and descriptions splitted in two files

The user can input the commands and descriptions in two distincts files that will take the 
form of the followings : 

The file : 
```bash
command 1
command 2
command 3
@command 4
@command 5
command 6
@command 7
```
for the commands.

And the file : 
```bash


description 3


description 6
```
for the descriptions

Here is an example of a [commands file](/tests_commands/commands.txt) and a [descriptions file](/tests_commands/descriptions.txt) one could 
use to run the Script with.<br/>

> :bulb: To test these files you can run : `./video.sh commands_file descriptions_file`


> :warning: The only requirement here is that the row index of the description has to match the row index of the command it describes.
> For example : if one was to describe only the 3rd command in a script, they would have to create a description file with 
> all rows empty instead of the 3rd one which will contain the description of the 3rd command.

# Why this Script ?

This Script came to life because I wanted to be able to execute a sequence of commands in order to demonstrate how my other scripts worked.<br/>
I couldn't bear having to manually write (with mistakes and corrections) the commands to my terminal window in order to showcase how a given 
script works.

## Why is it useful and what problems does it solve ?

The video script solves the problem of needing to manually write the commands in order to make any demonstration/presentation. <br/>
It empowers the user to run any script (even a script that needs to read from the command line) in order to focus only on what matters, which is 
providing explanations about how the script works.

# Technical Considerations

This script uses file descriptors 6 and 7 to read input (from either files or the command line) so it doesn't conflict with any script that reads 
from standard input or any file descriptor that is not 6 or 7.

# Contributing
There are two ways to contribute to this project
- Send me a message on discord (for 42 students) or to the following [email](mailto:nsainton@student.42.fr?subject=[video_tutorial])
- Pull requests that are currently closed but are going to be oppened soon for you to add all your amazing features to the project

# Demo Video

Click on the picture to open the video on youtube

