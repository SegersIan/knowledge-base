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


| Mode | Desc | Pro | Con | conclusion |
| --- | --- | --- | --- | --- |
| RAID 0 - Striping | Data across all disks | Good I/O | No fault tolerance | More to just have IO |
| RAID 1 - Mirroring | Data duplicated to another drive(s) | Good I/O + availability | Needs double the storage |  |
| RAID 5 - Striping + parity | Data across all disks + 1 disk for parity/checksums | Fast reads, slow writes, can rebuild as long only one disk fails | Only handles one disk failure at a time. Rebuilding impacts performance | If you expect many reads, but not many writes |
| RAID 10 - Mirroring + parity | At least 4 drives, with adding in pairs. Data mirrored and then striped | PRO and CONs of Raid 0 and Raid 1 | PRO and CONs of Raid 0 and Raid 1 | |

## Response and Recovery Controls
### Capacity Planning for Resilience and Recovery
### Testing Resilience and Recovery Controls and Designs

## Physical Security Controls
### Site Security
### Detecting Physical Attacks
