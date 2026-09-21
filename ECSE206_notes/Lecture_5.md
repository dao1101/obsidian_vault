### Vim
- Powerful text editor to write text from terminal
- Modal editor: keys have different functions depending on current mode
	- modes
		- insert
			- to edit
		- normal
			- used as commands
			- move around in the file, change modes, copy, undo, etc.
		- cmdl mode
			- save, load, quit, search etc.
		- visual
- Commands
- Insert mode:
	• To get in insert mode, any of the following: i, I, a, A, o, O
		• i – insert text before the cursor | I – insert at start of line before first non-blank
		• a – append text after the cursor | A – append text at the end of the line
		• o – begin a new line below the cursor and insert text | O – same but above cursor
- Normal mode:
	• To get to to normal mode: Esc key
	• To move:
		• h, j, k, l to move left, down, up, right
		• (arrows also work but not recommended)
		• gg – go to first line | G – go to last line
		• many others like w to go to next word, ( to go to next unmatched (, etc.)
	• To delete: dd, D, x, r
		• dd – delete a line | D – delete the rest of the line
		• x – delete a character | r – replace a character
	• To copy (yank) and paste a line:
		• yy or Y (equivalent) – yank | p - paste before cursor | P – paste after cursor
	• To undo and redo:
		• u (undo) and ctrl-r (redo
- Command-line mode:
	• w, q, wq, q!, line number, e filename
		• :w – save file | :q – quit current window | :wq save and quit | :q! quit and discard changes
		• :number – go to a specific line number (For example, :14)
		• :e filename – Edit a file
	• To search: / (forward), ? (backwards)
		• Once you press enter, press n and N to get next/previous
- For help:
	- :help

### Permission
*Recall:*
![[Screenshot 2026-09-15 at 15.39.05.png]]
- All files owned by a user and a group.
	- usually, this owner is the user that created the file
- permissions on files exists at three level
	- use, group and others
- three types of permission
	- read, write and execute
	 ![[Screenshot 2026-09-15 at 15.37.21.png|233]]

#### chmod command
- change file permissions
	- can be used by owner or superuser(root)
- who
	- u, g, o*thers*
	- a: all above
- changes to
	- =: become
	- +: add
	- -: remove
- examples:
	- remove all permissions from others
		- `chmod o= file3.txt`
	- read only to user and execute only to group
		- `chmod u=r,g=x` ==no space after comma==

#### Binary representations of permissions

From the binary, **octal representations**
- e.g. 111 000 110 --> 706