# Connecting Via SSH

- [Get access to the manifest group](#get-access-to-the-manifest-group)
- [Checking connection to network](#checking-connection-to-network)
- [Connect to the server](#connect-to-the-server)
- [Connect your VS Code to server](#connect-your-vs-code-to-server)
- [Connect your GitHub to server](#connect-your-github-to-server)
- [Connect R packages](#connect-r-packages)

## Get access to the manifest group

You will need to be added to the **BIOC-adattie-docker-admins** group. Please ask a current user to add you to the manifest [here](https://manifest.services.wisc.edu/Group/Index/1b018a1e44f5492b9af50a28fb75c2ac).

## Checking connection to network
To connect to the server, you must be on the biochem network in person or using the VPN.

To ensure that you are connected, try pinging the server using:
> ping -p 80 attie.diabetes.wisc.edu

## Connect to the server

Connect to the server using SSH
> `ssh [your wisc id]@wisc.edu@attie.diabetes.wisc.edu`

Your password is the same as your wisc password (NetID password). 

If you are having issues, make sure you are connected to the network and are apart of the manifest group.

## Connect your VS Code to server

Try reading
[Remote development over SSH](https://code.visualstudio.com/docs/remote/ssh-tutorial)
but it may prove confusing.
Here are key steps to do on your VS Code relevant to the Attie Server

- Be sure you have VPN connection to biochem network.
- Use Extension widget on left panel to add extension
[Remote- SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
- Use `CTRL-SHIFT-P` or menu `View -> Command Palette` and type `Remote-SSH: Connect to Host...`
- Click `+ Add New SSH Host...`
- type `ssh [your wisc id]@wisc.edu@attie.diabetes.wisc.edu`
- Return to `Command Palette` and click on `attie.diabetes.wisc.edu`.

This should open a new window on your computer that is running on the Attie Server.
Next time you can use the `Command Palette` or click on the `Remote Explorer` icon (`><` possibly with terminal screen) and select `attie.diabetes.wisc.edu`.
While you are connected to the Server, you should see a blue bar at the far bottom left of the VS Code window that reads " >< SSH: attie.diabetes.wisc.edu".

## Connect your GitHub to server

If you are doing development with GitHub, you will need to have SSH
connection between the server and your GitHub account.
There is a part you do in your home area on the server and a part you do
on you GitHub account.
They are arcane and involve several steps, but are quite doable.
Note that `pbcopy` does not seem to be on the Attie Server Linux;
you can simply copy-and-paste the old-fashioned way.

- Attie Server: See instructions at
[Generating a new SSH key and adding it to the ssh-agent (GitHub)](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
- GitHub: See instructions at
[Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## Connect R packages

Below, I replaced my home directory `/home/byandell@ad.wisc.edu` with `~`
for clarity.
In your case, your home directory will appear.

### Do not save workspace on exit from R

When you quit an R session, be sure to **not** save workspace image

```
> q()
Save workspace image? [y/n/c]: n
```

You can also quit with `q("no")` to eliminate the message.
You can set this as default by creating a `~/.Rprofile` file
in your home directory with the following one line:

```
formals(quit)$save <- formals(q)$save <- "no"
```

### Installing R packages you need for QTL work

Right now, the basic collection of R packages are installed on the Attie server.
You will need the following packages (at least, plus their dependencies) installed:

- `qtl2`
- `qtl2convert`

The default library paths can be found in R via the command

```
> .libPaths()
[1] "/usr/local/lib/R/site-library" "/usr/lib/R/site-library"      
[3] "/usr/lib/R/library"
```

Base packages are typically in `/usr/lib/R/library`, and `/usr/lib/R/site-library` is empty.
Packages added by the administrator are in `/usr/local/lib/R/site-library`;
it seems the Attie system currently has `tidyverse` and other packages installed there.
Ultimately, we will want `qtl2` and other relevant analysis and visualization
packages stored in that folder.

For now, each user must add their own verions of `qtl2` or other packages.
This 

```
> install.packages("qtl2","qtl2convert)
Installing package into ‘~/R/x86_64-pc-linux-gnu-library/4.4’
(as ‘lib’ is unspecified)
also installing the dependencies ...
```

If you are a regular user and this is the first time installing a package,
R will state something like, "You have no permission to write in `/usr/lib/R/library`.
If the folder `~/R/...` does not exist, R will first ask you if you want to create it.

This takes some time and generates a ton of output, because it requires installation
of several other packages and compilation of the `qtl2` package code.
These will automatically be placed in a folder in your home directory,
`~/R/x86_64-pc-linux-gnu-library/4.4/`,
where `4.4` is the current version of R.
You will see the folder `~/R` in your home directory; best to leave it alone
and store your material elsewhere.
After installing this (or other packages) locally, your search path changes:

```
> .libPaths()
[1] "~/R/x86_64-pc-linux-gnu-library/4.4"
[2] "/usr/local/lib/R/site-library"                               
[3] "/usr/lib/R/site-library"                                     
[4] "/usr/lib/R/library"
```

Note that your local library will be searched first.
If Attie Lab later installs a common version of `qtl2` or other packages,
you will want to remove those from your library.
You can examine the contents of your local library with `ls`.

```
$ ls ~/R/x86_64-pc-linux-gnu-library/4.4/
qtl  qtl2  qtl2convert  RcppEigen  RSQLite
```
