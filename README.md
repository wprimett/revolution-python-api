# BITalino (r)evolution Python API
The BITalino (r)evolution Python API provides the needed tools to interact with BITalino (r)evolution using Python.

This fork is adjusted to work with python3/[ServerBIT (r)evolution](https://github.com/BITalinoWorld/revolution-python-serverbit)

## Dependencies
* [Python >2.7](https://www.python.org/downloads/) or [Anaconda](https://www.continuum.io/downloads) or [Python 3.4](https://www.python.org/downloads/)
* [NumPy](https://pypi.python.org/pypi/numpy)
* [pySerial](https://pypi.python.org/pypi/pyserial)
* [pyBluez](https://pypi.python.org/pypi/PyBluez/) (Not needed for Mac OS)

## Installation
To use specific version, clone or download the repo and copy `bitalino.py` to your working directory. From you main script, call:

```
from bitalino import *
```

## Documentation
http://bitalino.com/pyAPI/

## Example
~~~python
import time
from bitalino import BITalino

# The macAddress variable on Windows can be "XX:XX:XX:XX:XX:XX" or "COMX"
# while on Mac OS can be "/dev/tty.BITalino-XX-XX-DevB" for devices ending with the last 4 digits of the MAC address or "/dev/tty.BITalino-DevB" for the remaining
macAddress = "00:00:00:00:00:00"

# This example will collect data for 5 sec.
running_time = 5
    
batteryThreshold = 30
acqChannels = [0, 1, 2, 3, 4, 5]
samplingRate = 1000
nSamples = 10
digitalOutput = [1,1]

# Connect to BITalino
device = BITalino(macAddress)

# Set battery threshold
device.battery(batteryThreshold)

# Read BITalino version
print(device.version())
    
# Start Acquisition
device.start(samplingRate, acqChannels)

start = time.time()
end = time.time()
while (end - start) < running_time:
    # Read samples
    print(device.read(nSamples))
    end = time.time()

# Turn BITalino led on
device.trigger(digitalOutput)
    
# Stop acquisition
device.stop()
    
# Close connection
device.close()
~~~
## License
This project is licensed under the [GNU GPL v3](LICENSE.md)
