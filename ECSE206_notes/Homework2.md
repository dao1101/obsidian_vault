# Note:

This assignment requires making Bash scripts, which we will talk about in class next week. However, you can start working on it now: Before getting started, see the file `starter-code`, which gives a quick tour of the features of bash scripting that you will need to complete this homework.

Learning goal developed and assessed in this homework:

- Write bash scripts to automate development tasks


## Q1: Making backups of your homework


Recall that `rm` is irreversible on Linux. This is different from Windows or macOS, where

"deleting" a file actually places it into some kind of recycling/trash bin from where you can

restore the file.  

This means that making backups is very important on Linux! It sure would be terrible if you

accidentally did `rm -rf ~/comp-206/homework`.  

**Your task** is to create a script called `backup-hmk`, to be run from the `~/comp-206`

directory, which creates an archive of your `homework` directory, storing it in

`~/comp-206/backups`. Your script should create this directory if it does not already exist.
Example:

```bash

$ cd ~/comp-206

$ # from here, run the script that is in homework/hw2/backup-hmk

$ homework/hw2/backup-hmk

Created backup: backups/homework-2026-09-11T15:41:00.tar.gz

$ tar tvf backups/homework-2026-09-11T15:41:00.tar.gz

homework/

homework/hw1

homework/hw1/instructions.md

homework/hw1/hello_world.txt

homework/hw1/screenshot.png

...

```

  

* Your script must create the subdirectory `backups` if it does not exist already.

* Your script must name the archive according to the example.

* That is, it must include the current date and time (a *timestamp*) from when the script is

      run.
* The `date` command prints the current date and time, but in the wrong format!

* Read the manual, `man date`, to see how to control the format of the timestamp.

* To capture the output of the `date` command into a variable, look up "bash command

      substitution", or see here:

 https://unix.stackexchange.com/questions/440088/what-is-command-substitution-in-a-shell

To learn how to use the `tar` program for creating archives, see

