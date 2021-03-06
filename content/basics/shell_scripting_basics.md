+++
title = "Shell scripting basics"
date = 2021-03-24T12:58:37+13:00
draft = false
weight = 30
+++



Once you move beyond basic shell commands, and the process becomes increasingly complicated, you are going to want the commands into a shell script. There are many good tutorials online to get you started. The [**Software Carpentry website**](https://software-carpentry.org/lessons/) includes some good tips on their [**Unix Shell lesson**](http://swcarpentry.github.io/shell-novice/) (chapters 5 and 6). As well, [**Data Carpentry**](https://datacarpentry.org/lessons/) has a good introduction on their lesson: [**Introduction to the Command Line for Genomics**](https://datacarpentry.org/shell-genomics/). For the lesson here, we will take you through some basics to get you started.

### Simple script

In a text editor, add the following:

```
#!/usr/bin/env bash

# a first script

echo 'Hello World'

```

The first line is called the *Shebang*, which tells the script where the BASH interpreter is. It is possible to run without this line, but your script may not work in all environments (see [**Here**](https://www.in-ulm.de/~mascheck/various/shebang/) and [**Here**](https://bash.cyberciti.biz/guide/Shebang) for more details than you would ever want to know). The next line that starts with the `#` is a comment, and is ignored by BASH, but can help tell the reader what is going on in the script. The last line just has the command to output "Hello World" to the screen. 

In order to run any new shell script, you have to make it executable:

```
chmod a+x
```

and now it should run. You just have to do this the first time you run it.

### A little less simple: running other programs

The following script *fastq2fasta.sh* will convert one of our example fastq files to a fasta format

```
#!/usr/bin/env bash

# running another program with the shell: seqtk 

# This command will convert the fastq file to a fasta file


seqtk seq -A example_data/e4485061.924a.4f09.9d7e.bfefc780d1a8_11_L001_R1_001.fastq > example_data/sample1.fasta

```

### Repeating the same command: Looping

The above script works fine if we want to just do one file (but then you would hardly need a script for one command for one file), but if we want to do the same command on multiple files, we can set up a for loop:

**Shell script: *fastq2fasta_loop.sh***

```
#!/usr/bin/env bash

# running another program with the shell: seqtk 

# This command will convert multiple fastq files to the fasta format

cd example_data

for fq in *.fastq
do
	seqtk seq -A $fq > $fq\.fasta

done

```

The `\` in the command is called an *escape*. That is so the program doesn't confuse what variable you are calling. 

### Playing with variables

Okay, now we can loop through multiple files and run the same command. The only thing with the above script is that now all of the fasta files end in ".fastq.fasta", which doesn't look so nice. We can adjust the variable that the for loop is iterating through to adjust the output name:

**fastq2fasta_loop_rename.sh**

```
#!/usr/bin/env bash

# running another program with the shell: seqtk 

# This command will convert multiple fastq files to the fasta format

cd example_data

for fq in *.fastq
do
	sampleName=$(echo $fq | cut -f 1 -d '.')
	echo $sampleName
	seqtk seq -A $fq > $sampleName\.fasta

done

```

### Looping from a file

If we don't want to run all the files in the folder, we can make a list and run the loop from there. One way to do this is a *While* loop:

**fastq2fasta_while_loop_rename.sh**

```
#!/usr/bin/env bash

# running another program with the shell: seqtk 

# This command will convert multiple fastq files to the fasta format

cd example_data

cat fqlist | while read line
do
	sampleName=$(echo $line | cut -f 1 -d '.')
	echo $sampleName
	seqtk seq -A $line > $sampleName\.fasta

done

```

We can also take more complicated things from a file, for example a table with old and new names, and use these with our variable slicing to give more sensible names to our files:

**fastq2fasta_loop_newName.sh**

```
#!/usr/bin/env bash

# running another program with the shell: seqtk 

# This command will convert multiple fastq files to the fasta format

cd example_data

cat fqTable | while read line
do
	currentName=$(echo "$line" | cut -f 1)
	newName=$(echo "$line" | cut -f 2)
	echo $currentName
	echo $newName
	seqtk seq -A $currentName > $newName\.fasta

	# can also use to just change names:
	#mv $currentName $newName

done

```


### *Are you jazzed about for loops and want even more speed?* 
We've got a small guide on how to [parallelize these loops](2019_09_11_parallel_loop_extension.md)









