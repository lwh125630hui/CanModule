=======
Running
=======

The proper kernel modules, drivers and libraries for the vendors used through CanModule 
have to be present during runtime. Please also refer to `Status`_ for an overview over 
runtime conditions (april 2019).


general dependencies
--------------------
* CanModule.dll/.so
* LogIt (cloned from github during cmake)
* boost 1.64.0
* xerces 3.2 (xerces-c_3_2D.dll)

Anagate
-------
* libancan.dll/.so  (standard API)
* linux: libAPIRelease64.so, libCANDLLRelease64.so, libAnaGateExtRelease.so, libAnaGateRelease.so
* windows: ANAGATECAN64.dll

Systec
------
* linux: libsockcan.so (standard API), driver kernel module systec_can.ko and dependent modules
* windows: libstcan.dll (standard API), USBCAN64.dll

Peak
----
* linux: libsockcan.so (standard API), driver kernel module pcan.ko and dependent modules
* windows: libpkcan.dll (standard API), PKCANBASIC.dll

message speed
-------------
the bitrate bits/s of the CAN bus has to be adjusted to make both the master and all slaves 
happy. Many older modules use 125000bit/s, and some newer are at 250000bit/s. Nevertheless it 
turns out that sometimes a high rate of messages can not be processed properly by a slave. A "throttled"
version of sendMessage(...) can be used to slow down the message frequency to (below) 100Hz:
sendmessage( &cm, true ) ; as descripbed in the standardAPI. Some rare collisions can occur on the
CAN bus which are only reported as ACK fails directly on the bus but are not seen by the software. 

Message throttling seems to be needed for certain ISEG controllers. 

.. _Status: https://edms.cern.ch/file/2089743/1/CanModuleStatus2019_v4.pptx
  
  