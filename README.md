# Distributed Systems Practice

Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

## Area 1: Cloud Web Apps

> Beginner Level

[AWS Tutorial: Launch a VM](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/) (time: 30 min)

Notes: In this lecture, I have learned how to lauch, configure, connect, and terminate an instance in the cloud. Besides, I have learned 2 linux commands:  `chmod` and `ssh` :

- chmod xxx filename . Change the access permissions, **ch**ange **mod**e. 3 digits stand for: user, group, and world. 4 means read, 2 means write, 1 means execute.

```
chmod 400 file.txt    // allow read by owner
chmod 740 file.txt     // allow read, write, execute by owner, allow read by group
chmod 777 file.txt    // allow everyone to read, write, and execute file
```

- ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine.

```
ssh -i file [user@]hostname	// here, -i means selecting a file from which the identity for RSA is read.
```

[QwikLab: Intro to S3](https://awseducate.qwiklabs.com/focuses/30?parent=catalog)

## Area 2

> Include notes here about each of the links
