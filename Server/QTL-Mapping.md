# QTL Mapping

## Setup for Running QTL Scans

These notes assumes you know how to

- [Connect to Attie Server via SSH](Connecting.md)
- [Connecting to Research Drive on attie.diabetics](research-drive.md)

This setup is for using VSCode on the Attie Server.
Example below uses notes from
[22 Jan meeting](https://github.com/AttieLab-Systems-Genetics/qtl_mapping/blob/main/Meeting_Minutes.md#15-Jan-2025)
led by Kelly Mitok.

1. ResearchDrive: Set up your projects folder in ResearchDrive folder, which will contain subfolders for individual projects.
For instance, Kelly has her `cpep_and_ins` from mouse build 39 in
`/mnt/rdrive/mkeller3/General/QTL_mapping_KM/DO_diet_GRCm39/cpep_and_ins`.
    - Create projects folder `/mnt/rdrive/mkeller3/General/QTL_mapping_XX`, with `XX` being your initials.
    - Create subfolders for each separate project with easily identified names.
      Use further subfolders if needed, but be mindful of navigation.
    - Include `README` file in your main folder, and subfolders, to identify contents and aid navigation.
    - Set up configuration and data files in your individual project folder (say `.../cpep_and_ins`).
The file `config.yml` has all the setup points to all needed files and folders.
        - config: `config.yml`
        - trait_file: `run_these_phenotypes.csv`
        - covariate_file: `use_these_covariates.csv`
        - mouse_file: `use_these_mice.csv`
2. Attie Server: Set up local folders on the server in your home director (`~`).
    - `/home/data/mapping_data`
        - this is already created with read-only files for all users
    - For each project, have a folder for QTL output
        - `~/QTL_mapping_KM/DO_diet_GRCm39/cpep_and_ins`
        - Note convention of matching local names with ResearchDrive names to help navigation
    - Clone one local copy of GitHub repo for local use
        - `~/qtl_mapping`: user clone of GitHub repo
        - <https://github.com/AttieLab-Systems-Genetics/qtl_mapping>
5. Run QTL scan wrapper
[QTL_scan_wrapper.R](https://github.com/AttieLab-Systems-Genetics/qtl_mapping/blob/main/scripts/latest/QTL_scan_wrapper.R)
from your local copy.

```
cd ~/qtl_mapping/scripts/latest
./QTL_scan_wrapper.R --config="/mnt/rdrive/mkeller3/General/QTL_mapping_KM/DO_diet_GRCm39/cpep_and_ins/config.yml`
```

or in one line

```
~/qtl_mapping/scripts/latest/QTL_scan_wrapper.R --config="/mnt/rdrive/mkeller3/General/QTL_mapping_KM/DO_diet_GRCm39/cpep_and_ins/config.yml`
```

## Symbolic Links and Home Directory

Your home directory is `~` = `/home/[NetID]@ad.wisc.edu` (with `[NetID]` replaced by your NetID.
You can usually use `~` as shorthand, which is helpful for scripts used across machines.
This is where you land when you SSH to the Attie Server.

[Symbolic links](https://www.freecodecamp.org/news/symlink-tutorial-in-linux-how-to-create-and-remove-a-symbolic-link/)
are a handy way to condense folder paths to ResearchDrive and other places.
Use them sparingly, and they can be helpful.
Below are commands to set up a symbolic link for `~/RD` and two project folders,
a local folder `~/QTL_mapping_BY`, and a folder on ResearchDrive `~/main_directory/QTL_mapping_BY`.

```
$ cd
$ ln -s /mnt/rdrive/mkeller3/General RD
$ mkdir ~/RD/QTL_mapping_BY
$ mkdir QTL_mapping_BY
$ ls -l ~
```

The `ls` command shows the contents of my home directory

```
total 0
drwxr-xr-x 2 byandell@ad.wisc.edu domain users@ad.wisc.edu  6 Jan 23 09:27 QTL_mapping_BY
lrwxrwxrwx 1 byandell@ad.wisc.edu domain users@ad.wisc.edu 28 Jan 23 09:37 RD -> /mnt/rdrive/mkeller3/General
```


