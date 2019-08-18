# Networking 101

Summary of network relevant topics regarding computers.

## Introduction OSI model

* **OSI:** Open Systems Interconnection Model
  * Standardizes communication functions of telecommunication/computer systems with standard communication protocols.
  * Original model defines 7 abstraction layers.
  * A layer servers the layer above and served by the layer below.
  * ISO standard
  * Each level has a **PDU**, Protocol Data Unit (e.g. Data, Package, Segment, Frame, ...)
  * A PDU has a **payload** (Service Data Unit, SDU) + protocol related header and footer.
  * Some protocols might define "sublayers" for the benefit of the protocol design.
  
* Communication protocols enable an entity in one host to interact with corresponding entity at the same layer in another host.

* The 7 Layers
  * Layer 1: **Physical** - Transmission of raw data between devices over a medium. Converts bits to electric/radio or optical signals.
  * Layer 2: **Data Link** - Node to node transfer. Detects/corrects errors in physical layer. Defines protocol to establish and terminate connections between physical devices + flow control. (e.g. 802.11 Wi-Fi)
  * Layer 3: **Network** - Functional and procedural means of transferring variable length packets from one node to another in different networks. At this point there is a concept of "address" for each node and a packet can be "routed". At this point the packet does not travel perse between 2 devices that are physically directly connected. More details later.
  * Layer 4: **Transport** - Functional and procedural means of transferring variable length packets from source to destination while maintaining QoS functions.
  * Layer 5: **Session** - Controls (establish, manage and terminate) connections between computers. Provides full-duplex, half-duplex and simplex operation. RPCs usually live on this layer.
  * Layer 6: **Presentation** - Establish context between application-layer entities. Translates between network and application formats. So translates data into the format that he application layer accepts. Layer can also include compression functions.
  * Layer 7: **Application** - Layer closest to end user, communicating with the software application.
  
* Cross-layer functions: Services not tied to a given layer, may affect multiple layers (e.g. security).

* Comparison with TCP/IP model:
  * Internet Application Layer: Maps to OSI's Application (#7), Presentation (#6) and Session Layer (#5).
  * TCP/IP Transport Layer: Graceful close functions of OSI Session (#5) and Transport layer (#4).
  * Internet Layer: OSI Network Layer (#3)
  * Link Layer: OSI Data Link Layer (#2) and Phsyical Layer (#1)
  * Notice how OSI Session layer relates to Internet Application and Transport layer of TCP/IP.
  
## Layer 1: Physical


