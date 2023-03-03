# Netifaces
![no logo](images/netifaces.png){: .center}

The authors or maintainers [alastair](https://pypi.org/user/alastair/) and [opalmer](https://pypi.org/user/opalmer/) made an excellent description so i will just copy it.

> It’s been annoying me for some time that there’s no easy way to get the address(es) of the machine’s network interfaces from Python. There is a good reason for this difficulty, which is that it is virtually impossible to do so in a portable manner. However, it seems to me that there should be a package you can easy_install that will take care of working out the details of doing so on the machine you’re using, then you can get on with writing Python code without concerning yourself with the nitty gritty of system-dependent low-level networking APIs.
This package attempts to solve that problem.

1. [Pypi page](https://pypi.org/project/netifaces/)
2. [Github page](https://github.com/al45tair/netifaces)

## How I use it/ How I find it

I wanted to find a way to get the IP address of the computer running the python code, the idea was use it as part of my personal project `Project_horus` as part of the discovery devices.

```python
from netifaces import interfaces, ifaddresses, AF_INET

# AF_INET - Address Family - Normal internet address

#Todo:
"""set logging system for this script"""
print(f'\n Interfaces: {interfaces()} \n------------>\n')

def extract_scope_(interface):
	""" it willl filter the Ethernet/internet interface
	and return just the IP address """
	if AF_INET in ifaddresses(interface):
		print(f'interface {interface} : {ifaddresses(interface)[AF_INET]}')
		ip_address = ifaddresses(interface)[AF_INET][0]['addr']
		return ip_address


scope = None

# extrat the IP "scope" of the IP range of the Ethernet interface
if not scope : ips = list(map(extract_scope_,interfaces()))

# Extract the first two numbers of the address
scope = ['.'.join(ip.split('.')[:2]) for ip in ips if ip]

print(f'\n------------>\nscope {scope}') #the scope,
# ['127.0', '192.168']
```
