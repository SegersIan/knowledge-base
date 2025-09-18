# Resilience and Physical Security
* **Resilience** is key to tackle the **availability** goal of the CIA Triad.

## Resilience and Recovery in Security Architectures
* **Resilience and ability to recover** is key.

### Key Concepts & Practices
* **Continuity of operations** - ensure operations will continue even if issues from single system failure to wide-scale natural disaster occurs.
* **Redundancy**
  * Geographic dispersion of systems to protect against single dissaster/failure/attack.
  * Seperatio of servers and other devices in datacenters
  * Power Distribution Unit (PDU)
  * Multipath - multiple network paths to deal with loss of connectiity
  * Redundant network devices
* **High availability designs**
  * Load balancing
  * Clustering (e.g. kubernetes)
* Uninterruptible power supply (UPS)
* Systems and storage redundancy
* Platform diversity - diversy across technologies and vendors

### Architectural Considerations and Security
* **Availabiliy targets** to meet organizational requirements, balanced against other considerations.
* **Resilience** what type and level of potential disruptions can handle without availability issues
* **Cost**
* **Responsiveness**
* **Scalability**
* **Ease of deployment**
* **Risk transferance**
* **Ease of recovery**
* **Patch availability** and **vendor support** how often an how, well supported
* **Inability to pach** consideer when high availability is required
* **Power consumption**
* **Compute requirements**
### Storage Resiliency
* **Redundent Arrays of Inexpensive Disks (RAID)**
  * Methods
    * Data striped (spread across disks)
    * Data mirrored (complete duplicated)
    * And technology to make sure data is not corrupted or lost (parity)
* **Backups**
  * Full - entire full snapshopt everytime - lots of disk, but fast recovery
  * Incremental
    * Backs up changes since the last backup (regardless of type)
    * less space and faster, but slow recovery
  * Differential - deltas between backups
    * Backs up changes since the last full backup
    * faster recovery, but slower backup
  * Most efficient, differential backups, with a periodic new full backup
* **Replication**
  * Constant streaming changes
* **Journaling**
  * Create a log of changes that can be replayed, allows to restore to point in time
  * Not perfect, as this would also need a backup if you would use this
* **Recovery Point Objective (PRO)** how much loss is acceptable
* **Recovery Time Objective (RTO)** how long a recovery can take before causing issues
* **Full Backup:** = Data-focused
  - **What**: Complete copy of all data, you bakcup files and folders (no OS, Apps, settings)
  - **When**: Scheduled intervals (weekly/monthly)
  - **Restore**: Single restore operation
  - **Use case**: Disaster recovery, compliance, archival
* **Snapshot:** = State-focused
  - **What**: Point-in-time view of data state
  - **How**: Usually copy-on-write (shares unchanged blocks) - IT TRACKS Changes
  - **Speed**: Near-instantaneous
  - **Use case**: Quick rollbacks, testing, before major changes
* **Image:** = System-focused
  - **What**: Exact bit-for-bit copy of entire system/disk (including OS, Apps, settings, AND Data)
  - **Includes**: OS, applications, data, boot sectors - everything
  - **Use case**: System cloning, bare-metal recovery, VM deployment
* When to use:
  * Snapshot: Before deployments, quick dev/test environments
  * Image: Server provisioning, disaster recovery baseline
  * Full backup: Regulatory compliance, long-term data protection

| Mode | Desc | Pro | Con | conclusion |
| --- | --- | --- | --- | --- |
| RAID 0 - Striping | Data across all disks | Good I/O | No fault tolerance | More to just have IO |
| RAID 1 - Mirroring | Data duplicated to another drive(s) | Good I/O + availability | Needs double the storage |  |
| RAID 5 - Striping + parity | Data across all disks + 1 disk for parity/checksums | Fast reads, slow writes, can rebuild as long only one disk fails | Only handles one disk failure at a time. Rebuilding impacts performance | If you expect many reads, but not many writes |
| RAID 10 - Mirroring + parity | At least 4 drives, with adding in pairs. Data mirrored and then striped | PRO and CONs of Raid 0 and Raid 1 | PRO and CONs of Raid 0 and Raid 1 | |

| Type | Speed | Storage | Granularity | Primary Use |
|------|-------|---------|-------------|-------------|
| **Full Backup** | Slow | High | File-level | Long-term protection |
| **Snapshot** | Fast | Efficient | Block-level | Quick recovery/testing |
| **Image** | Medium | High | System-level | Complete system restore |

