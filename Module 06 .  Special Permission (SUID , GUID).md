## Linux permissions: SUID, SGID

Linux permissions are a concept that every user becomes intimately familiar with early on in their development. We need to execute scripts, modify files, and run processes in order to administer systems effectively, but what happens when we see Permission denied? Do you know why we see this message? If you know the cause of the problem, do you know how to implement the solution?

Skip to the bottom of list
Career advice
Take a sysadmin skills assessment
Explore training and certification options
Red Hat Certification remote exams FAQ
10 resources to make you a better communicator
How to explain modern software development in plain English
Learning path: Getting started with Red Hat OpenShift Service on AWS (ROSA)
I will give a quick explanation of the various ways to calculate permissions, and then we will focus on the special permissions within Linux. If you want an in-depth look at the chmod command, check out this article from Sudoer Shashank Hegde, Linux permissions: An introduction to chmod.

### Symbolic method

The symbolic method uses the following syntax:

```bash
[tcarrigan@server ~]$ chmod WhoWhatWhich file | directory
```

Where:

- Who - represents identities: u,g,o,a (user, group, other, all)
- What - represents actions: +, -, = (add, remove, set exact)
- Which - represents access levels: r, w, x (read, write, execute)

An example of this is if I want to add the read and write permissions to a file named test.txt for user and group, I use the following command:

```bash
[tcarrigan@server ~]$ chmod ug+rw test.txt
```

Full disclosure, this is not my preferred method of assigning permissions, and if you would like more information around this method, I recommend your nearest search engine.

### Numeric method
The numeric method is, in my experience, the best way to learn and practice permissions. It is based on the following syntax:

```bash
[tcarrigan@server ~]$ chmod ### file | directory
```

Here, from left to right, the character # represents an access level. There are three access levels—user, group, and others. To determine what each digit is, we use the following:

- Start at 0
- If the read permission should be set, add 4
- If the write permission should be set, add 2
- If the execute permission should be set, add 1

This is calculated on a per access level basis. Let's interpret this permissions example:

```bash
[tcarrigan@server ~]$ chmod 650 test.txt
```

## Special permission explained

Special permissions make up a fourth access level in addition to user, group, and other. Special permissions allow for additional privileges over the standard permission sets (as the name suggests). There is a special permission option for each access level discussed previously. Let's take a look at each one individually, beginning with Set UID:

## user + s (pecial)

Commonly noted as SUID, the special permission for the user access level has a single function: A file with SUID always executes as the user who owns the file, regardless of the user passing the command. If the file owner doesn't have execute permissions, then use an uppercase S here.

Now, to see this in a practical light, let's look at the /usr/bin/passwd command. This command, by default, has the SUID permission set:

```bash
[tcarrigan@server ~]$ ls -l /usr/bin/passwd 
-rwsr-xr-x. 1 root root 33544 Dec 13  2019 /usr/bin/passwd
```

Note the s where x would usually indicate execute permissions for the user.

## group + s (pecial)
Commonly noted as SGID, this special permission has a couple of functions:

- If set on a file, it allows the file to be executed as the group that owns the file (similar to SUID)

- If set on a directory, any files created in the directory will have their group ownership set to that of the directory owner

```bash
[tcarrigan@server article_submissions]$ ls -l 
total 0
drwxrws---. 2 tcarrigan tcarrigan  69 Apr  7 11:31 my_articles
```
This permission set is noted by a lowercase s where the x would normally indicate execute privileges for the group. It is also especially useful for directories that are often used in collaborative efforts between members of a group. Any member of the group can access any new file. This applies to the execution of files, as well. SGID is very powerful when utilized properly.

As noted previously for SUID, if the owning group does not have execute permissions, then an uppercase S is used.
