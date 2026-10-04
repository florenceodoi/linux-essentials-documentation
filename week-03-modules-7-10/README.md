# Linux Essentials Week 3 Documentation

## Modules 7–10: Filesystem Navigation, File Management, Archiving, Compression and Text Processing

This week, I continued my Linux Essentials journey by learning how to navigate the Linux filesystem, manage files and directories, create archives, compress files, and work with text from the command line.

The practical exercises helped me understand how Linux users move around the filesystem, organise files, create backups, reduce file sizes, and process text efficiently using commands and pipelines.

## What I Learnt

### 1. Navigating the Linux Filesystem

I learnt that Linux uses a hierarchical filesystem.

The top level of the filesystem is the root directory:

```bash
/
```

A user's personal working directory is the home directory, represented by:

```bash
~
```

I also learnt the difference between absolute and relative paths.

An absolute path starts from the root directory, while a relative path starts from my current working directory.

Two useful shortcuts are:

```text
.  = current directory
.. = parent directory
```

### 2. Listing Files and Directories

The `ls` command is used to display files and directories.

```bash
ls
```

Useful options include:

```bash
ls -a
```

Displays all files, including hidden files.

```bash
ls -l
```

Displays detailed information about files.

```bash
ls -lh
```

Displays detailed information with human-readable file sizes.

I also learnt that Linux hidden files normally begin with a dot, such as `.bashrc`.

## My Hands-On Practice

### Screenshot 1: Navigating the Filesystem

![Filesystem Navigation](screenshots/01-filesystem-navigation.png)

In this exercise, I practised checking my current location and moving through different directories.

### Screenshot 2: Managing Files and Directories

![File Management](screenshots/02-file-management.png)

Here, I practised creating, copying, renaming, and listing files and directories.

### Screenshot 3: Archiving and Compression

![Archiving and Compression](screenshots/03-archiving-compression.png)

This exercise helped me understand how Linux combines files into archives and compresses them to reduce storage space.

### Screenshot 4: Working with Text

![Working with Text](screenshots/04-working-with-text.png)

In this exercise, I practised creating, displaying, and processing text from the command line.

### Screenshot 5: Pipes and Redirection

![Pipes and Redirection](screenshots/05-pipes-redirection.png)

This exercise showed me how the output of one command can be redirected into a file or passed into another command.

### Screenshot 6: Searching Text with Grep

![Grep and Regular Expressions](screenshots/06-grep-regex.png)

Here, I practised searching and filtering text using `grep` and simple regular expressions.

## Commands I Used

### `pwd`

```bash
pwd
```

The `pwd` command displays my current working directory.

### `cd`

```bash
cd ~
```

The `cd` command changes directories. The `~` symbol represents my home directory.

### `ls`

```bash
ls
```

The `ls` command displays files and directories.

### `mkdir`

```bash
mkdir linux-week3-practice
```

The `mkdir` command creates a new directory.

### `touch`

```bash
touch sample.txt
```

The `touch` command creates an empty file.

### `cp`

```bash
cp sample.txt sample-copy.txt
```

The `cp` command copies a file.

### `mv`

```bash
mv sample-copy.txt renamed-sample.txt
```

The `mv` command moves or renames files.

## Globbing

I learnt that globbing allows the shell to match groups of filenames using patterns.

For example:

```bash
echo *
```

The `*` character matches zero or more characters.

Other glob characters include:

```text
?     = matches one character
[ ]   = matches one character from a range or group
```

## Archiving and Compression

I learnt that archiving and compression are related but different.

Archiving combines several files into one file.

Compression reduces the size of a file.

Some of the tools I studied include:

- `tar`
- `gzip`
- `gunzip`
- `bzip2`
- `bunzip2`
- `xz`
- `unxz`
- `zip`
- `unzip`

### `tar`

```bash
tar -czf linux-week3-practice.tar.gz linux-week3-practice
```

In this command:

```text
-c = create archive
-z = use gzip compression
-f = specify archive filename
```

I also learnt the difference between lossless and lossy compression.

