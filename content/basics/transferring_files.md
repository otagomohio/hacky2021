+++
title = "Transferring Files"
date = 2021-03-24T12:58:37+13:00
draft = false
weight = 5
pre = "<b>1. </b>"
+++


Following are some example commands for transferring files and folders to and from the server. 

Remember:

* You must have permissions to access the target folder on the server to which you wish to move your file

* Your terminal must be on your computer to move files (that is, your pwd should be somewhere on your own computer)

## Transfer files from your own computer to the server

```bash
scp /path/to/file/FILENAME mahuika:/path/to/target/folder
grep -c '>' FILENAME
```

(Note the colon ':' after the server name.) 

If your terminal is in the folder containing the file, you do not need the path:

```bash
scp FILENAME mahuika:/path/to/target/folder
```

Likewise, if you are transferring the file to your home folder on NeSI, then you do not need the path (although remember that your NeSI home folder does not have much space):

```python
for i in team:
    print(i)

scp FILENAME mahuika:
```

Transferring to a subfolder in your home folder on NeSI:

```r
library(tidyverse)
a <- read.table('tablename')
scp FILENAME mahuika:scripts/
```

If the folder is in another part of NeSI, then you need to put the full path:

```bash
scp FILENAME mahuika:/nesi/project/uooXXXX/example_project/example_subfolder/
```

If you want to upload an entire folder (make sure you want to move all the files), just add the -r argument:

```bash
scp -r /path/to/FOLDERNAME mahuika:/path/to/target/folder
```

Note that this will create a folder called FOLDERNAME within the target folder.

## Transfer files from the server to your own computer

In order to move files from NeSI or another server to your own computer, the order of paths is reversed:

```bash
scp mahuika:/path/to/file/FILENAME /path/to/target/folder/
```

Note if your terminal is in the target folder (pwd), then you can just add a period at the end:

```bash
scp mahuika:/path/to/file/FILENAME .
```

The same rules apply for absolute paths. For example, if you are moving a file from your home folder on NeSI:

```bash
scp mahuika:FILENAME /path/to/target/folder/
```

You can also substitute the ~ (tilde) for the root path on your computer (e.g. ~/ instead of /Users/hughcross/)

And the same rules apply for downloading folders:

```bash
scp -r mahuika:/nesi/project/uooXXXX/example_project/example_subfolder/ /path/to/target/folder
```

## rsync: A better way?

You can also use the command line tool **rsync** to move files to and from the server. It has many uses, such as making regular backups to an external hard drive. rsync has some advantages over using scp, for example, you can update a folder you have already copied to the server, and it will only update the files that have changed (if it is a big folder, this can save lots of time). As well, if the transfer is interrupted, rsync will pick up where it left off. For purposes of archiving, when using rsync, the timestamp of your original files will be preserved, whereas with scp the date of the copied files will be the current one. This can be useful when backing up and preserving the original dates of your files.

For a single file

{{< highlight bash >}}
rsync FILENAME mahuika:/path/to/target/folder
{{< / highlight >}}

It is better to use the ```-a``` option, as that will preserve time stamp and permissions, etc. Here I have also added the ```-v``` option (--verbose) which will output the status:

```bash
rsync -av FILENAME mahuika:/path/to/target/folder
```


For syncing folders it is the same command:

```bash
rsync -av /path/to/folder mahuika:/path/to/target/folder
```

And, the same thing transferring from the server to your computer:

```bash
rsync -av mahuika:/path/to/folder ~/Documents
```

If you add the ```--delete``` option, any files on the target that are not on the source folder will be deleted. To avoid accidentally deleting any precious files, it is advised to use the ```--dry-run``` command first, which will show you what would happen without actually doing anything:

```bash
rsync -av /path/to/source/folder --dry-run --delete scripts mahuika:/path/to/target/folder
```

Once you have checked it will do what you want, you can run without the ```dry-run``` option

```bash
rsync -av /path/to/source/folder --delete scripts mahuika:/path/to/target/folder
```

As mentioned, you can do this to back up to an external hard drive:

```bash
rsync -av /path/to/source/folder /Volumes/NAME_OF_EXTERNAL_HD/target/folder
```


