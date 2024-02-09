# Connecting to Research Drive on attie.diabetics

This guide provides instructions on connecting to a research drive mounted on `/mnt/rdrive/adattie/` on the server. Learn how to navigate to the drive using `cd` and copy files to/from the drive using `cp`.

## Navigating to the Research Drive

To access the research drive, use the `cd` (change directory) command.

1. Open your terminal.
2. Navigate to the research drive:

```bash
cd /mnt/rdrive/adattie/
```

Use the `ls` command to list files and directories within the current directory.

## Copying Files to the Research Drive

Use the `cp` command to copy files. The syntax is:

```bash
cp [options] source destination
```

### Example: Copying a File to the Research Drive

To copy `example.txt` from your home directory to the research drive:

```bash
cp ~/example.txt /mnt/rdrive/adattie/
```

## Copying Files from the Research Drive

To copy files from the research drive to another location, reverse the source and destination.

### Example: Copying a File from the Research Drive to the Home Directory

```bash
cp /mnt/rdrive/adattie/example.txt ~/
```
