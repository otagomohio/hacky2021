+++
title = "Loops"
date = 2021-10-05
draft = false
weight = 17
+++

Written and Presented by Ludovic Dutoit

Loops are awesome at doing what computers do best, repeating an exact task many times without errors. They are commonly used to repeat a task over a list of files, or numbers, or anything you can think of.

## The Bash loop

The basic structure of a loop is as follows:

```sh
for <variable name> in <a list of items>
do <some command> $<variable name>
done
```

The variable name will be the variable you specify in the do section and will contain the item in the loop that you're on.

The list of items can be a lot of different things, but we often works with numbers or files.

Here is a simple bash loop

```sh
for fruit in banana lemon orange
do echo $fruit
done
```

**Output:**

```
banana
lemon
orange
```

It is important to understand that your variable (i.e. fruit) can be called anything. We just called it fruit in the example because it makes sense to us. It is important to use the $ before the variable name inside the loop cause we are referring to the variable, not the word fruit. Any word could be used instead:

```sh
for animal in banana lemon orange
do echo first $animal
echo second $anial
done
```

There are loads of resources when it comes to using loops to real life example. Below is an example on 2 little files.

Let's create two files:

```
echo $'first file line 1 \nfirst file line 2' > file1.dummy
echo $'second file line 1 \nsecond file line 2' > file2.dummy
```

we can easily manipulate those files with a loop:

```
rm -f last_lines.txt # will store the last lines
for file in *dummy
do 
echo $file
tail -n 1 $file >> last_lines.txt # append the last line to file last_lines.txt
done
```

In this loop the last line of each file that finished by dummy is appended using >> to the file last_lines.txt. A single > would simply overwrite the file every time. Note that I remove the file as the first line. This is because I append in the loop and if the file already existed, I'd end up appending to an already existing files. So I remove a file that may or may not exist as a precaution. The -f means you don't get an error message if the file does not exist (yet).

You can check the content of the file with:

```
cat last_lines.txt
```

### Job arrays

On Nesi, iterating (i.e. looping) over numbers can be used to run easily a large number of jobs. The help examples from the [job array support page](https://support.nesi.org.nz/hc/en-gb/articles/360000690275-Parallel-Execution#t_array) was given in class. 


### R Loops

To introduce to R loop, I am simply going to share one very well documented link that has all the info. Loops are functionally similar across programming languages, but the syntax (i.e. way of writing) varies slightly.

[Data carpentry R loops]https://datacarpentry.org/semester-biology/materials/for-loops-R/