## Response and Recovery Controls
* **Nonpersistence** - Controls to make a system go to it's original state
  * Snapshot
  * Go back to last known configuration
  * Systems reset after reboot
* **Live boot media** - Boot from USB stick a portable OS to go in and fix stuff (or forensics too)
* **Site resilience** (part of Site COnsiderations)
  * **Hot Sites** Have everything to run, and often run fulltime (taking a portion of the traffic)
    * Most expensive
    * Quickest Recovery
  * **Warm Sites** Live data not in place, but all infrastructure to jump in quickly
    * Medium expensive
    * Medium recovery speed
  * **Cold Sites** All infra and newtwork is there, but not systems/data
    * Cheapest
    * Longest recovery

### Capacity Planning for Resilience and Recovery

* **People** - have enough staff, can't upscale quickly, 3th parties can fill in that void when necessary
* **Technology** - that are present and how they can scale
* **Infrastructure** - that can handle all these different loads

### Testing Resilience and Recovery Controls and Designs

* **Tabletop excercises** - use discussion between relevant personel beeded for the plan to be validated
  * Least disruptive
  * Low quality feedback
* **Simulation excercises** - Drills & practice that personel simmulate in case of an actual event
* **Parallel processing excercises** - Move processing/traffic partially to hot or alternate site to validate if everything works
* **Failover excercises** - Do full switch to another side/faillover
  * Potentialy most disruptive
  * Highest quality feedback

## Physical Security Controls
### Site Security
* **Site security Plan** - Risk assesment of a site and them decide what to implemment, mitigate, transfer...  resulting in an action plan for the site. A site security plan.
* **Industrial Camouflage** - nondescript location, without a name on it, so it doesn't have Amazon call center in big on it.
  * It's security through obscurity, but its a little help, security in layers right?
* **Fences** - Often first line defence
  * Works as detterent, to scare off but to also actually fence off.
* **Bollards** - posts/obstacles that prevent vechicle access
* **Lighting** - Discourage intruders and make staff veel safe by not having dark/shadow pplaces
* **ANTI - Drones or Unmanned Areal Vechicles (UAV) systems**
  * Attacks by drones: Capture image/video, cut wire, block video
  * Anti-drone detections: wireless signals, EM emission, heat production (infrared), accoustic (listen for drone sounds), optical (just see a drone), ...
  * Defense against drones: Kinetic systems to shoot drones down, jamming signals, ...
  * Be careful to take drones down, cause it might cause in expensive fines (e.g. it was just a casual neighbour)
* **Access Badges** - Can be for authN, authZ, etc, often
  * Social Engineering often used for trying to copy a badge
* **Vestibule** - is like a buffer zone between lower and higher security zones
  * Let someone first enter this vestibule zone after verification
  * Once we know the person is alone in the vestibule, close the door
  * Now open the door to the higher secure facility
  * Against anyone piggybagging entrance (like keeping the door open)
* **Others**
  * Alarms - Some pentesters make alarms go off often, so when the actual intrusion happens, no one is looking up.
  * Locks - locks keep honest people honest, but can always be bypassed
#### Guards'
* Where human interaction is neccesary or helpful
* Offer detective and responsive capabilities
* An alert guard can significantly make it more difficult to get in with fake signatures, ids, ...
* But also prone to
  * Social ENgineering
  * Human mistakes
  * Expensive

#### Video Surveilance, Cameras and sensors
* **Motion Recognition Cameras** - activate when motion occurs.
  * Good for when motion is infrequent
  * Comes with a buffer of a few seconds before motion was picked up
  * Might lack the video when no motion was "Sensed" but maybe there was, depending on the sensor.
* **Object Recognition Cameras** - Can detect cetain objects and if there are moving
* **Dazzle paint** - used to confuse cameras
* **Closed-Circuit TV (CCTV)** - shows live on screens what they see, and *can* additionly record, but not necessarily.
* **Sensors** another way to provide security
  * Infrared - trigger when changes happen in infrared space, very inexpensive.
  * Pressure - Good to trigger if an object is moved.
  * Microwave - More expensive, more reach, but more error prone. They take a baseline of the room and can then detect if changes happened from the baseline.
  * Ultrasonic - uncommon, but trigger on certain vibrations, good for proximity detection.


### Detecting Physical Attacks
