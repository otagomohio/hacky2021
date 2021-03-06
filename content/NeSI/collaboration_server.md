+++
title = "Collaboration on NeSI"
date = 2021-03-24T12:58:37+13:00
draft = false
weight = 10
+++



The Linux operating system was designed for multiple users, which makes it ideal for a server environment, and allows you to share your scripts and files with your colleagues. Here are some links and quick tips to getting your work going and letting others access your files. 

### Quick tip: getting your script running

Once you have written your script, in order to run it you have to make it *executable*. This is accomplished with one simple command:

```
chmod a+x
```

To break down the above command: `chmod` means 'change mode', and is the main command to change permissions. The `a` refers to all: that you are giving permission for anyone to use this script; the `+` is to add a permission, and the `x` is to make the file executable. 

For a full explanation of all the permission symbols, see [**this link**](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/)

### Making your script available system wide

Once you have your script, you can make it available so the computer can find it anywhere on the system. If you are submitting a job (slurm) script on NeSI, you can add something like the following to the slurm script:

```
export PATH='/nesi/project/uoo5555555/scripts/':$PATH
```

The script should be able to then find the script and run it (don't forget to make it executable). 

#### Symbolic links

If you have a folder that is already in the Path (e.g. /usr/local/bin), you can add a [**symbolic link**](https://www.shellhacks.com/symlink-create-symbolic-link-linux/) that adds the script to the existing path:

```
ln -s /path/to/file /path/to/symlink
```

### Sharing files and folders on the server

If you are using NeSI, the server is set up so that anyone on the same project can share files and folders in that project directory. If you need to join a project, go to [**this link**](https://support.nesi.org.nz/hc/en-gb/articles/360000693896-Applying-to-join-a-NeSI-project) for instructions.

On other servers, the defaults may be different, and you will have to change the permissions to add a user to one of your directories. A single command can allow everyone in your group access:

```
sudo chmod -R 775 /path/to/directory
```

Now run `ls -l` to see the change in permissions

The only issue is that future files that you create will assign the group to the default for your user account. There are two steps to keep all files written in this directory assigned to the group:

```
umask 0002

sudo chmod g+s /path/to/directory
```

The `umask` command is explained in detail [**here**](https://www.computerhope.com/unix/uumask.htm) and [**here**](https://linuxize.com/post/umask-command-in-linux/), and the special permissions command (`chmod g+s`) is explained [**here**](https://linuxconfig.org/how-to-use-special-permissions-the-setuid-setgid-and-sticky-bits).















