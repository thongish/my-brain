1. start by introducing myself
2. explain the assignment
	1. 
	2. creating 2 identical web servers and a load balancer connected to them
4. start by demoing script on droplet that's not set up yet
	1. explain that i have 2 droplets, one of them is configured to serve static html and file server via nginx
	2. the other i have yet to set up yet and will demo 
5. show working nginx server on droplet that was just set up
6. talk about the script
	1. webgen system user, why?
7. talk about systemd and unit files
	systemd is a service manager and also acts as the init system in most linux distributions
	services are background processes that run without a user interface
		they generally wait for events to occur and trigger some kind of response in return
		there are different types of 
		they are defined in plain text files called unit files
		placed in /etc/systemd/system/ because this directory is typically reserved for system-wide configuration files. placing our unit files in this directory ensures they are available to all users and are loaded automatically when the system boots
	1. services vs timers, targets, sections, directives
		1. targets are a set of services that are attached through dependencies that start all of the services required to meet a system state
			1. so network-online.target might mean a set of services that start to meet the requirement of the system network being online
		2. monotonic vs realtime timer
			monotonic timers start their service counter part based on a system even such as on boot
			realtime timers start based on calendar events. 
			the OnCalendar events follow this format:
			DayOfWeek Year-Month-Day Hour:MInute:Second
			OnCalendar=\*-12-25 00:00:00 <- christmas
			it's important to note that all times are based on UTC time
	1. how to check that a service ran correctly or if enabled or not
	2. systemctl status generate-index.service
	2. systemctl status generate-index.timer
1. briefly explain what nginx is
	1. free open source HTTP web server and reverse proxy software
	2. briefly go over nginx.conf
		1. user webgen; directive specifies which user will run the web server process
		2. include sites-enabled/\*; tells nginx to include all the server blocks inside the sites-enabled directory
	3. go over serverblock
		1. wild card specifies any server name, you can only have 1 of these server blocks
		2. talk about root and alias
			1. the file path to where files are served
		3. method of separating server blocks into separate files
		4. sites-available
		5. sites-enabled
		test nginx config with `sudo nginx -t`
1. talk about ufw <-  uncomplicated firewall
	1. firewalls are important for security because they can block incoming malicious traffic before it reaches the network as well as prevent sensitive information from leaving the network 
		by default ufw blocks all incoming traffic and allows all outgoing traffic 
	1. ssh, http, limit ssh
	2. we allow ssh so we can still ssh into our droplets
	3. we allow http so our web server can send out a response to http requests to our server
1. create load balancer and while it's loading go over a diagram
	1. explain static, dynamic
	2. load balancers choose which server to send requests to using either a static or dynamic algorithm
	3. static algorithms essentially send traffic based on a specific pattern like 1, 2 repeat
	4. dynamic algorithms send traffic based on more complicated parameters such as server load and health
2. show off load balancer at work

        autoindex on;                # Enables the directory listing
        autoindex_exact_size off;    # Shows file sizes, human-readable
        autoindex_localtime on;      # Displays file timestamps