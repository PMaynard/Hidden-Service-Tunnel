# Hidden Servier Tunnel with port knocking

This script will configure two services Tor, and Knockd.

Tor will be configured to setup a hidden service, exposing port 22 inside Tor's network. Make sure to add the Hidden service authentication to the client's torrc.

```/var/lib/tor/hidden_service/hostname``` contains the connection information.

	2dpiuqpmvb3pypis.onion dW/yhnk29udp/4plOKn19J1 # client: client-secrect
			^					^								^
			|					|								|
		Hostname			 cookie							   auth

Client's Torrc:

	HidServAuth 2dpiuqpmvb3pypis.onion dW/yhnk29udp/4plOKn19J1 client-secrect

Knockd, will configure the firewall (UFW) to open the ssh port for the specific IP address and close it after 120 seconds.

## SSH Tips

Setup Tor to work on your client machine, add the following to ~/.ssh/config

	Host *.onion
		ProxtCommand /bin/nc -xlocalhost:9050 -X5 %h %p

