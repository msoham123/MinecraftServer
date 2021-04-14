# Soham's Minecraft Server

While the actually repository is used to save world data and settings, this README.md serves as a tool for me to document and explain how my Minecraft Server works.

## Section One - What is a Minecraft Server?

A Minecraft server is a player-owned or business-owned multiplayer game server for the 2009 Mojang video game Minecraft. These servers allow players of the game to play together without having to use a LAN to connect. 

## Section Two - Java and Paper

Minecraft is a Java program that can be run on Windows, Mac, and Linux. The server software is no exception to this and you need Java to run it. Mojang provides a minecraft server JAR that you can use to run your server. However, there are a myriad of community forks of this JAR, and I am using one called Paper. Paper is a high performance fork of the Spigot Minecraft Server that aims to fix gameplay and mechanics inconsistencies as well as to improve performance. I am using Paper as opposed to other alternatives because my server machine is not an enterprise level server: it is a low spec old laptop. 

(Note: I would highly reccomend installing a Linux Distrubition on your machine. It makes a later step so much easier.)

## Section Three - Hardware

Minecraft is now more than a decade old. It is no surprise that you do not need top of the line hardware to run a minecraft server. I am running my minecraft server on an old HP Envy Touchsmart Laptop, which will only cost you 129$ at the time of writing. This laptop is equipped with a low spec Intel Core I3 and a hard drive. Essentially, as long as your laptop has a decent x86 CPU from within the last six years, you will be able to run your Paper server on it.

![image](https://user-images.githubusercontent.com/51520568/114766157-eb75ab80-9d1a-11eb-8867-835d4571488c.png)

The next thing you need to consider is a). Your Internet b). Port Forwarding

I am running my Minecraft server with a 45 mbps (download) internet plan. This plan seems to be enough for the Minecraft server, and I do not experience rubber-banding (laggy teleportation) or ping spikes. If you have a plan that is lower, I would stil go ahead and try it out. According to servermania.com, Minecraft servers need a minimum of 15-20 mbps download and a 5-8 mbps upload to run optimally. 

The second component to configure is your router. Port forwarding enables an external source network or system to connect to an internal source node/port, which typically connects to Internet services and an internal private LAN (Local Area Network, or your router and the connected devices). So, we need to port forward in order for other people who are not connected to our network at home to connect from across the world. It is crucial that you port forward carefully, as port forwarding leaves your router susceptible to external attacks. Find your router model, your ISP, and research how to safely port forward. I have AT&T, and I used this [guide](https://www.youtube.com/watch?v=aTilhmo1vso).

## Section Four - Server Config

At this step, we can assume that you have your minecraft server running on your machine, and that it has been port forwarded succesfully. If you direct connect to your server in Minecraft, you should be able to join from anywhere. We need to configure a few things first before we give our IP address to friends or family. 

The first thing we need to do is configure the server itself. Go to the Paper folder, and find the `server.properties` file. Here, you can change a myriad of settings from gamemode to port (I'm using default). 

![image](https://user-images.githubusercontent.com/51520568/114766459-44ddda80-9d1b-11eb-849e-a5017d12bc73.png)

Once you have the configuration you desire, we need to whitelist the players that are going to join the server. Whitelisting essentially tells the server that these players are allowed to join, and is a second layer of security beyond your firewall. To whitelist, go to your `whitelist.json` file. If you are unfamiliar with the JSON format, read the [documentation](https://minecraft.fandom.com/wiki/Whitelist.json).

![image](https://user-images.githubusercontent.com/51520568/114766523-57f0aa80-9d1b-11eb-9e30-4d86312e3eca.png)

You can find the `uuid` key by inputing a username into this [website](https://mcuuid.net/).

## Section Five - Server Admin

There are two things we need to do to effectively administrate our server.

The first step does not require much config. Most Linux Distros have SSh (Secure Shell Protocol) installed. SSH allows you to connect to your machine from another machine from the same network. This saves you the trouble of walking back and forth to your server interface. To ssh, simply type `ssh <SERVER-NAME>@<IP>` on the machine that you are connecting to the server with. 

The server name is the name of your machine, which you can find in the settings of the server machine. To find the IP of your machine type `hostname –I` into the terminal of the machine (server) to get the IP.

If you are having trouble with SSH, please see this [guide](https://www.howtogeek.com/311287/how-to-connect-to-an-ssh-server-from-windows-macos-or-linux/).

Linux provides us with daemons, which are processes that we can init and deinit alongside the server. Read [this](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units) if you want to learn more about daemons and systemctl. What we need to do is fairly straightforward:

1). Create a `mcserver.service` file in your `/etc/systemd/system/` directory. 
This is what my file looks like. We can see that that the ExecStart param lauches a bash script. This bash script is explained in the second point.

![image](https://user-images.githubusercontent.com/51520568/114764644-0cd59800-9d19-11eb-91ab-213797204dc0.png)

2). The script I am launching using the mcserver service is located in my Paper file. I created it there to make it easier to access. We can see that the script is executing one command `java -Xms2G -Xmx4G -jar paper-1.16.5-439.jar nogui`. What does this mean? Well, the java prefix means that we are using java to run the .jar file for the server. The -Xms2G and -Xmx4G means that the server will use a minimum of 2GB of RAM and a maximum of 4GB. My machine only has 8GB of ram, so this is a good amount to allocate. The actual .jar file is the program that we are exuciting. Because the .jar file and script are in the same directory, I can access it directly. Finally, the nogui component means that the server will not open a window to display the program. The screen for our server will not be on, and we do not need a GUI (Graphical User Inteface) since we have our mcserver service. Therefore, we are saving resources by disabling gui.
![image](https://user-images.githubusercontent.com/51520568/114765116-a13ffa80-9d19-11eb-8f72-2b271872bbfe.png)

3). `mcserver.service` should start on boot. However, if you need to stop, restart, and start the service once again, here are the corresponding commands.
 - `systemctl status mcserver` gives you the status of the server
 ![image](https://user-images.githubusercontent.com/51520568/114766022-bcf7d080-9d1a-11eb-9393-29a3390f72d8.png)
 - `systemctl start mcserver` will start your server

 ![image](https://user-images.githubusercontent.com/51520568/114765930-9fc30200-9d1a-11eb-9eea-f7e927277832.png)
 - `systemctl stop mcserver` will stop your server
 - `systemctl restart mcserver` will restart your server 
 


