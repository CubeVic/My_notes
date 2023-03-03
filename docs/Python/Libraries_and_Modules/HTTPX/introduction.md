#HTTPX
![HTTPX logo](images/butterfly.png){: .center}

>HTTPX is a fully featured HTTP client for Python 3, which provides sync and async APIs, and support for both HTTP/1.1 and HTTP/2.

1. [Pypi page](https://pypi.org/project/httpx/)
2. [Documentation](https://www.python-httpx.org/)

## How I use it/ How I find it

I run into this library trying to understand `python-onvif-zeep-async` and in order to know a bit more i decided to check it.
I haven't done anything with it yet, so i will leave just the first code developer shows in the documentation.

```python
import httpx
r = httpx.get('https://www.example.org/')
r
# <Response [200 OK]>
r.status_code
# 200
r.headers['content-type']
# 'text/html; charset=UTF-8'
r.text
# '<!doctype html>\n<html>\n<head>\n<title>Example Domain</title>...'

```
