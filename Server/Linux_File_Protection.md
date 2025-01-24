# Linux File Protection

I think it is about time to protect the files in `/home/data` on the Attie Server
that are our primary copies and that multiple people are accessing.
These should be readable (and maybe executable) by everyone but only writeable by a select group.

I don’t know how much you know about Linux groups.
[File Permissions in Linux (FreeCodeCamp](https://www.freecodecamp.org/news/file-permissions-in-linux-how-to-use-the-chown-chgrp-command-s/))
seems to be somewhat helpful, and the 
[CoreUtils Manual](https://www.gnu.org/software/coreutils/manual/html_node/)
seems to be comprehensive.

Groups are maintained in the file `/etc/group`,
where you will see that the docker group is the only one with specific names attached.
Here are its members:

```
$ getent group docker
docker:x:999:bioadmin,biochem-ansible,yjherr@ad.wisc.edu,mekassel@ad.wisc.edu,
mkeller3@ad.wisc.edu,ruotti@ad.wisc.edu,emfinger@ad.wisc.edu,
bioc-adm-yjherr@ad.wisc.edu,khwillis@ad.wisc.edu,khwillis@wisc.edu
```

A superuser can create a new group (that should be distinct from existing system groups),
such as `qtl2-dev`, which could have only you two in it (and maybe Chris or ???).
You would want to discuss this with Biochem gurus before proceeding of course.

Switching gears, the directory `/home/data` has the following permissions

```
/home/data$ ls -lha
total 20K
drwxrwxrwx  8 root                 root                      123 Jan 13 20:05 .
drwxr-xr-x 27 root                 root                     4.0K Dec  4 13:44 ..
drwxr-xr-x  3 ruotti@ad.wisc.edu   domain users@ad.wisc.edu  147 Jan 13 20:41 condor
drwxrwxrwx  2 ruotti@ad.wisc.edu   domain users@ad.wisc.edu    6 Dec 10 11:30 input_data
drwxrwxrwx  7 emfinger@ad.wisc.edu domain users@ad.wisc.edu  165 Jan 10 09:36 Islet_DO_newscans
drwxrwxrwx  3 ruotti@ad.wisc.edu   domain users@ad.wisc.edu 4.0K Jan 17 16:24 mapping_data
drwxr-xr-x  2 ruotti@ad.wisc.edu   domain users@ad.wisc.edu  328 Jan 10 10:23 raw_data
drwxrwxrwx  3 ruotti@ad.wisc.edu   domain users@ad.wisc.edu 8.0K Jan 23 12:09 scans_cross_test
```

That is, the owner is root and the group is domain (`domain users@ad.wisc.edu`).
I see that `raw_data` is set for read/execute only (`r-x`) for both everyone else,
which means only root can modify folder contents.
That is, `rwxr-xr-x` specifies for owner (first triplet),
group (second triplet) and other users (third triplet).
The command `chmod` can be used to change this either with a number (755)
or character shorthand (see links).
Of course, this should be done recursively (`-R`) to set all files below that folder.

I think `mapping_data` should be changed either to `rwxrwxr-x` (775) or `rwxr-xr-x` (755).
The danger right now, with `rwxrwxrwx` is that one of our users could accidentally
alter or remove a file, affecting everyone else.
The latter setting would mean only the owner (root) can write, which means whoever modifies
the folder must become user “root” first.
Maybe you want that? Alternatively, using the former permissions `rwxrwxr-x` (775)
would be useful if `/home/data/mapping_data` had group `qtl2-dev` (or some such),
in which case you would not have to `sudo` to root in order to modify the directory contents.
You would have to change group of folder (`chgrp -R …`) after setting up the group
and adding limited users to the group.
