## These scripts have been developed to help with getting your environment setup quickly and to help automate some of the initial scanning tasks that need to be performed.

### PortDiscovery

The `PortDiscovery` script takes arguments for an IP/hostname, then creates and writes to a user specified file that the scans will be written to, appending each subsequent scan to the file. It will then provide a list of options to scan the target machine. 

```
Select 1 to check if host is alive (-sn -vv)
Select 2 to run Port Discovery scan (-Pn -p- -T4 -vv)
Select 3 to run Service Enumeration scan (-Pn -sV -vv --stats-every 15s)
Select 4 to run Default Script scan (-Pn -sC -vv --stats-every 15s)
Select 5 to run Options 1-4 at once
Select 6 to run UDP Common Port scan (-sU)
Select 7 to exit         
```

Please note that Option 2 - Port Discovery Scan, must be ran prior to selecting options 3 and 4, since it uses the discovered ports in option 2 to specifically target those ports and services in options 3 and 4. 

Option 6 only scans the most common UDP ports, you may need to dig a bit deeper depending on the malevolence of the box creator.....

**Note**: These are only the initial scans. You will need to individually target services found using the `nmap scripting engine` to enumerate more about each service. Also, don't blindly run this script or any other script without first looking at it and verifying their content. Also, always test in a VM with a backup copy so if anything ever goes awry, you can just revert.   

### set_it_all

The `set_it_all` script provides the user with the ability to set the `ip_address` and `hostname` of the target machine in the `/etc/hosts` file. 

It also creates a `/tmp/target_ip.txt` file with the targets ip address. This is used to point to a Generic Monitor - Top Panel widget, which you will need to create.

It then reads the `/tmp/target_ip.txt` file every `5 seconds` (or whatever period you set it for) using `'Command 'cat /tmp/target_ip.txt'`  to display the targets IP address in the top panel. 

It also writes an entry into your `~/.zshrc` file that is the targets IP address. 
Run `source ~/.` to export the IP to the `$target` variable.

Now you can use the `$target` varible instead of typing out the IP address.

Examples:

`nmap -Pn -sC -p80 -vv $target`
`ping $target`
`nikto -h http://$target:8080/`


