# WS-Dicovery in Python


>This is WS-Discovery implementation for Python 3. It allows to both discover services and publish discoverable services. For Python 2 support, use the latest 1.x version of this package.

1. [Pypi page](https://pypi.org/project/WSDiscovery/)
2. [Documentation](https://python-ws-discovery.readthedocs.io/en/latest/#)

## How I use it/ How I find it

I wanted to understand some of the implementation of `python-onvif-zeep-async` so I decided to take a look to the libraries use on it, and this was one of those libraries 

```python
from wsdiscovery.discovery import ThreadedWSDiscovery as WSDiscovery
from wsdiscovery import Scope
import re


base = 'onvif://www.onvif.org/'
profile_scope = base + 'Profile/'


scope1 = Scope(base) # to be use later to filter just those with ONVIF services
scope2 = Scope(profile_scope)

def fetch_devices(services):
	for service in services:
	#filter those devices that dont have ONVIF service
	# print(f'\nAddress:\n{service.getXAddrs()[0]}\n')
		ipaddress = re.search('(\d+|\.)+', str(service.getXAddrs()[0])).group(0)
		print(f'\nIP Address: {ipaddress}')
		for scope in service.getScopes():
			#Scope methods getMatchBy, getQuotedValue, getValue
			print(scope.getValue())
	print(f'\nnumber of devices detected: {len(services)}')

wsd = WSDiscovery()
wsd.start()
# devices_services = wsd.searchServices(scopes=[scope1])
devices_services = wsd.searchServices()

fetch_devices(devices_services)

wsd.stop()
```