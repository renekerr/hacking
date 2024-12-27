# Linux Operators Quick Reference

## Overview
Common Linux operators used for command execution and output redirection.

## Operators Table

| Symbol / Operator | Description |
|------------------|-------------|
| & | This operator allows you to run commands in the background of your terminal. |
| && | This operator allows you to combine multiple commands together in one line of your terminal. |
| > | This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. |
| >> | This operator does the same function of the > operator but appends the output rather than replacing (meaning nothing is overwritten). |

## Usage Examples

```text
# Background process with &
long-running-command &

# Command chaining with &&
cd /path/to/directory && ls -la

# Output redirection with >
echo "Hello" > file.txt

# Output appending with >>
echo "World" >> file.txt
