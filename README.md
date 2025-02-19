# Simwood Partner Python Client

A modern Python client library for Sipcentric
([Simwood Partner](https://simwood.com/uk/partner/), formerly Nimvelo)
[API](https://developer.simwood.com/docs/direct/introduction/).

```python
from sipcentric import Sipcentric
api = Sipcentric(username="myusername", password="mypassword")
print api.sms.post(_from="0123", to="03301201200", body="Hello World!")
```

## Install

### Best method

```
sudo pip install sipcentric
```

*You may need to install `simplejson` if you don't have it already.*

### Manual method

```
git clone git@github.com:faelix/sipcentric.git && cd sipcentric
sudo python setup.py install
```

## Getting started

### Examples

**Get account details**

```python
from sipcentric import Sipcentric

api = Sipcentric(username="myusername", password="mypassword")

print api.account.get()
```

**Connect to the streaming api**

```python
from sipcentric import Sipcentric

api = Sipcentric(username="myusername", password="mypassword")
stream = api.Stream

def callHandler(call):
  print 'Incoming call from ' + call['callerIdName'] + ' (' + call['callerIdNumber'] + ')'

def smsHandler(sms):
  print sms['excerpt'] + ' from: ' + sms['from']

stream.register(type='incomingcall', callback=callHandler)
stream.register(type='smsreceived', callback=smsHandler)

stream.connect()
```

## Reference

- sipcentric.Sipcentric(username, password, base='https://pbx.sipcentric.com/api/v1', customer='me')
  - account
    - get()
  - callBundles
    - get()
  - recordings
    - get()
  - phoneBook
    - get()
  - timeIntervals
    - get()
  - endpoints
    - get()
  - phoneNumbers
    - get()
  - sms
    - get()
    - post(to, _from, body)
  - creditStatus
    - get()
  - calls
    - get()
  - sounds
    - get()
  - outgoingCallerIds
    - get()
  - Stream
    - register(type, callback)
    - connect()
    - disconnect()

## History

This project was forked from Nimvelo's original project (for Python 2.7)
[python-client](https://github.com/Nimvelo/python-client).  The name was
changed to `sipcentric` after discussion with the development team at Simwood.
