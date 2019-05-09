# USB Spec and how it works

Here I summerize useful information on how USB works,
this is a part of my research project to use a PS4 controller in the browser.

## Terms And Abbreviations

The extensive list can be [found here](terms_and_abbreviations.md).

## Architectural Overview

Host-scheduled, token-based protocol.

### USB System

3 areas

* USB interconnect (Manner which USB devices are connected and communicate with the host)
  * Bus Topology
  * Inter-layer relationships: In terms a capability stack, the USB tasks performed at each layer in the system.
  * Data Flow Models: Manner in which data moves
  * USB Schedule
* USB Devices
* USB host

A USB device usually provides one or more "functions".

#### USB Protocol

All communication happens through a POLLING mechanism. So the USB Bus Protocol is Poll oriented.

Most bus transactions involve transmissions of up to 3 packets. Each transaction begins when the Host Controller,
on a scheduled basis, sends a **USB Token packet** describing the: 
* Type of transaction
* Direction of transaction (IN or OUT)
* the USB device address
* Endpoint number
 
The addressed USB device selects itself by decoding the appropriate address fields. (AH! That's me!).
The targeted device will then send a data packet or indicate if it has no data to transfer. The host will then
reply witha handshake packet indicating if the transfer was successful.

The data transfer model between source and destination on the host and an endpoint is reffered to as a **pipe**.

A pipe can be

* Stream pipe (has no USB defined structure)
* Message pipe (has USB defined structure)

One message pipe, the **Default Control Pipe** always exists once a device is powered. (used for device's configuration,
status and control information)

The Host assigns a unique USB address to a newly attached device and then determines if it's a Device or Hub or a Function.
Then the hosts establishes  its end of the **control pipe** for the newly attached USB device using the assigned
USB address and endpoint `0x0`.

If the newly attached device is a hub with attached devices, the above procedure is followed for each of the attached USB devices.

#### USB Enumeration

Activity that identifies and assigns unique address to devices attached to a bus. This happens periodically and
does the detection of removing and adding of devices.

#### Data Flow Types

Data and control change happens through a set of either uni-directional or bi-directional pipes. 
**Transfer take place between host software and a particular endpoint on a USB device**.
The association between the Host Software and a USB device endpoint **is a pipe**.
In general, data movement through one pipe is independent from the data flow of any other pipe.

* **Control Transfer** : USed to configure a device at attach time and can be used for other device-specific purposes,
including control of other pipes on the device.
* **Bulk Data Traansfers** Generated or consumed in relatively large and bursty quantities and have wide dynamic latitude in transmission constraints.
* **Interupt Data Transfer** Used for timely but reliable delivery of data,.
* **Isochronous Data** Occupy a prenegotiated amount of USB Bandwidth with a prenegotiated delivery latency. Typically for real time consumption.
  As this is for real time, errors are often not corrected.

A single pipe only supports one data flow type for any given device configuration.

#### USB Devices

Devices are divided into classes such as hub, human interface, printer, imaging or mass storage device.

Each device is assigned an address when attached and enumerated. USB devices will have a designated pipe at endpoint `0x0`
where to the *Default Control Transfer` pipe will be established. From the default control pipe we get the characteristics 
of a device:

* Class
* USB Vendor
* Standard

Two major classes exist, hubs and functions. Functions provide capabilities to the host, hubs just more connections.

A device can have multiple functions (like sound and video, like a webcam).
Each function will have a configuration. **Before function can be used, it MUST be configured by the host.**


## USB Data Flow Model

## Protocol Layer

... maybe others