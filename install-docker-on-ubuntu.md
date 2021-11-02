# This is a guide for installing a specific version of docker on Ubuntu linux

# THIS IS ARCHITECTURE SPECIFIC ! watch out for your processor (ARM / intel / AMD) and x32 / x64 bit as well as the flavor of your OS


## now let's get started
# open a terminal on your ubuntu 20 system
# we first will clear any docker versions just in case
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```
# extra tidying up
```
sudo apt autoremove
```
# update the package registry
```
sudo apt update
```
# run this block command
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
# get certificates installed for interacting with docker repo
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
# add docker key
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
## lets check what flavor Ubuntu you are running
```
cat /etc/lsb-release
```
# Add the correct Docker repository to APT sources:  
## (WATCH THE VERSION , IM ON 64 bit AMD processor with UBUNTU FOCAL)
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
## force install from the place we linked instead of default ubuntu
```
apt-cache policy docker-ce
```
#it should list out available versions, if they look okay go ahead and install
```
sudo apt install docker-ce
```
#check the status
```
sudo systemctl status docker
```
# if it says running then awesome! you can close out with ctrl+c
# open a new terminal, then make sure you are in the root directory by typing cd
```
cd
```
# list file system by typing ls
```
ls
```
# now out of the list, change directory to documents
```
cd Documents
```
# make a folder (you can change the name)
```
mkdir docker-projects 
```
# change into the folder you made
```
cd docker-projects
```
# now we will run hello-world to make sure everything works, if it pops stuff into the terminal then its working!
```
docker run hello-world
```
# Oops... mine is denied :( that's because we didn't set up docker group to access things without the power of sudo
# you can be naughty and just put sudo in front of the command - or be safe and make the docker user
```
sudo usermod -aG docker ${USER}
su - ${USER}
groups
```
# if groups shows docker, you're set now. navigate back to the docker folder from root/$
```
cd Documents
cd docker-projects

docker run hello-world
```
## congrats!!! if it didn't work, I recommend digitalocean's guide, 
# it's a little less wordy than dockers official docs
# https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04

# So why is this cool? well first off, your computer didn't have hello-world, 
# docker figured that out right away and went and grabbed the official up to date copy, 
# pulled it down, and launched it as a service
# if you're curious what else docker can find and pull for you use search before pull
```
docker search node
```
# this should yield a list of image options for node images
# other images are available on github and docker hub ... in general well rated or officially supported projects in docker hub are a breeze to use and pull
# A powerful tool to dockerize is node - a fabulous server and package manager
# Node projects might take different packages and different versions though which is why its good to containerize!
# docker pull node would work , but i'm working on an app using node 14 LTS

# we can pull the specific version like this
```
docker pull node:14.4-alpine3.11
```
# to see what images have been pulled type 
```
docker images
```
# run the ubuntu image with -i and -t for shell access
# (replace imageid with one from the 'docker images' list )
```
docker run -it IMAGEID

# I did docker run -it and the image id for node 14.4 alpine
# the result was it popped up super fast with a node command prompt!
```
## what is cool about this? 
# well , you didn't (need to) use sudo , but then docker created a linux image and ran it without being root, 
# but now gave you a shell inside ubuntu that IS root. if they both have internet access maybe you can see how powerful this can be! 
# containers in containers!!! rent your PC infrastructure out to the mice in your closet!!! etc!!! :DDDD
# you can ctrl+tab away and use a different terminal or use ctrl+c in a running docker shell to close out
# you can run multiple images at a time if your computer can handle it
# to check which containers you have going 
```
docker ps
```
# to view all containers, including inactive ones
```
docker ps -a
```
# to start a container again use this line, replacing container id with one from the 'docker ps -a' list
```
docker start 'CONTAINER ID'
```
# for other general container operations see the main cheat-sheet repository file "docker commands"
