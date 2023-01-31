---
title: "Don't be afraid of the command line"
date: 2023-01-28T19:24:20+04:00
draft: false
tags:
  - tech
  - linux
---


We are so used to graphical user interfaces that we forget computers started off without it. As an engineer, there are many reasons why using the command line can help with scripting.

- Less context switching -> more focus
- Lightweight -> faster development
- Deeper understanding of tools and the computer
- Higher interoperability between computers

On an aside, the recent trend of containerization requires you to be familiar with the command line. With most containers being in linux and entering them would mean that there's no user interface so you have to depend on the good old fashion command line.

# CLI Basics

I'm assuming you're using either Mac or Linux, as Windows may behave differently. Most development machines are based on UNIX anyway.

With that, I'll be explaining some common command line commands that are present in most computers which I commonly use. They won't be exhaustive but I encourage you to read more of them in the [Linux Pocket Guide](https://www.amazon.com/Linux-Pocket-Guide-Essential-Commands-ebook/dp/B01GGQKXRG).

## cd
It allows you to go to a relative or absolute path.

```
cd child_directory  # relative path to child_directory 
cd /usr/foo/directory  # absolute path
cd ../sibling_directory  # go to parent directory then into sibling directory
cd  # without arguments returns you to the home directory
```

## ls
Short for "list". Lists attributes of files and directories.

```
ls  # lists files in current directory
ls directory  # list files in that directory
ls -a  # lists all files, including hidden ones
ls -lhrt # I use this most of the time
```

## export
Creates environment variables. Note that you'll need to define these environment variables in a `.bashrc`, `.zshrc` or any file that loads when the shell is created if you want this environment variable to always be present. Otherwise, this environment variable would not persist beyond it's current shell.

```
export FOO=ohayo
echo ${FOO}  # would show `ohayo`
```
## printenv
Helpful for debugging to figure out what are the current environment variables.

## history
Prints the commands you have used previously. Helpful when used with `grep`.

## alias
Does what it says.

```
alias gp='git push'
gp  # would be equivalent to typing `git push`
```

## mv
Short for "move". Move / Rename file(s) or directories.

```
mv foo.txt bar.txt  # renames foo.txt too bar.txt
mv blah.txt foo.txt destination_directory  # moves blah.txt and foo.txt to destination_directory
```

## cp
Short for "copy".

```
cp original.txt copy.txt  # creates copy.txt which is a copy of original.txt
cp original.txt directory  # creates a copy of original.txt into `directory`
```

## rm
Short for "remove".

```
rm foo.txt  # removes foo.txt
rm -r directory  # removes anything in this directory
```

## pwd
Prints the absolute path of your current working directory.

## mkdir
Short for "make directory".

```
mkdir foo  # creates foo directory
mkdir -p foo/bar/bar  # creates any parent directories if necessary
```

## echo
Prints arguments passed into it.

```
echo ohayo  # prints `ohayo`
```

## cat
Concatenates and print files. Basically just means printing the whole file.

## less
Something like cat but good for larger text and if you want to browse by pages.

## grep
Given some files, print lines which match a regular expression pattern. Pretty powerful stuff if you're well versed in regular expressions.

## Given this file a_text_file.txt.

```
80 days around the world, we’ll find a pot of gold just sitting where the rainbow’s ending.
Time — we’ll fight against the time, and we’ll fly on the white wings of the wind. 
80 days around the world, no we won’t say a word before the ship is really back.
Round, round, all around the world. Round, all around the world. Round, all around the world.
Round, all around the world. 
```

```
grep time  # Time — we’ll fight against the time, and we’ll fly on the white wings of the wind.
```

## touch
Usually used to create empty files since it creates the file if it doesn't exist. It also updates the modification timestamp and access timestamp of the file.


## | (pipe)
Passes the output of the previous command to the next. This is the key to mastering the command line. Commands on it's own don't seem that powerful but combine them with each other and the possibilities are endless. And that's what the unassuming | (pipe) does.

```
cat file.txt | grep text  # finds `text` in every line in file.txt
history | grep git  # prints git commands you have used previously
```

## xargs
Another powerful command that reads each line of text from the input and turns passes each of them to the next command and executes them. It'll be clearer when you try out the examples.

```
ls | xargs ls  # runs ls on all child directories and prints the result
grep foo --files-with-matches | xargs rm  # removes all files with `foo`
```

## Exploring tools
Now you know the basics, but you'll need to figure out how to use these commands on your own. Most commands have a help option.

```
ls --help
grep --help
```

If not, they would likely have a `man` or short for manual.

```
man ls
man cat
man echo
man grep
```

These commands are just scratching the surface of what you can do, so the best way to try them out is to use them in your daily workflow.