[this guide](https://www.gnu.org/software/tar/manual/html_chapter/Tutorial.html)

written by the folks at GNU, which are the makers of the programs `ls`, `mkdir`, etc. that we use all the time.

Take notes (in vim) along the way!

**Besides writing the script,** answer these short questions in a file called `using-tar.txt`

(in your `hw2` directory, of course!)

Answer each in at most two lines, giving an example and a brief explanation in words:  

- Q1.1: how do you use tar to create an archive?

- Q1.2: how do you use tar to list the contents of an archive?

- Q1.3: how do you use tar to extract the entire contents of an archive?

- Q1.4: by default, where do the files get extracted to?

- Q1.5: what is the significance of the two extensions `.tar.gz`?

- Q1.6: what is a 'tarbomb'? Why could extracting one be dangerous?

    - Read this https://www.linfo.org/tarbomb.html and give a succinct answer.


Of course you could chatgpt all these questions, but then you wouldn't actually be learning

anything from this exercise. That will harm you when you are eventually tested on this material in

a midterm! So do your best to answer by looking things up on google, and in particular using the

GNU tar tutorial I linked above.  

## Automating getting homework

To download this homework, you would have done something like...

```bash
hba
$ cd ~/comp-206/homework

$ git clone SEMESTER-comp206:hw2.git

...

git outputs some message about the clone

...

$ cd hw2

$ ls

instructions.md starter-code

```

  

There are many assignments in this course, but the only thing that would

realistically change for downloading any particular assignment would be the

number. This is a perfect candidate for writing a script for automation.


**Your task** is to write a script called `get-homework` to automate this process.  

Running `get-homework 1` performs a git clone of the hw1 repo into the hw1 subdirectory of

`homework`.

Here's a simple example session demonstrating how the script should work.


```bash

$ ls ~/comp-206/homework

$ # see, no assignments yet; ls produced no output

$ get-homework 1

$ ls ~/comp-206/homework

hw1

$ ls ~/comp-206/homework/hw1

instructions.md

$ get-homework 1

Homework 1 directory already exists. Overwrite? [y/n] y

$

```

  

Here's the list of features that your script needs to support.

1. **The script must not be senstive to the current working directory.**

   In other words, you could be in any directory when you run the script, and it

   will correctly download the homework into ~/comp-206/homework.

   For example, if I'm in the labs directory, the command-line for running get-homework

   might look like this:

   `jerrin1@teach-node-07:comp-206/labs$ ~/comp-206/homework/hw2/get-homework 1`

   See, I typed out an absolute path to run `get-homework`, because I was in a

   different directory from `hw2`. This should still work to clone the hw1 repo.

2. **The script runs `git clone` to download the requested homework into the

   right location.

   `get-homework 1` runs `git clone SEMESTER-comp206:hw1.git`, (with SEMESTER

   being the name of the current one, of course) and so on for `get-homework 2`,

   etc. By the way, to specify _where_ to put the cloned directory, check out `man

   git-clone`. There are extra parameters you can use to do this. Your solution

   must use this approach, of specifying the destination of the clone via an extra

   argument to `git clone`.

# Submission instructions

Commit and push your hw2 repo with files named exactly as below.

- `using-tar.txt`

- `get-homework`

- `backup-hmk`

The scripts `get-homework` and `backup-hmk` must have the execute permission

enabled.



dwang8@teach-node-08:~/comp-206/homework/hw2$ cat starter-code
```

#!/bin/bash

  

# This is a bash script!

# Comments are written with '#' and continue to the end of the line, just like in Python.

  

# The very first line is not really a comment; it's called the "shebang" line, short for "hash

# bang", the two symbols at the beginning. The exclamation mark is called a "bang" in programming.

  

# In a bash script, you write commands just like you're used to on the command-line:

  

echo 'Hello world!'

  

# Any command you've seen before -- cp, mv, rm, rmdir, git, ls, cat, grep, cut, sort, uniq, etc. --

# can be used in a script.

  

# When you run this program as ./starter-code it will print out "Hello world!"

  

# To end a script early, you can use the `exit` command, and provide a _status code._

# This is a number that indicates whether the command succeeded or failed.

# Zero means success, and anything else means failure.

  

exit 0

  

##### PART 2: variables #####

  

# To define a variable in bash, use `=` but crucially with no spaces around it!

# To _use_ the value of a variable, put a `$` before the name of the variable.

  

name="$USER"

# ^ Creates a new variable `name` initialized with the value of the variable `USER`.

  

# Why no spaces? Imagine I had this line instead.

#

#     name = "$USER"

#

# Bash would understand this as _running a program_ named "name" and giving it two arguments:

# 1. the string "="

# 2. the string "jerrin" (in case it was you running the program, it would be your username)

  

# There are also numbered variables. There are the command-line arguments of the script.

  

echo $1 $2 $3 $4 #作为start-code的参数

  

# If we run this program as `./starter-code hello world foo bar`

# Then the program will print out: hello world foo bar

  

# In other words:

# $1 would hold "hello"

# $2 would hold "world"

# $3 would hold "foo"

# $4 would hold "bar"

  

##### PART 3: control flow #####

  

# the `if` and `while` statements in bash run a _command_ and check whether it succeeds (exits with a status code of 0)
  

if ls ~ #see if the ls ~ command succeeds

then

    echo 'Your home directory exists!'

else

    echo 'Uh-oh...'

fi

# An if-statement is terminated by the keyword "fi", which is "if" backwards. Seriously.

  
# Note that the command's output, if any, gets displayed. To prevent that, we can redirect the

# output.

  

if ls ~ >/dev/null 2>&1

then

    echo 'Your home directory exists!'

else

    echo 'Uh oh...'

fi

  

# /dev/null is a special file that just ignores anything you write to it. It's like a trash can for

# command output you don't care about.

#

# Recall the syntax `2>&1` means "redirect file descriptor 2 into whatever

# descriptor 1 currently points to". File descriptor 2 is the standard error

# stream, and we already redirected file description 1 (stdout) to /dev/null.

# Therefore in that command, `2>&1` also sends stderr to /dev/null.

  

# What about checking equality of two strings? Perhaps we want to check if the first command-line

# argument $1 equals "--help" to print out a helpful message.

  

# To do this, we use a program called "test" which can do all kinds of tests besides string

# equality.

  

if test "$1" = "--help" ; then # use a semicolon to put `then` on the same line as `if`

    echo "you're not really supposed to run this file, but rather read it."

fi

  

# The `test` program sees `=` and performs a string comparison. It exits with code 0 (success) if

# the strings are equal and with a nonzero code if they're unequal.

  

# That example can also be written as:

  

if [ "$1" = "--help" ] ; then

    echo "helpful message"

fi

  

# Indeed there is literally a file /bin/[

# That's right, there is a program called "open square bracket" and it's the exact same program as

# "test". The only difference is that it expects its last argument to be "]".

# Although this _looks_ like special syntax, it's not.

# Bash is just running a program (called open-square-bracket '[') and checking whether its exit code is 0.

  

# You might wonder why I put quotes around "$1" in that example.

# There's a good reason for that.

# If I didn't put quotes, what if someone did `./starter-code "multiple words"` ?

# Then `if [ $1 = "--help" ] ` expands into `if [ multiple words = "--help" ] `

# and `[` will give us an error because it's expecting exactly one argument to come before the `=`.

  

# But with the quotes, `if [ "$1" = "--help" ]` expands into `if [ "multiple words" = "--help" ]`

# and there's no issue.

  

# The best practice is to ALWAYS double-quote variables.

  

# Single-quotes, on the other hand, prevent variables from being expanded.

  

echo '$USER'

  

# will literally print out the string "$USER"

  

### One more way to check whether a command succeeds ###

  

# Every time you run a command, bash updates the variable $? (dollar question mark) with the exit

# code of that command. However, unless you care about the specific value of the exit code, it's

# more natural to just use the `if` statement to check whether running a command succeeds.
```


```bash
#backup
#!/usr/bin/bash

mkdir -p $HOME/comp-206/backups

TIMESTAMP=$(date +"%Y-%m-%dT%H:%M:%S")

BACKUP_FILE="$HOME/comp-206/backups/homework-${TIMESTAMP}.tar.gz"  

tar -czf "$BACKUP_FILE" -C "$HOME/comp-206" homework

echo "Created backup: backups/homework-${TIMESTAMP}.tar.gz"
~
```

```bash
#get-homework
#!/bin/bash

HW_PATH="$HOME/comp-206/homework"

SEMESTER="fall2026"

if ls $HW_PATH/hw$1 >/dev/null 2>&1

then
        echo "Homework $1 directory already exists. Overwrite? [y/n]"
        read answer
        if [ "$answer" = "y" ]; then
                rm -rf $HW_PATH/hw$1
                git clone "$SEMESTER-comp206:hw$1.git" "$HW_PATH/hw$1"
        fi
else
        git clone "$SEMESTER-comp206:hw$1.git" "$HW_PATH/hw$1"
fi
```