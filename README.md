# Mirai for Docker
Create your own Mirai botnet using Docker. 

## Pre-compiled Binaries
For use with Ubuntu 14.04 x64. For the source code, please refer to: [mirai](https://github.com/lejolly/mirai)

## Prerequisites
1. Docker Swarm
2. Portainer (used for managing the swarm, you can of course use the command line if you prefer but you'll have to translate the commands yoruself)

## Instructions
1. Clone this repository. 
2. In each of the `docker-bot` and `docker-cnc` directories, build the corresponding image
	- e.g. for the cnc: `$ sudo docker build -t cnc .`
	- e.g. for the bot: `$ sudo docker build -t bot .`
3. Create the botnet network in Portainer
	- Name: `botnet`
	- Subnet: `172.20.0.0/16`
	- Gateway: `172.20.0.1`
	- Driver: `overlay`
	- Driver options: `com.docker.network.bridge.enable_icc:true`
4. Start the cnc service in Portainer
	- Name: `cnc`
	- Image: `cnc:latest`
	- Mode: `Replicated`
	- Replicas: `1`
	- Port Mapping: `Host:8080`, `Container:23`, `TCP`
	- Network: botnet
5. Start the bot service in Portainer
	- Name: `bot`
	- Image: `bot:latest`
	- Mode: `Replicated`
	- Replicas: `<up to you, a safe estimate is 1 bot per CPU core>`
	- Network: `botnet`
6. Connect to the cnc
	- Telnet to the mapped port (`8080`)
	- Username: `root`
	- Password: `root`
	- Login credentials can be changed via the last line in  [db.sql](docker-cnc/db.sql)
	- Launch an attack (for more details refer to: [mirai](https://github.com/lejolly/mirai))
