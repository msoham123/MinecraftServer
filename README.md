# Soham's Minecraft Server

While the actually repository is used to save world data and settings, this README.md serves as a tool for me to document and explain how my Minecraft Server works.

## Section One - What is a Minecraft Server?

A Minecraft server is a player-owned or business-owned multiplayer game server for the 2009 Mojang video game Minecraft. These servers allow players of the game to play together without having to use a LAN to connect. 

## Section Two - Java and Paper

Minecraft is a Java program that can be run on Windows, Mac, and Linux. The server software is no exception to this and you need Java to run it. Mojang provides a minecraft server JAR that you can use to run your server. However, there are a myriad of community forks of this JAR, and I am using one called Paper. Paper is a high performance fork of the Spigot Minecraft Server that aims to fix gameplay and mechanics inconsistencies as well as to improve performance. I am using Paper as opposed to other alternatives because my server machine is not an enterprise level server: it is a low spec old laptop. 

## Section Three - Hardware

Minecraft is now more than a decade old. It is no surprise that you do not need top of the line hardware to run a minecraft server. I am running my minecraft server on an old HP Envy Touchsmart Laptop, which will only cost you 129$ at the time of writing. This laptop is equipped with a low spec Intel Core I3 and a hard drive. Essentially, as long as your laptop has a decent x86 CPU from within the last six years, you will be able to run your Paper server on it.

The next thing you need to consider is a). Your Internet b). Port Forwarding

I am running my Minecraft server with a 45 mbps (download) internet plan. This plan seems to be enough for the Minecraft server, and I do not experience rubber-banding (laggy teleportation) or ping spikes. If you have a plan that is lower, I would stil go ahead and try it out. According to servermania.com, Minecraft servers need a minimum of 15-20 mbps download and a 5-8 mbps upload to run optimally. 

The second component to configure is your router. Port forwarding enables an external source network or system to connect to an internal source node/port, which typically connects to Internet services and an internal private LAN (Local Area Network, or your router and the connected devices). So, we need to port forward in order for other people who are not connected to our network at home to connect from across the world. It is crucial that you port forward carefully, as port forwarding leaves your router susceptible to external attacks. Find your router model, your ISP, and research how to safely port forward. I have AT&T, and I used this [guide](https://www.youtube.com/watch?v=aTilhmo1vso).
