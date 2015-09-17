mightex_device_python
=====================

This Python package (mightex\_device) creates a class named MightexDevice,
which contains an instance of serial\_device2.SerialDevice and adds
methods to it to interface to Mightex LED controllers.

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

##Example Usage

```python
dev = MightexDevice() # Automatically finds device if one available
dev = MightexDevice('/dev/ttyUSB0') # Linux
dev = MightexDevice('/dev/tty.usbmodem262471') # Mac OS X
dev = MightexDevice('COM3') # Windows
dev.get_serial_number()
'04-150824-007'
dev.get_channel_count()
4
channel = 1 # channel numbering starts at 1, not 0!
dev.get_mode(channel)
'disable'
dev.set_normal_parameters(channel,1000,30)
dev.get_normal_parameters(channel)
{'current': 30, 'current_max': 1000}
dev.set_mode_normal(channel)
dev.get_load_voltage(channel)
2622
dev.set_normal_current(channel,200)
dev.get_load_voltage(channel)
3054
dev.set_mode_disable(channel)
dev.set_strobe_parameters(channel,100,1)
dev.get_strobe_parameters(channel)
{'current_max': 100, 'repeat': 1}
dev.set_strobe_profile_set_point(channel,0,100,1000000)
dev.set_strobe_profile_set_point(channel,1,10,500000)
dev.set_strobe_profile_set_point(channel,2,0,0)
profile = dev.get_strobe_profile(channel)
profile
[{'current': 100, 'duration': 1000000},
 {'current': 10, 'duration': 500000},
 {'current': 0, 'duration': 0}]
dev.set_mode_strobe(channel)
dev.get_strobe_profile(channel+1)
[{'current': 20, 'duration': 1000},
 {'current': 10, 'duration': 1000},
 {'current': 0, 'duration': 0}]
dev.set_strobe_profile(channel+1,profile)
dev.get_strobe_profile(channel+1)
dev.set_mode_strobe(channel+1)
dev.set_trigger_parameters(channel,100,True)
dev.get_trigger_parameters(channel)
{'current_max': 100, 'falling_edge': True}
dev.set_trigger_profile_set_point(channel,0,100,1000000)
dev.set_trigger_profile_set_point(channel,1,10,500000)
dev.set_trigger_profile_set_point(channel,2,0,0)
dev.get_trigger_profile(channel)
[{'current': 100, 'duration': 1000000},
 {'current': 10, 'duration': 500000},
 {'current': 0, 'duration': 0}]
dev.set_mode_trigger(channel)
dev.reset()
dev.get_trigger_profile(channel)
[{'current': 20, 'duration': 1000},
 {'current': 10, 'duration': 1000},
 {'current': 0, 'duration': 0}]
dev.set_trigger_profile_set_point(channel,0,100,1000000)
dev.set_trigger_profile_set_point(channel,1,10,500000)
dev.set_trigger_profile_set_point(channel,2,0,0)
dev.store_parameters()
dev.reset()
dev.get_trigger_profile(channel)
[{'current': 100, 'duration': 1000000},
 {'current': 10, 'duration': 500000},
 {'current': 0, 'duration': 0}]
dev.restore_factory_defaults()
dev.store_parameters()
dev.reset()
dev.get_trigger_profile(channel)
[{'current': 10, 'duration': 20},
 {'current': 0, 'duration': 0}]
```

```python
devs = MightexDevices()  # Automatically finds all available devices
devs.keys()
dev = devs[serial_number]
```

##Installation

[Setup Python](https://github.com/janelia-pypi/python_setup)

###Linux and Mac OS X

```shell
mkdir -p ~/virtualenvs/mightex_device
virtualenv ~/virtualenvs/mightex_device
source ~/virtualenvs/mightex_device/bin/activate
pip install mightex_device
```

###Windows

```shell
virtualenv C:\virtualenvs\mightex_device
C:\virtualenvs\mightex_device\Scripts\activate
pip install mightex_device
```
