# UFW 
[***go back to README***](README.md)

---

These are notes on this video by HackerSploit:
https://youtu.be/-CzvPjZ9hp8 

UFW is a utility that is designed to simplify the setup and management of
firewall rules, more specifically iptables rules. UFW allows you to easily and
succinctly control you various firewall rules. The main tool UFW uses to do
this is iptables. To get more context on what it does and how it's used:

    man ufw 

UFW is a service. You can start it, stop it, restart it, enable it to run on
startup and so on. Make sure you DO NOT enable the service before you configure
your firewall because you can lose access to it. To view the status of your
firewall:

    sudo ufw status

The default UFW configuration file is located in /etc/default/ufw. To disable
the service you can run:

    sudo ufw disable

It's always recommended when setting up a firewall, especially one on a server,
to set up everything from scratch because it's these types of rules that can 
really cause an issue. To start fresh, reset:

    sudo ufw reset

Don't worry, by default the program will back everything up before resetting.

You can get started by setting up the default policies. This is recommended for
every new configuration. The default policies are as follows:

- deny incoming connections 
- allow outgoing connections

The commands are:

    sudo ufw default deny incoming
    sudo ufw default allow outgoing

If outgoing connections don't work, you can disable the service completely:

    sudo systemctl stop ufw 

You disable everything, you set your rules and then you activate it. 

The next to understand is what services you want to keep active in regards to
incoming and outgoing connections and what services you want to prevent from 
being accessed. Imagine that you want http/https and ssh to work. To allow them
run:

    sudo ufw allow ssh OR sudo ufw allow 22
    sudo ufw allow http 
    sudo ufw allow https 

If you want to allow ftp:

    sudo ufw allow ftp
    
And so on and so forth. If you want to allow a particular connection from an IP
address explicitly:

    sudo ufw allow from 10.0.0.1

To deny all ssh connections except from one IP address:

    sudo ufw allow from 10.0.0.1 to any port 22

You can also specify an entire subnet:

    sudo ufw allow from 10.0.0.1/24 to any port 22
    
Make sure that when you set up individual IP addresses that they are static. If
they are dynamic, things are going to break because your addresses will change.

To start and enable a service at the same time:

    sudo systemctl enable --now ufw 
	sudo ufw enable

After enabling the service, you can now list the rules you have configured:

	sudo ufw status

If you want to delete certain rules, you should list them with indexes:

	sudo ufw status numbered

And then delete the unnecessary rules:

	sudo ufw delete <number>

Better to delete rules with bigger rule indexes first, so that the order does
not change each time you delete a rule. 
All incoming connections are blocked by default (if you used the rules above),
so if you don't explicitly allow access to some services (that is, their port
numbers), you won't have access to them.

Again, to allow a protocol use:

	sudo ufw allow <protocol-name or protocol-number>

To explicitly allow a particular IP address to a port:

	sudo ufw allow from <IP> to any port <port-number>
	
For example, you can limit SSH to a particular IP:

	sudo ufw allow from <IP> to any port 22

To deny traffic, for example ftp:

	sudo ufw deny ftp

To deny access from IP address:

	sudo ufw deny from <IP>

Keep in mind what things you want to allow and what you want to deny.

To reset UFW to get rid of all your rules:

	sudo ufw reset

If you reset your firewall, it will be turned off.

A few things to make clear:

- Set up your default policies first 
- Then explicitly define what policies you want to allow AND deny
- and only then enable the firewall

DON'T FORGET ABOUT ENABLING SSH!!! :)
