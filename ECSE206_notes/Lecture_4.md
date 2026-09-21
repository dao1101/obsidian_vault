### More commands
- `pwd`: print working directory
- `cd`: change directory
- `history`: or search history through `Ctrl+r`
- `exit`/ `logout`
- `Ctrl+c`: force stop programs ==but do not exit==
- `Ctrl+d`: stop input or exit on empty command line

==Notes: ==
- Flags can be combined
	- e.g. `ls -la` = `ls -l -a`
- Can autocomplete with Tab

### Wildcards
A symbol used to replace one or more characters in a filename . In Bash and (POSIX)
- `*.doc`: any pattern
- `?at.doc`: any single char
- `cat.d[aoz]c`: any character within the brackets
	- `[a-d]` = `[abcd]`
	- `[!a]` = any single character except a
- echo
### Filenme expansion (globbing)
The shell recognizes and expands wildcards patterns into the list of pathnames matching the pattern, which is called blocking
- works for every command
```bash
#e.g. type ls in a directory
echo ls *.doc
#shell expands it to
ls john.doc cat.doc
#The shell expands wildcards before giving them as arguments to the commands (the commands themselves don't take wildcards as argument)
#echo prints that out
#If no echo then the shell just expands and then executes ls
```
==Note: `*.txt`does not match `.hiddent.txt` but `.*.txt`does==
If the wildcards can't be matched then the shell won't do anything with them or send and error message. Could cause unexpected results
### Command substitution
The shell can also substitute the outputs of commands
Syntax: `$`(command)
```shell
touch $(date +%Y-%m-%d).txt
#shell first run the date command
#$ replaces the command by the 2026-09-10
#touch creates file 2026-09-10.txt
```
### Redirection
- Standard Streams
	- communication channels between a computer program and its environment when it begins execution
	- STDIN: channel where keys typed by the user are gathered
	- STDOUT: channel where normal application output sent
	- STDERR: channel where error output sent
		- normal output and error output is separated on two different channels

- FIle Descriptors
	- It is an non-negative integer index used by OS kernel to identify an ==open== file or I/O resource for a specific process

		![[Screenshot 2026-09-11 at 13.13.27.png]]

		![[Screenshot 2026-09-11 at 13.19.36.png]]
	==Note: the program her is standard user commands you run inside your terminal session(e.g. grep, cat, ls, or a compiled C program)==

- by default
	- stdin goes from keyboard to program stdout and stderr goes from program to display 
	- but they can be redirected
	
- redirect stdout to a file
	- `>`
	-  e.g. `ls -la > list.txt`
	- variant: append to existing file instead of overwriting
	- `ls -la >> list.txt`
		![[Screenshot 2026-09-11 at 13.21.44.png|477]]

- redirect stdin from a file
	- `<`
	- e.g `my_program < input.txt`
		![[Screenshot 2026-09-11 at 13.39.36.png|475]]

- Connecting stdin/stdout of two programs (Piping)
	- `|` 把一个程序的输出当下一个文件的输入
	- e.g. `ls -l | more`
		![[Screenshot 2026-09-11 at 13.43.29.png|482]]

- Chaining: redirect and piping can be chained together to make complex commands
	- `my_program < input.txt > output.txt`
		![[Screenshot 2026-09-11 at 13.48.58.png|443]]
	- `ls -l | head > output.txt` (head shows the first 10 lines)
		![[Screenshot 2026-09-11 at 13.51.28.png|454]]

e.g. `cat $(ls *.log | tail -n5) >> text.out`
- shell interprets the parenthesis first
	- expands wildcard
	- ls gives back the list of files
	- piped to tail
		- shows the last 10 lines by default, but `-n5` makes it show only last 5 lines
- shell substitutes `$()`by the output of the command
- `cat` concatenates the contents of file and output is directed to text.out

More variant: (no need to memorize)
- redirect stderr to a file: `2>` and `2>>` to append
- redirect stderr to stdout: `2>&1` e.g. `my_program > output.txt 2>&1` 
- redirect to both stdout and a file by piping with tee command
	- `ls -l | tee output.txt`
		- output goes to stdout and output.txt
	- `ls -l | tee -a output.txt`
		- output goes to stdout and is appended at the end of output.txt