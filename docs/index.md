#  BTRFS Backups Fedora Linux

This documentation was generated using ChatGPT with editing by Daniel Rosehill (danielrosehill.com).

This repository is intended as an experiment to try out this publishing workflow. 

But it also contains information about a backup approach intended to provide incremental backups of a Fedora Linux desktop/workstation onto an external SSD.

While Fedora is the assumed OS, this documentation might also be helpful for users on other distros that are working with a BTRFS filesystem.

V1: 26-10 (Oct) - 2024.

---

## BTRFS To BTRFS Backup

This documentation demonstrates how to run BTRFS snapshots onto an external device. 

My setup involves backing up a Fedora Workstation, configured with BTRFS + RAID1, to an external SSD. 

This gives me a backup approach that's replicable and reliable and which provides me with a reasonable degree of confidence that some of my desktop system configuration could be recovered in the event of hardware failure (etc).

While I picked up an external SSD because I wanted the snapshots to write quickly onto the target, this method is adaptable to various storage devices, leveraging the powerful and space-efficient snapshot capabilities of BTRFS while utilizing an external device for risk mitigation.  

Note: as a general rule, preserving data in cold storage is not recommended and neither SSD nor HDD provides obvious benefits. 

To mitigate risk, you could run the snapshots onto an SSD or HDD which was provisioned within a live (running) filesystem, ideally with fault-tolerant storage hardware (e.g. running RAID). This could be done by adapting this approach to backup onto (say) a volume within a Synology NAS or your own NAS.

---

## BTRFS Versus Bare Metal For Full System Backups

BTRFS snapshotting has advantages and deficiencies when compared with full disc imaging backup-methodologies (ie, bare metal backup). 

Clonezilla is used as an example of a disk imaging / block-level backup approach.

| Feature                | BTRFS                      | Clonezilla               |
|------------------------|---------------------------|--------------------------|
| **Bare Metal?**        | No                        | Yes                      |
| **Incremental?**       | Yes                       | No                       |
| **Recovery**           | Provision new OS, then recover from snapshot | Direct recovery from image |
| **Storage Efficiency**  | High (deduplication)      | Moderate (full image)    |
| **Flexibility**        | High (individual file recovery) | Low (whole system only)  |
| **Speed**              | Fast (snapshotting)       | Slower (image creation)   |

The tradeoff creates some differences in terms of recovery:

Recovery from tools like Clonezilla or REAR might be thought of as the "gold standards" in disaster recovery. Both are recovery methods which enable comprehensive restores onto new hardware.

BTRFS restores using this method would require some more "groundwork" in the form of provisioning a new OS and bootloader. 


## Attribution

This documentation was created by [Daniel Rosehill](https://danielrosehill.com) in conjunction with GPT-4. It is licensed for anyone's use with proper attribution.
