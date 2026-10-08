<!-- Written by TA Eve -->
# The Log Analyzer

Bash is used a lot of the time for system health checks (tracking logs and alerts). The goal of this question is to write a Bash script that analyzes a server log file. The question is split into a few parts that test different aspects of Bash: arguments, file tests, loops, pipes, and redirection. Note that the full script should be in one file, called `analyze.sh`.

Each line of the log file has the following format:

```text
DATE TIME LEVEL MESSAGE
```

where `LEVEL` is one of `INFO`, `WARNING`, or `ERROR`, and `MESSAGE` can contain spaces. An example log file, `server.log`, is shown below. You can test with this one or create your own.

```text
2026-09-20 14:02:11 INFO Server started
2026-09-20 14:05:43 WARNING High memory usage
2026-09-20 14:07:02 ERROR Disk full
2026-09-20 14:07:05 ERROR Write failed
2026-09-20 14:10:19 INFO User login: alice
2026-09-20 14:12:55 ERROR Disk full
2026-09-20 14:15:30 WARNING Slow response time
2026-09-20 14:20:01 ERROR Connection timeout
2026-09-20 14:21:47 INFO User logout: alice
2026-09-20 14:25:10 ERROR Disk full
2026-09-20 14:30:00 ERROR Backup failed
```

## a)

The script should take exactly one argument: the path to the log file. For example:

```text
./analyze.sh server.log
```

Before doing anything else, the script should check its input:

- If the number of arguments is not exactly one, print a usage message and exit with error code 1.
- If the file does not exist or is not readable, print an error message and exit with error code 2.

## b)

Using a `while` loop, read the log file line by line and count how many lines there are of each level. Then print the totals in the following format:

```text
INFO: 3
WARNING: 2
ERROR: 6
```

**Hint**: Note that `read` can split a line into several variables at once. If you give it more variable names, each word goes into the next variable, and the last variable gets the rest of the line. You may find this helpful for getting the level out of each line.

Make sure your counters start at 0, so that a level with no lines prints `0` rather than nothing.

## c)

Now compute the same counts **without using a loop**, using only pipes and basic commands such as `grep`, `cut`, `sort`, and `uniq`. Print the result to the terminal. (The output format does not need to match part b) exactly.)

Then answer the following question in a comment in your script: if a new level called `DEBUG` were added to the log file, which of your two approaches (b or c) would need to be changed, and why?

Be careful: a line such as `2026-09-20 14:40:00 INFO Recovered from ERROR state` should count as `INFO`, not `ERROR`. Make sure your solution handles this case.

## d)

If the log file contains **more than 5** errors, the script should add a line to a file called `alerts.txt` in the current directory, in the following format:

```text
2026-09-24: server.log had 6 errors
```

where the date is today's date and the filename is the argument passed to the script.

The alert should be **added** to the end of `alerts.txt`, not overwrite it. If you run your script twice, `alerts.txt` should contain two lines. If the file does not exist yet, it should be created.

## e) (Bonus)

1. Print the most common `ERROR` message and how many times it appears. In the example log, this is `Disk full`, which appears 3 times.
2. Allow the user to pass an optional second argument that sets the error threshold for part d). If no second argument is given, the threshold should default to 5. Update your check from part a) so that the script accepts either one or two arguments.


```bash
#!/bin/bash
if [ $# -ne 1 ]; then
	echo "The number of arguments should be 1." >&2
	exit 1
fi

if [ ! -f $1 ]; then
	echo "File does not exist" >&2
	exit 2
fi

counti=0
countw=0
counte=0

while read -r date time level message; do
 case "$level" in
	 WARNING)
		 countw=$((countw+1))
	 ;;
	 INFO)
		 countw=$((countw+1))
	 ;;
	 ERROR)
		 countw=$((countw+1))
	 ;;
	 esac
done < "$1"
	
echo "INFO: $counti\nWARNING: $countw\nERROR: $counte"

#or equivalently
cut -d ' ' -f3 "$1" | sort | uniq -c

if [ "$counte" -gt 5 ]; then
	echo "$(date +%Y-%m-%d): "$1" had "$counte" errors" >> alterts.txt
fi
```