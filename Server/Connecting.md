# Connecting Via SSH
## Get access to the manifest group
You will need to be added to the **BIOC-adattie-docker-admins** group. To do the please ask a current user to add you to the manifest [here](https://manifest.services.wisc.edu/Group/Index/1b018a1e44f5492b9af50a28fb75c2ac).

## Checking connection to network
To connect to the server, you must be on the biochem network in person or using the VPN.

To ensure that you are connected, try pinging the server using:
> ping -p 80 attie.diabetes.wisc.edu

## Connect to the server

Connect to the server using SSH using ssh
> `ssh [your wisc id]@wisc.edu@attie.diabetes.wisc.edu`

Your password is the same as your wisc password. 

If you are having issues, make sure you are connected to the network and are apart of the manifest group.

## Connect your VS Code to Server

Try reading
[Remote development over SSH](https://code.visualstudio.com/docs/remote/ssh-tutorial)
but it may prove confusing.
Here are key steps to do on your VS Code relevant to the Attie Server

- Be sure you have VPN connection to biochem network.
-  Use Extension widget on left panel to add extension
[Remote- SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
- Use `CTRL-SHIFT-P` or menu `View -> Command Palette` and type `Remote-SSH: Connect to Host...`
- Click `+ Add New SSH Host...`
- type `ssh [your wisc id]@wisc.edu@attie.diabetes.wisc.edu`
- Return to `Command Palette` and click on `attie.diabetes.wisc.edu`.

This should open a new window on your computer that is running on the Attie Server.
