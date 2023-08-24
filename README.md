# streaming-02-multiple-processes

> Multiple processes accessing a shared resource concurrently

## Overview

This example starts a shared database and multiple processes.

The processes represent multiple users, or locations, or programs 
hitting a shared database at the same time. 


## Task 1. Fork 

Fork this repository ("repo") into **your** GitHub account. 

Repo was forked without issue.

## Task 2. Clone

Clone **your** new GitHub repo down to the Documents folder on your local machine.

The repo was cloned without issue.

## Task 3. Explore

Explore your new project repo in VS Code on your local machine.

## Task 4. Execute Check Script

Execute 00_check_core.py to generate useful information.

This ran without issue.

## Task 5. Execute Multiple Processes Project Script

Execute multiple_processes.py.

Read the output. Read the code. 
Try to figure out what's going on. 

1. What libraries did we import?
    Datetime, logging, multiprocessing, os, platform, sqlite3, sys, and time.
1. Where do we set the TASK_DURATION_SECONDS?
    Near the top of the script, shortly after the imports. It is set in the same area the database and the divider.
1. How many functions are defined?
    7 functions are defined.
1. What are the function names? 
    recreate_database, create_table, drop_table, insert_pet, process_one, process_two, process_three
1. In general, what does each function do? 
    recreate_database: creates a database by creating or removing tables.
    create_table: create a table in a database if a connection to the database can be established.
    drop_table: remove a table from a database if that table name exists.
    insert_pet: create a record in the table for a given pet.
    process_one: insert 2 specific pet records
    process_two: insert 2 specific pet records
    process_three insert 2 specific pet records
1. Where does the execution begin? Hint: generally at the end of the file.
    At the line near the bottom that reads: if __name__ == "__main__":
1. How many processes do we start?
    We start 3 processes.
1. How many records does each process insert?
    Each process inserts 2 records into the database.

In this first run, we start 3 processes, 
each inserting 2 records into a shared database 
(for a total of 6 records inserted.)

In each case, the process gets a connection to the database, 
and a cursor to execute SQL statements.
It inserts a record, and exits the database quickly.

In general, we're successful and six new records get inserted. 

## Task 6. Execute Multiple Processes Script with Longer Tasks

For the second run, modify the task duration to make each task take 3 seconds. 
Hint: Look for the TODO.
Run the script again. 
With the longer tasks, we now get into trouble - 
one process will have the database open and be working on it - 
then when another process tries to do the same, it can't and 
we end up with errors. 

It seems that when the time is updated to 3 seconds, the tables do not run in any particular order, and errors or lockouts tend to occur.

## Task 7. Document Results After Each Run

To clear the terminal, in the terminal window, type clear and hit enter or return. 

`clear`

To document results, clear the terminal, run the script, and paste all of the terminal contents into the output file.

Use out0.txt to document the first run. 

Use out3.txt to document the second run.


-----

## Helpful Information

To get more help on the early tasks, see [streaming-01-getting-started](https://github.com/denisecase/streaming-01-getting-started).

### Select All, Copy, Paste

On Windows the select all, copy, paste hotkeys are:

- CTRL a 
- CTRL c 
- CTRL v 

On a Mac the select all, copy, paste hotkeys are:

- Command a
- Command c
- Command v

Detailed copy/paste instructions (as needed)

1. To use these keys to transfer your output into a file, 
clear the terminal, run the script, then click in the terminal to make it active.
1. To select all terminal content, hold CTRL and the 'a' key together. 
1. To copy the selected content, hold CTRL and the 'c' key together. 
1. To paste, open the destination file (e.g. out0.py) for editing.
1. Click somewhere in the destination file to make it the active window.
1. Now hit CTRL a (both together) to select all of the destination file.
1. Hit CTRL v (both together) to paste the content from your clipboard.

Do a web search to find helpful videos on anything that seems confusing
and share them in our discussion.

### Reading Error Messages

Python has pretty helpful error messages. 
When you get an error, read them carefully. 

- What error do you get?

### Database Is Locked Error

Do a web search on the sqlite3 'database is locked' error.

- What do you learn?
- Once a process fails, it crashes the main process and everything stops. 

### Deadlock

Deadlock is a special kind of locking issue where a process 
is waiting on a resource or process, that is waiting also. 

Rather than crashing, a system in deadlock may wait indefinitely, 
with no process able to move forward and make progress.

### Learn More

Check out Wikipedia's article on deadlock and other sources to learn how to prevent and avoid locking issues in concurrent processes. 


### Zach's Notes

When streaming from my own data source, I ran into an issue where I had more columns in my csv than I was unpacking, which caused an error. To solve this, I simply needed to remove the unnecessary columns from the csv and try again. 

To avoid deadlock, it seems that limiting the amount of time a process occurs can help. In the multiple processing example, the script ran without errors when the time was set to 0 seconds, but when it was set to 3 seconds, lockouts occurred. However, I imagine deadlock could possibly still occur with a time span of 0 seconds due to a number of factors with specific processes. There are probably ways in the processing module to order how processes occur, which I imagine is the appropriate way to handle this situation.