### More on Linux

#### quiet (option of grep)
- If you don't want to see the output of a command on the screen 
```bash
grep -q

ls > /dev/null 2 > /dev/null #redirect stdout and stderr to devnull
#or
ls > /dev/null 2>&1 #redirect stdout to devnull and stderr to stdout

```

#### Environment variable
- contains information about your login session 
	- `$HOME`
	- `$PATH`
	- `$PS1`: prompt string1, the content of primary command-line prompt
			- e.g. `dwang8@teach-node-05:~$`
- can be edited like any other variables
	- `export $PATH="$PATH:~/my_dir"` this adds ~/my_dir to $PATH
	- modifications only visible int that particular session, once logged out and open a new terminal changes won't be seen
	- 若想效果一直保留，必须写入配置文件


#### System script
- System configuration purpose
	- `~/.bash_profile`: executed once when log in bash shell
	- `~/.bashrc`: runs every time you open a new terminal window
	- Add `export PS1="[\t]\u@\h:\w\$"` to`~/.bash_profile`
		- make your prompt permanently show the current 24-hour time(\t), username (`\u`), host (`\h`), and directory (`\w`) every time you log in.

| **File**              | **When it runs**                                                                      | **Primary Use Case**                                                                   |
| --------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **`~/.bash_profile`** | **Login shells** (executed once when you first log in, e.g., via SSH or server login) | settings that only need to be initialized once per overall login session               |
| **`~/.bashrc`**       | **Non-login shells** (executed every time you open a new terminal tab/window)         | Interactive terminal settings, aliases, custom functions, and prompt designs (`$PS1`). |
#### Alias 别名
- give an alternate name to commands
- syntax: `alias NEWNAME=OLDXPRESSION`
	- `alias dir='ls -l -a'` 
	- 设置包含空格或多个参数的命令别名时，**必须使用引号将原表达式包裹起来**


#### Tar
- archive: a collection of files combined into one file.
- two most common archive tools: `tar` and `gzip`
	- .tar and .tgz(compressed tar)
- switches (like options but with no argument)
	- -c: create
	- -r: update tar archive
	- -x: extract
	- -f: specifies file name
	- -v: verbose mode(冗长) used to outputs information
	- -z: zip

#### diff
- shows the difference between two files
- syntax:  `diff [options] file1 file2`

#### hard and symbolic links
- `ln` and `ln -s`
- used to create links to files and folders
	- hard: ln /path/file link_name
	- soft: ln -s /path/file link_name

- **硬链接：** 多个人共享**同一个 inode（索引节点）**，节点连接着数据。删一个名字，节点还在。
    
- **软链接：** 自己有**独立的 inode（索引节点）**，但节点里的内容是“指向别人的地址”。源文件（目标节点）没了，它的地址就失效了