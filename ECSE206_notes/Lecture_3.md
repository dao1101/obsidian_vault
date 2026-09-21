### Shell

Shell is a program that provides users access to the system on which it runs
- e.g. bash (most common linux shell), zsh, PowerShell

### Command-line interface

e.g. `dwang8@taeach-node-02:~$ rm -rf hw1`
- `username@hostname`
- `$` indicates the end of prompt and the start of the user input
- Command: rm
- Flag: -rf; also called switches or options, modifies behaviour of the command
- Argument: input passed to command

```bash
dwang8@teach-node-02:~$ pwd
/home/2026/dwang8
dwang8@teach-node-02:~$ echo hellow
hellow
dwang8@teach-node-02:~$ echo ~
/home/2026/dwang8
dwang8@teach-node-02:~$ echo ..
..
```

### Unix file and directories

Directories are simply a special type of file that contains a list of index nodes (inodes)

Unix does not impost any file format to regular files. Their structure and the way to interpret them is entirely dependent on the software using them.
- file extensions mean nothing and are only useful for the user. ==different from Windows==

Path
	- special symbols: ~(home automatically logged in), /(root), .(current), ..(parent)
#### File manipulation Commands
==man(in front of a command): open commands manual==
- `ls`: sort alphabetically by default
		- syntax: `ls [OPTION]... [FILE]...`
		- common flags: 
			- -l: see contents in long format
				- ![[Screenshot 2026-09-09 at 19.36.19.png|488]]
			- -a: show hidden file
		- if use it on files, you will see **more information about the file**

- `mkdir`: make directories if they do not already exist
		- syntax: `mkdir [OPTION]... DIRECTORY...`

- `touch`: make an empty file
		- the original purpose of touch is to update a file timestamp, but a side-effect is that it creates the file if it does not exist, which became its most common use
		- syntax: `touch [OPTION] FILE`

- `rm`:
	- `rm [options] file1 file2 ...`
	- There is no way for to recover files(also true when overwriting with cp and mv)

- `mv`: move files or directories
		- syntax:
			- `mv [OPTION] SOURCE DEST`
			- `mv [OPTION] SOURCE... DIRECTORY`
			- if the last argument is directory, it moves, otherwise it moves and rename the file/directory 

- `cp`
		1. `cp [options] source destination`
		2. `cp [options] source1 source2 ...dreictory` *copy multiple files at the same time*
		3. If the target is a directory, this is usage 2 and the file(s) will be copied inside of it. Otherwise, this is usage 1 and the file will be copied as destination(created a new copie)

*Options for cp, mv, and rm:*
- -i (cp, mv, rm): interactive, prompt and wait for confirmation before proceeding
- -r or -R (cp, rm): recursive, recursively visiting the files and subdirectories beneath it.
- -f (mv, rm): don’t prompt for confirmation (overrides -i if placed after