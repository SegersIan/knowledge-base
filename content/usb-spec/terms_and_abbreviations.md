---
title: "Terms And Abbreviations"
---
# Terms and Abbreviations

I'm listing here terms and abbreviations that were relevant for my research. Skipping some more mainstream ones like "audio device"
and "Big Endian".

### ACK (packet)

A packet that signals a positive handshake acknowledgement.

### Active Device

Device that is **powered** and not in **suspend** state.

### Asynchronous Data

Data transferred at irregular intervals with relaxed latency requirements.

### Asynchronous RA

The incoming and outgoing **data rate** of the RA process. The rates are in this case independent (notice async), meaning
there is also no shared master clock.

### Asynchronous SRC

The incoming and outgoing **sample rate** of the SRC process.

### Babble

Unexpected bus activity that persists beyond a specified point in a (micro)frame.

### Bit Stuffing

Insertion of `0` bits into a data stream to cause electrical transition on the data wires.

### b/s

Bits/second

### B/s

Bytes/second

### Buffer

Storage used to compensate for a difference in data rates or time of occurrence of events, when transmitting data from
on device to another.

### Bulk Transfer

**One of the 4 USB transfer types**. Non-periodic, large busty communication typically used for a transfer that can use any
available bandwidth and can also be delayed until bandwith is available.

### Bus Enumeration

Detecting and identifying USB devices.

### Capabilities

Those attributes of a USB device that are administrated by the host.

### Characteristics

Those qualities of a USB device that are unchangeable; for example, the device class is a device characteristics.

### Client

Software resident on the host that interacts with the **USB System Software** to arrange data transfer between a function
and the host. The client is often the data provider and consumer for transferred data.

### Configuring Software

Software resident on the host software that is responsible for configuring a USB device. This may be a system configurator
or specific to the device.

### Control Endpoint

A pair of device endpoints with the same endpoint number that are used by a **control pipe**. Control endpoints transfer data
in both directions and, therefore, use both endpoint directions of a device and endpoint number combination.
Thus, each control endpoint consumes two endpoint addresses. See also [Device Endpoint](#device-endpoint)

### Control Pipe

Same as a message pipe.

### Control Transfer

**One of the 4 USB transfer types**. Control transfers support configuration/command/status type communications
between client and function.

### CRC (Cyclic Redundancy Check)

A check performed on data to see if an error has occured in transmitting, reading or writing the data. The CRC
is typically stored or transmitted with the checked data. This helps to determine if an error occured.

### CTI

Computer Telephony Integration

### Default Address

An address defined by the USB Spec and used by the USB device when it is first powered or reset. Default is `0x00`.

### Default pipe

Message pipe created by the USB System Software to pass control and status information between the host and a USB device's
*endpoint zero*.

### Device Address

Seven-bit value representing the address of a device on USB. Default is `0x00`. Addresses are uniquely assigned by
USB System Software.

### Device Endpoint

A uniquely addressable portion of a USB device that is the source or sink of information in a communication flow
between the host and device. See also [Control Endpoint](#control-endpoint)

### Device Resources

Resources provided by USB devices, such as buffer space and endpoints. See also Host Resources and Universal Serial Bus Resources.

### Device Software

Software responsible for using a USB device. May ir may bit also be responsible for configuring the device to use.

### Downstream

Direction of flow from the host or away from the host

### Driver

* When reffering hardware - An I/O pad that drives an external load.
* When referring software - A program responsible for interfacing to a hardware device (a device driver).

### DWORD (Double Word)

A data element that is two words. (e.g. four bytes or 32 bits when the word size is 2 bytes)

### Dynamic Insertion And Removal

The ability to attach and remove devices while the host is in operation.

### End User

The user of a host.

### Endpoint

[Same as Device endpoint](#device-endpoint)

### Endpoint Address

The combination of an endpoint number and an endpoint direction on a USB device. Each endpoint address supports data transfer
in one direction. Basically there will be two addresses at least for a USB device. Each one address has then a bit that
dictates the direction.

### Endpoint Direction

The direction of data transfer on the USB. This can be:

* **IN** - transfer to the host
* **OUT** - Transfers out from the host

### Endpoint Number

A four bit value between `0x0` and `0xF`, inclusive, associated with an endpoint on a USB device.

### EOF (End-of-(micro)Frame)

Self explaining

### EOP (End-of-Packet)

Self explaining

### Frame

a 1 ms time based established on full/low -speed buses.

### Frame Pattern

A sequence of frames that exhibit a repeating pattern in the number of samples transmitted per frame.

### Fs

Sample rate

### Full-duplex

Simultaneously data transmission in both directions.

### Function

A USB device that provides a capability to the host (like mic, speakers).

### Handshake Packet

A packet that acknowledges or rejects a specific condition.

### Host

Host computer systm where the USB Host controller is installed.

### Host Controller

Host's USB interface.

### Host Controller (HCD)

USB Software layer that abstracts the Host Controller Hardware.

### Interrupt Request (IRQ)

Signal to request attention from the host.

### Interrupt Transfer

**One of the 4 USB transfer types**. Small data, non-periodic, low-frequency and bounded-latency.

### I/O Request Packet (IRP)
 
An identifiable request by a software client to move data between itself and an endpoint of a device in appropriate direction.

### Isochronous Data

Stream of data whose timing is implied by its delivery rate.

### Isochronous Device

An entity with Isochronous endpoints.

### Jitter

Lack of synchronization.

### Message Pipe

Bi-directional pipe that transfers data using a request/data/status paradigm.

### Microframe

A 125 microseconds time base on high speed buses

### NAK

Rejecting handshake package

### Object

Host software or data structure representing a USB entity.

### Packet

A bundle of data organized in a group of transmission. Packets typically contain three elements:

* Control information (source, destination and length)
* Data to be transferred
* Error detection and correction bits

### Packet ID (PID)

A field in packet that indicates the type of packet. By inference it indicates the format of the packet and the 
type of error detection.

### Phase

A token, data or handshake packet. A transaction has 3 phases.

### Pipe

Abstraction of the association between an endpoint of the device and the software on the host. A pipe has several
attributes. So we have stream pipe's and message pipes.

### Polling

Asking (multiple) devices if they have any data to trasmit.

### Power on Reset (POR)

Restoring a storage device, register or memory to a predetemrined state when power is applied.

### Port

Point of access to or from a system or circuit.

### Rate Adaption (RA)

Adapting the rate of a data stream with certain loss of quality.

### Request

A request made to a USB device contained within the data portion of a SETUP packet.

### Service

A procedure provided by a System Programming Interface (ISP)

### SOF (Start Of Frame)

### SOP (Start of Packet)

### SRC (Sample Rate Conversion)

### TDM (Time Division Multiplexing)

### TDR (Time Domain Reflectometer)

### Token Packet

A type of paket that identifies what transaction is to be performed on the bus.

### Transfer

One ore more transactions to move information.

### Transfer Type

Determines the characteristics of the data flow. Types

* Control
* Inerrupt
* Bulk
* Ischronous

### USB-IF

USB Implementers Forum

### Virtual Device

A device that i represented by a software interface layer. 

### Word

2 bytes.