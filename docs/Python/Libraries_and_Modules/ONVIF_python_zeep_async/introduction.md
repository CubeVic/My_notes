# `python-onvif-zeep-async`

![No_logo](images/onvif_zeep_async.png){: .center}

>ONVIF Client Implementation in Python 3 (using https://github.com/mvantellingen/python-zeep instead of suds as SOAP client)

1. [Pypi page](https://pypi.org/project/onvif-zeep-async/)
2. [Github page](https://github.com/hunterjm/python-onvif-zeep-async)

## How I use it/ How I find it

I was looking for libraries in python that can help me to get the video streaming form CCTV cameras, i run into a version of this project using non asynchronous "architecture"/"implementation" but i found this async version more suitable for what i want to achieve in my personal project `Project_Horus`.

The following example, will log in in a camera (we need to input the IP address) and get the profiles and save it in a .txt.

```python
from onvif import ONVIFCamera
import asyncio

async def fetch_profiles(cam_ip, cam_port, cam_user, cam_password ):
    mycam = ONVIFCamera(cam_ip, cam_port, cam_user, cam_password)
    await mycam.update_xaddrs()
    media_service = mycam.create_media_service()
    profiles = await media_service.GetProfiles()
    print(f'profile {profiles[0].Name} :\n {profiles[0]}')
    with open('profile.txt','w') as file:
        file.write(str(profiles))
    # token = profiles[0].token
    # print(token)
    return await mycam.close()

cam_ip = input("Camera IP: ")
cam_port = input("Camera cam_port: ") or 80
cam_user = input("Camera User: ") or 'admin'
cam_password = input("Camera password: ") or '123456'
asyncio.run(fetch_profiles(cam_ip, cam_port, cam_user, cam_password))
```
