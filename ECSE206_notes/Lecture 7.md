#### Positional variables
- e.g. if we run `./script 5 2 bob`
- From the script we access using $1, $2, $3

#### Quotes
- single quotes are use to preserve the literal value of characters within the quotes
- double quotes are used to preserve the literal values of characters within the quotes
	- exceptions: $ (variables still get expanded), \` , \ (escape character)
- e.g. `mkdir "John Smith"` --> a directory called John Smith
	- otherwise create two directories John and Smith
```bash
x = "John Smith"
mkdir $x # expand to mkdir John Smith
# creates two directory
mkdir "$x"
```

#### Control flow

Exit status
- Any program when it exists, gives a status code back to the OS to signal whether the command succeeded or failed
- 0 means success, 1 commonly means failure
- 