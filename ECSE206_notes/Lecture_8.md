Reserved words
- The recognition shall only occur when none of the characters is quoted and when the word is used as
	- first word of a command
	- the first word following the reserved word other than case, for, in
	- `in`: third word in `case`
	-  `in`, `do`: the third word in `for`
![[Screenshot 2026-09-24 at 21.02.01.png]]

#### `read`
- the scripts stdin is connected to the terminal
eg.
```bash
echo "how old are you?"
read -r age 
echo "you are $age years old"
```
by using a pipe, we can fee the output of a command to such a while loop, enabling us to loop over the lines of output produced by a program
```bash
ls | while read -r file; do
#the flag meaning read **without escape** the next line input from the output of `ls` and store in variable file
#since some input may contain backlashes
	if [ -d "$file" ]; then
		echo "Is a directory: $file"
	else
		echo "Is not a directory: $file"
	fi
done
```

This program asks the user if hey want to proceed before either doing the thing or exiting
```bash
read -p "Are you sure? [y/N] " -r answer
#-p let the prompt show directly instead of doing a separate echo
#-r可有可无
if [ "$answer" != "y" ]; then
	exit 0
fi
```

shift example
```bash
while [ $# -gt 0 ]; do
	echo "$1"
	shift # shift $2 up and so on
		  # it will also remove the argument everytime
done
```

Short-circuiting
```bash
# && and || used to chain conditions
if [ -f file1 ] && [ -f file2 ]; then
	echo "file1 and file2 exist"
else
	echo "missing file1 or file2"
```
Evaluating arithmetic expressions
```bash
echo $((5+3))

result=$(($1+$2)) #if the strings are not valid number, error

echo $((var++)) #post increment
```

```bash
i=1
weekdays="Mon Tue Wed Thu Fri"
for day in $weekdays
do
	echo "Weekday $((i++)): $day"
done
```

Case statement
```bash
animal=$1
case $animal in
	cat)
		echo "You entered 'cat'"
	;;
	dog)
		echo "You entered 'dog'"
	；；
	*) #anything but case excutes from top to bottom sequentially.
	   #if the top conditions are meet, the last line skip automatically 
		echo "You did not enter 'cat' or 'dog'"
	;;
esac

#use `|` if multiple patterns execute the same block
case $1 in
	add | addition)
		result=$(($2 + $3))
	;;
	sub | subtraction)
		result=$(($2 - $3))
	;;
	*)
	result=0
	;;
esac
echo "The result is $result"
```

#### Functions: use like command 
- useful whenever there is repetitive cod e
- `local` defines local variables otherwise the variables are global by default even defined in a function
```bash
fun() {
	local x=5
	y=6
}
fun #calling function
echo "value x outisde function: $x" ($x is empty)
echo "value y outside function: $y" (6)
```

- passing argument through $1 $2 ...
```bash
add(){
	echo $(( $1 + $2 )) #永远指向函数内部
}

add 5 6 #same as command arguments
```

- bash function returns an exit status, cannot return a value
- can use command to echo returned value
```bash
add() {
	local sum=$(( $1 + $2 ))
	echo $sum
}
result=$(add 5 6)
```
#### Text stream processing commands
`cut -d <delimiter分隔符> [file]`
```bash
cut -d ',' -f1,3 data.csv
#定逗号为分隔符
#提取以逗号分隔的第一和第三列 (field numbers)
#若不写-d 默认tab为分隔符
```

`wc [-clw] file` 
- word count
- clw stands for character, line and word, and tells wc which to count

cut with csv(comma separated values) file
- each row is called a record 行
- each unit of data in a row is called a 'field' 列 fieldname(列的第一行)
```bash
cut -d ',' -f2 users.csv #extract the second field
```

More commands

`sort [option] [file]`
- -n : numerically 
- -r : in descending order
- -o outputfile : output the sort result to a file

`uniq [file]`
- Removes *consecutive duplicate* lines and prints only one instance
- -c : prefix each line with the number of occurance
- only works on sorted input, because it only compares adjacent lines

**Text stream processing often chained together with `|`**
`cat data.txt | cut -f2 | sort | uniq -c | sort -nr`

#### grep
- used to search for patterns in files
- `grep [options] STRING FILE_LIST`
	- STRING is the pattern to match (regular expression/regex)
	- it returns a whole line containing the match
- options
	- -i : ignore case
	- -n : display line number along with the line on which a match was found
	- -c : report only a count of lines with the matches
	- -v : invert, displays the lines do not that
	- -l : list filenames, not lines
```bash
grep 'Je' students.txt #list out students whose names start with Je

cat students.txt | grep 'Je' #piping txt to grep, equivalent

grep -n 'Je' students.txt
#6:Jeremy
#7:Jessica
#10:Jean-Sebastien
``` 

#### quiet
- If you don't want to see the output of a command on the screen 
```bash
grep -q

ls > /dev/null 2 > /dev/null #redirect stdout and stderr to devnull
#or
ls > /dev/null 2>&1
```