Lossless compression allows the original data to be restored exactly, while lossy compression removes some information to reduce file size.

# Module 10: Working with Text

## Viewing Text Files

The `cat` command displays the contents of a text file.

```bash
cat linux-note.txt
```

The `head` command displays the beginning of a file.

```bash
head linux-note.txt
```

The `tail` command displays the end of a file.

```bash
tail linux-note.txt
```

For larger files, I learnt that `more` and `less` allow users to view text one page at a time.

## Creating and Redirecting Text

I used `echo` to create text.

```bash
echo "Linux is becoming interesting" > linux-note.txt
```

The `>` symbol redirects standard output into a file.

I learnt that `>` overwrites existing content.

To add new text without deleting the existing content, I used:

```bash
echo "I am learning text processing" >> linux-note.txt
```

The `>>` symbol appends output to a file.

## Pipes

One of the most useful concepts I learnt was piping.

The pipe symbol is:

```text
|
```

It sends the output of one command into another command.

Example:

```bash
ls /etc | head
```

The `ls` command produces the directory listing, while `head` displays only the first part of that output.

Another example is:

```bash
cut -d: -f1 /etc/passwd | sort | head
```

This extracts usernames, sorts them, and displays the first results.

I learnt that the order of commands in a pipeline matters because each command receives the output of the previous command.

## Standard Input, Output and Error

Linux uses three standard streams:

```text
STDIN  = 0
STDOUT = 1
STDERR = 2
```

`STDIN` usually comes from the keyboard.

`STDOUT` is the normal output produced by a command.

`STDERR` contains error messages.

These concepts helped me understand Linux redirection.

Examples include:

```text
>   redirect output and overwrite
>>  redirect output and append
<   redirect input
2>  redirect error messages
```

## Text Processing Commands

### `wc`

```bash
wc linux-note.txt
```

The `wc` command counts lines, words, and bytes.

### `cut`

```bash
cut -d: -f1 /etc/passwd
```

The `cut` command extracts selected fields or columns.

### `sort`

```bash
cut -d: -f1 /etc/passwd | sort
```

The `sort` command arranges lines of text.

### `grep`

```bash
grep "Linux" linux-note.txt
```

The `grep` command searches for lines containing a specified pattern.

To ignore uppercase and lowercase differences:

```bash
grep -i "linux" linux-note.txt
```

## Regular Expressions

I also learnt that regular expressions are patterns used to search text.

Some important symbols include:

```text
.     = any single character
[ ]   = one character from a range
*     = zero or more repetitions
^     = beginning of a line
$     = end of a line
```

For example:

```bash
grep '^root' /etc/passwd
```

searches for lines beginning with `root`.

Extended regular expressions can be used with:

```bash
grep -E
```

Examples of extended regular expression symbols include:

```text
? = zero or one occurrence
+ = one or more occurrences
| = OR
```

## Challenges

One challenge this week was understanding the difference between absolute and relative paths.

At first, paths such as:

```text
/home/user/Documents
```

and:

```text
Documents
```

looked similar, but practical navigation helped me understand that the first starts from the root directory while the second depends on my current location.

Another challenge was remembering command options because the same option can behave differently with different commands.

Module 10 also introduced several symbols such as `>`, `>>`, `|`, `^`, `$`, and `*`. At first, these symbols looked confusing, but using them practically helped me understand their purposes.

I also realised that when output is redirected to a file, nothing may appear on the screen. This initially looked like the command had failed, but I learnt that the output had simply been sent somewhere else.

## Key Takeaways

My biggest takeaway from Week 3 is that Linux commands become more useful when they are combined.

Filesystem commands allow me to move around and manage files.

Archiving and compression tools allow me to organise files, create backups, and reduce file sizes.

Text-processing commands allow me to search, filter, sort, count, and redirect information.

The pipe command was especially important because it showed me how several simple commands can work together to perform a more powerful task.

I am also learning that using Linux effectively is not about memorising every command. It is about understanding what commands do, practising them, reading the output, and learning how to combine them.

Week by week, I am becoming more comfortable working directly from the Linux terminal.
