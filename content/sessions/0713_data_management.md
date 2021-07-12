+++
title = "Data management"
date = 2021-03-24T12:58:37+13:00
draft = false
weight = 5
+++

Ludovic Dutoit, July 2021

### Description

This session covers the essential of data management for a project on NeSI. It starts with a bit of general thinking before moving into some [NeSI](https://www.nesi.org.nz/) specifics. 


## Good habits

* Always have your data in at least two places.
* Never edit your raw data.
* Use informative file names: `filtered_data.txt`is meaningless on its own. `data_noMISSINGDATAremoved12lowqual.csv` is much better.
* Avoid proprietary formats
* Have a readme file
* Your methods are easily transportable, and should bring anyone from raw data to results. Put your efforts there, Try to see files as checkpoints, not at the center of your structure.
* Use version control (i.e. github.com)

## Tips and tricks for data management on NeSI


If you do not have access to NeSI yet, apply [here](https://www.nesi.org.nz/). Free, powerful, and maintained for you!


There are essentially 3 file systems on NeSI.

They are explained [here](https://support.nesi.org.nz/hc/en-gb/articles/360000177256-NeSI-File-Systems-and-Quotas).


**How to check your usage?**

```sh
nn_storage_quota # check your quotas, specific to NeSI
du -h # Show the size of every directory in the data structure.
du -h | grep -E "^[0-9]+G" # check all the directories in the Gb range
```

That is all good and well, but we sometimes end up with huge quantity of small files, can we have an infinity of those? No, files are assiocated to metadata, an empty file still takes some space for metadata on the system. That space is referred to as **inodes**, and they can also reach a quota.

```sh
nn_storage_quota
echo "Inode usage for $(pwd)" ; for d in `find -maxdepth 1 -type d | cut -d\/ -f2 | grep -xv . | sort`; do c=$(find $d | wc -l) ; printf "$c\t\t- $d\n" ; done ; printf "Total: \t\t$(find $(pwd) | wc -l)\n" # This counts the inodes
```


**Where are those backups anyway?**

```sh
cd  # Brings you home
cd .snapshots
ls -lh 
```

You got one week of backups there. Whether it is that exact folder or its content.

Same inside the `/nesi/project/` but not in 'nobackup'


## Links

```sh
cd /nesi/nobackup/uooXXXXX # go to your nobackup directory
mkdir tmp_data
touch sample{0001..1000}.fastq
```

Wow, we have a 1000 files here. You'd like to use them from your nobackup inside your normal project

```sh
cd  /nesi/project/uooXXXXX # go to your  project directory
```

Let's create a link:

```
ln -s  /nesi/nobackup/uooXXXXX/tmp_data/ . # create a soft link here. "." is for here
```

Have a look inside:

```
ld -lh
ls -lh tmp_data/
```
Yay it is all here, we basically created a shortcut without duplicating the files.


Let's remove it now:

```
rm -r  tmp_data/ # -r is needed to remove a directory
```

Is the original folder still there?

```
ls -lh  /nesi/nobackup/uooXXXXX/tmp_data/
```

YES!


Still not enough space? Ask [support@nesi.org.nz](support@nesi.org.nz) first, if it is not enough, you can get data on the [high capacity storage (HCS)](https://www.otago.ac.nz/its/services/hosting/otago068353.html) of the university too.
