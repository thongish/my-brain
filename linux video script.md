hi my name is kevin pham and this is my video for assignment 3 where i will be creating 2 identical nginx web servers and a load balancer connected to them

The first thing we'll need is 2 droplets that will serve as our nginx web servers
here i have 2 droplets where one of them is already has a nginx web server already set up
- show working web server
the other will be used to demonstrate my setup script
- show not working web server

so we'll go ahead and set up this droplet with my script from my repository
- go to droplet git clone 
- cd into the directory
- run `sudo ./setup-script`
- check server is working
---
So now we'll take a look at the script and see what it's doing
- show script
this script is split up into 4 parts

the first part sets up a new system user called webgen which will be used to handle all the nginx tasks
We're creating a system user here because it adds an extra layer of security 
by creating webgen as a system user we can essentially essentially ensure that whatever task webgen is supposed to carry out, it is the only user that can perform those tasks other than the root user
the script also sets up the directory structure which nginx will use to serve files and html

- show tree of /var/lib/webgen
this is what the directory structure looks like

we have a bin, documents, and HTML directory

the script copies this generate_index script from my repository into the bin directory

it will also copy over 2 sample files into the documents directory which will be used to test that our web server can serve downloadable files

the index.html file in the HTML directory will serve as our web servers home page

--- 
- go back to script
the second part of this script sets up some systemd unit files

systemd is service manager that also acts as the init system in most linux distributions

services are background processes that run without a user interface

they are defined within plain text files called unit files

they generally wait for events to occur and trigger some kind of response in return 

there are many different types of unit files but we'll just be looking at the service and timer types for this assignment

these custom unit files should be placed in the /etc/systemd/system directory because this directory is typically reserved for system-wide configuration files

placing our unit files in this directory ensures they are available to all users and are loaded automatically when the system boots

so this script copies over the unit files into /etc/systemd/system 

and then we run systemctl daemon-reload because systemd doesn't automatically see the changes we've made to this directory or the files in the directory

then we start the generate-index.service to create an initial index.html for our web server to serve

and then we start and enable the generate-index timer

--- 
let's take a look at our generate-index service

- go to generate-index.service

unit files are comprised of two things:
sections and directives

sections are words wrapped in square brackets

everything underneath the sections are the directives

as you can see inside the unit section we have a description directive

this is where you can give a description to the service

then we have the requires directive which tells systemd that this service is dependent on the network-online.target starting

the after directive tells systemd to start this service only after the network-online.target has finished running

it's important to note that if we don't specify the after directive, this service would start simultaneously alongside the network-online.target services

targets are sets of services that are attached through dependencies that start all of the services required to meet a system state

so in this case we could think of the network-online target as a set of services that run until the system reaches a state where the network is online

in the service section, which is a service type specific section

we specify the user and group that this service will be run by which would be our webgen system user

the execstart directive tells systemd to execute a command or script when this service is started

---

now let's take a look at the timer unit file associated with this service

- go to generate-index.timer

one thing to note is that there are two types of timers monotonic and realtime timers

monotonic timers start their service counter part bsed on a system event such as, on boot

realtime timers start based on calendar events
which is defined in the OnCalendar directive

this directive follows the format of:
dayofweek year month day hour minute seconds
so for example if we wanted to create an on calendar event that triggers on christmas we would

set the year to any year, the month to 12, the day to 25 and 00 hours 00 minutes and 00 seconds

the persistent=true directive ensures that if the system were to be down when this timer is supposed to go off, systemd would start this timer as soon as the system is back up

and the install section is where we set this timer as a dependency to a boot target. 

in this case we specify that this timer unit file is a dependency of the timers target

we're essentially adding this timer into the set of services the timers target needs to run to reach it's intended state

---
- go back to script
the next part of the script sets up our nginx configuration files

nginx is a free and open source HTTP web server and reverse proxy software that allows us to quickly set up web servers

let's go over to the main nginx configuration file

- go to nginx.conf

This configuration is the default configuration except for 2 lines

the first line is this user directive which states which user runs the nginx processes

the second line is inside this http  block and it says to include all server blocks from inside the sites-enabled directory

a server block is a configuration section within nginx that defines how the server the server should handle requests for a specific domain

an example of one is inside this http block here

this one says to listen on port 80 which is the HTTP port and the domain name is localhost

we can define as many server blocks as we want inside of this main nginx configuration file but it's much more convenient to separate the blocks

this is why we've included all the server blocks within the sites-enabled directory

let me elaborate

- show nginx tree

my script creates two folders called sites-available and sites-enabled

the sites available directory holds all of the available server blocks on the system but they remain dormant until a we create a symbolic link from the server block to sites-enabled 

this allows us to turn servers on and off by creating and unlinking symbolic links

----

now let's take a look at a custom serverblock

-go to assignment3-serverblock.conf

in this server block we can see it's listening on the HTTP port 80

this second listen directive is listening for ipv6

in this servername we used a wild card which tell nginx that the domain name can be anything

it's important to note that only 1 enabled serverblock should use the wildcard otherwise you'd run into issues

this location forward slash is essentially a route for when someone visits the server home page

the root directive is the path to where nginx can find the index index.html

this second location /documents is another route where users can download the two sample files copied into the webgen directory

it's important to note that when you use the root directive, the location route will append to the end of the root file path.

so when users go to this route, nginx will look for files in the var/lib/webgen/docuemnts directory

the autoindex directive enables the directory listing

the autoindex exact size = off will show file sizes in human readable format

the autoindex-local time directive will display file timestamps

---

- go to script
the last part of the script sets up ufw which stands for uncomplicated firewall

firewalls are important for security because they can block incoming malicious traffic before it reached the network as well as prevent sensitve information from leaving the network

by default ufw blocks all incoming traffic and allows all outgoing traffic

the first command we run is ufw allow ssh which will allow incoming and outgoing ssh requests to this server


the 2nd command we limit ssh. this denies incoming an incoming address if they attempt to connect more than 6 times within 30 seconds

the 3rd command we allow http

this is necessary because we want our web server to receive incoming http requests

and finally we enable ufw

---
now that the we've explained what's going on in the script we can go ahead and make a load balancer

so a load balancer basically routes requests to 

load balancers basically routes requests to servers that are connected to it from a client
it acts as a middle man between the client and your server
the load balancer chooses which server to send requests to based on algorithms
static algorithms basically send traffic based on a specifc pattern like 1, 2 repeat

dynamic algorithms send traffic based on more complicated parameters such as server load and health

for example if server 1 was heavily loaded the load balancer would start sending requests to server 2

load balancers are also useful if you want a backup server 

if server 1 went down there would still be server 2 to process requests and responses




