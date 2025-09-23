# Wireless and Mobile Security
> Have distinct challenges compared to wired networks.
> They broadcast their signals and are often available from outside the area that an organization contols.

## Building Secure Wireless Networks

### Connection Methods

#### Cellular
* networks provide connectivity by dividing geographic areas into "cells".
* Each cell might have more than one tower.
* 5G needs more attena density, but has more throughput, so requires more antenna planning than 4G.
* Provided by cellular carriers. - So it's a external network from your organization.
* *Operating Scope* : Long range

#### WIFI
* is a set of protocols for wireless LAN.
* Most popular *radio bands*: `2.4 GHz` and `5.0 GHz`
* Uses *multiple channels* for different WIFI networks to coexist in each others vicinity.
* *Key security concern* is that the signals travel outside the organization's walls.
* *Different standards* `802.11b`, `802.11ac`, `802.11x`, `802.11n`, `802.11g`...
  * Some are "aliased" like WIFI 6 is the alias for `802.11ax`
* *Protocols* like `WPA2` and `WPA3` provide security like encryption, authentication and network frames protection.
* *Wifi Devices Modes*
  * `ad hoc` - device-2-device communication, like p2p. No intermediaries. But both devices must be able to reach each other. Sometimes called mesh.
  * `infrastructure` - direct all traffic through base station/access point. Typical for your home router or access point. They follow a star/hub-and-spoke network design.
* `Service Set Identifiers (SSID)` are used to identify networks, these can be broadcasted or kept private.
* *Operating Scope* : Mid range

| Wi-Fi standard | Generation name | Maximum speed | Frequencies |
|----------------|-----------------|---------------|-------------|
| 802.11b | | 11 Mbit/s | 2.4 GHz |
| 802.11a | | 54 Mbit/s | 5 GHz |
| 802.11g | | 54 Mbit/s | 2.4 GHz |
| 802.11n | Wi-Fi 4 | 600 Mbit/s | 2.4 GHz and 5 GHz |
| 802.11ac | Wi-Fi 5 | 6.9 Gbit/s | 5 GHz |
| 802.11ax | Wi-Fi 6 and Wi-Fi 6E | 9.6 Gbit/s | 2.4 GHz, 5 GHz, 6 GHz |
| 802.11be | Wi-Fi 7 | 40+ Gbit/s | 2.4 GHz, 5 GHz, 6 GHz |

#### Bluetooth
* *radio band*: `2.4 GHz`
* *purpose* : Low power, short range and low bandwith.
* *Operationg mode* : Point-2-Point
* *Operating Scope* : close range
* *Pairing* : Process for establishing a connection, requires sometimes a `pin` to complete.
* *Security Modes*
  * 1 - No Security (non-secure)
  * 2 - Service-level enforced security
  * 3 - Link-level enforced securty
  * 4 - Standard pairing with Security Simple Pairing (SSP)
* *encryption* is supported, relies on `PIN` used by both devices, like a shared key.
  * Devices like headsets use `FIXED PINS` decreasing its security.
* *Attacks* against authN and negotiating encryption keys allows for eavesdropping.

### Radio Frequency Identification (RFID)
* Tags are either
  * `active`: Powered themselves and always emits signals to be read by a reader
  * `semie-active`: Powered themselves, but emit signals when the reader asks for it
  * `passive`: entirely powered by the reader.
* *Frequencey Ranges*
  * `low` - short-range, low-power (touch field)
    * Use case : Entry Access & Identification
    * power and frequency can be different around the world, so might not work everywhere the same.
  * `high` - Up to a meter (near field)
    * Communicates faster than `low`
    * Support `read-only`, `write-only` and `rewritable` tags
  * `ultra-high` - highest range and speed to read.
    * Use Cases: inventory, antitheft (shops)
* *Operating Scope* : near to close range (up yo 100m for active tags)
* *Tags are small and inexpensive*
* *Attack Vectors*
  * Destruct/damage tag so they can't be read
  * Reprograming of tags
  * Tags can be cloned, modified or spoofed, or readers can be impersonated.
#### Global Position System (GPS)
* *Operating Scope* : very wide range
* *Only sends signals* - you receive `location` and `time` signals, but you don't connect to have a casual dialog.
* *Attack Vectors*
  * Signal can be jammed
  * Signal can be spoofed
* *Goal* : Geolocation
* GPS often combined with other location centric data (wifi names, bluetooth, ...) to have an accurate location of a device.
#### Near Field Communication (NFC)
* *Operating Scope* : near/touch range (~10 cm)
* *Device-2-device* communication
* *Low bandiwth*
* *Attack Vectors*
  * When in close proximity: Intercept NFC traffic, replay attacks and spoof attacks.
  * NFC decices must not respond to queries unless desired. That's why paying with APple Pay, you need to "trigger your card" first before you can pay.

#### Infrared
* *Device-2-device* communication, but networks are technically possible
* *Attack Vectors*
  * Can be caputed by anything in line of sight.

### Wireless Network Models
* **point-top-point** (decentralized) like device to device, direct connection.
* **point-top-multipoint** (centralized) like an accesspoint/router using the `infrastructure` mode, central hub
* **mesh** - Multiple interconnected paths between many devices
* **broadcast** - sends out on many nodes (like GPS), no return path

### Attacks Against Wireless Networks and Devices
* **EvilTwins and Rogue Access Points**
* **Bluetooth Attacks**
* **RF and Protocol Attacks**
* **Sideload and Jailbreaks**

### Designing a Network
* **TODO**

### Controller and Access Point Security
* **TODO**

### Wi-Fi Security Standards
* **TODO**

### Wireless Authentication
* **Wireless Authentication Protocokls**

## Managing Secure Mobile Devices
* **TODO**

### Mobile Device Deployment Methods
* **TODO**

### Hardening Mobile Devices
* **TODO**
