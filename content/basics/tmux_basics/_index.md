---
title: "Tmux basics"
date: 2021-03-24T13:03:25+13:00
draft: false
weight: 10
---

tmux, or 'Terminal Multiplexer', is a very useful tool for using the command line. It has many, many tools, but the most important feature for starting out is that you can use it to run programs in the background while you are logged off. That is, you can start a long job, then log out of the server and go home, and tmux will keep the job running. Most of you are familiar with the program *screen* to accomplish this, but tmux is much more powerful. Below are a few commands to get you started. Once you are used to using it you can begin to explore more options. In the future we will try to keep this page updated with additional tips and tricks, but for now, here is one (of many) cheat sheets available online:

[tmuxcheatsheet.com](http://tmuxcheatsheet.com/)

## Starting and detaching from a session

### New Session

To start an unnamed session, you can just enter the name of the program at the prompt:

```bash
tmux 
```

I suggest you give a session a name when you start it, which will make it easier to keep track once you have multiple sessions going:

```bash
tmux new -s name_of_session
```

### Detach from a Session

To 'detach' or leave a session, you hold down the Control key and the 'b' keys at the same time, release, then press the 'd' key:

'''bash
Ctrl-b  d
'''

Note that the Control and b key action is referred to as a 'prefix' or 'chord', depending on the tmux guide. This action can be represented differently in different places. For example, on the link above, it is listed as "Ctrl + b  d. The prefix starts a lot of actions in tmux, but once you are used to it you will find it is easy. 

## Go back to existing session

If you have started a big job in tmux, and wish to re-enter it, or 'attach', it is:

```bash
tmux attach
```

or 

```bash
tmux a
```

This will go back to the last session. If you have named your session, you can specify this:

```bash
tmux a -t name_of_session
```

## Listing active sessions

You can list all your tmux sessions, even if you haven't named them:

```bash
tmux ls
```

Note naming your sessions will make it easier to know which you have. If you haven't named them, then they will be numbered. The names (or numbers) of sessions will be the first item when you list them

## Deleting active sessions

If you are finished with the job, and no longer need the session, then you can delete, or 'kill' it:

```bash
tmux kill-session -t name_of_session
```

If you do not specify a name of a session (no -t argument), then tmux will kill the last session made. 


