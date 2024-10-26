### Step 1: Format Your External SSD, Add A BTRFS Filesystem

The first step in this backup workflow is formatting the external backup device with a BTRFS filesystem (it's assumed that the external device you are using is formatted with something like a `FAT32` filesystem).

1. **Connect the SSD**: Plug the SSD into your Fedora computer via USB or SATA.

2. **Identify the Device**: Open a terminal and run:
   ```
   lsblk
   ```
   Locate your SSD (e.g., `/dev/sdc`).

3. **Create a Partition**:
   
   ```
   sudo parted /dev/sdc
   ```

   Then enter:

   ```
   mklabel gpt
   mkpart primary btrfs 1MiB 100%
   quit
   ```

4. **Format as BTRFS**:
   
   ```
   sudo mkfs.btrfs /dev/sdc1
   ```

This will format your SSD as a BTRFS filesystem with a single partition named "Backups."