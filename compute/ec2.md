# EC2

Can only assign IAM roles when EC2 instance is created

#### Security Groups:
- All inbound traffic is blocked
- All outbound traffic is allowed
- Changes to security groups take effect immediately
- You can have any number of EC2 instances within a security group
- Security Groups are Stateful
    - If you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again

#### Security:
- Snapshots of encrypted volumes are encrypted automatically
- Volumes restored from encrypted snapshots are encrypted automatically
- You can share snapshots, but only if they are unencrypted
    - These snapshots can be shared with other AWS accounts or made public


#### Root Device Volumes:
- To create a snapshot from Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot


#### Raid Volumes and Snapshots:
- RAID -- redundant array of independent disks
    - RAID 0 - striped, no redundancy, good performance
    - RAID 1 - mirrored, redundancy
    - RAID 5 - Good for read, bad for writes, AWS does not recommend every putting RAID 5's on EBS
    - RAID 10 - Striped & Mirrored, Good Redundancy, Good Performance

#### AMI:
An Amazon Machine Image (AMI) provides the information required to launch a virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need.
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/CopyingAMIs.html
  - Template for root volume for the instance (for example, an operating system, an application server, and applications)
  - Launch permissions that control which AWS accounts can use the AMI to launch instances
  - A block device mapping that specifies the volumes to attach to the instance when it launched

#### Elastic Block Storage (EBS) and Instance Stores:
All AMIs are categorised as either backed by Amazon EBS or backed by instance store:
  - EBS volumes: the root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot
  - Instance Store Volumes: root device for an instance launched from the AMI is an instance store volume created from a template stored in S3
  - Types:
    - SSD, General Purpose (GP2) up to 10,000IOPS
    - SSD, Provisioned IOPS (IO1) more than 10,000IOPS
    - HDD, Throughput Optimised (ST1)
    - HDD, Cold (SC1) less frequently accessed data
    - HDD, Magnetic (Standard) cheap, infrequently access, can be bootable
  - Instance store volumes are sometimes called Ephemeral Storage
  - Instance store volumes cannot be stopped, if the underlying host fails, you will lose your data.
  - EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped
  - You can reboot both, you will not lose your data
  - By default, both root volumes will be deleted on termination, however with EBS volumes, you can tell AWS to keep the root device volume
  - Volumes restored from Snapshot need to be initialised to perform at the volumes specified I/O capacity.
  - Can change EBS volume type and size without detaching the volume, but requires running commands to let the operating system use the new volume size
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-initialize.html

### Elastic File System
File storage service for EC2 instances (block based storage). Storage capacity is elastic and allows decreasing or increasing capacity as files are removed or added. Can be mounted to more than 1 EC2 instance unlike EBS.
- Supports Network File System4 (NFSv4)
- Only pay for storage that is used - scales to petabytes
- can support thousands of concurrent NFS connections
- Data stored across multiple AZ's within a region
- Read after write consistency

### Elastic Load Balancers:
- Act as a high availability proxy for EC2 instances. Route traffic to and from EC2 instances and a DNS endpoint
- Health checks - time intervals checking whether an EC2 instance is working
- Have their own DNS name, not given an IP address

### Volumes and Snapshots:
 - snapshots of encrypted volumes are encrypted automatically and volumes restored from encrypted snapshots are encrypted automatically
    - Snapshots can be shared but only when unencrypted
        + Can be made public or shared with other AWS accounts
Volumes exist on EBS
  - Volumes are virtual hard disks
Snapshots exist on S3
  - Snapshots are point in time copies of Volumes
  - Snapshots are incremental, only blocks that have changed will be moved to S3
  - Initial snapshots take time to create
Taking a Snapshot of a RAID Array:
  - stop the application or instance from writing to disk
    + performed by either: 1. freeze the file system; 2. unmount the RAID array; 3.
  - flush all caches to disk
  - then take the snapshot of the RAID EBS volumes



### Useful Commands:
https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Administration/s1-LVMsetupnfs-HAAA.html
- Attaching/Formatting/Mounting Block:
```bash
$ lsblk # lists storage devices on a linux instance
$ file -s /dev/<volume> # lists the file system on a volume, returns 'data' if no filesystem is present
$ file -s /dev/<volume> ext4 # formats the file system using the ext4 filesystem - look at mkfs
$ mkdir - p /path/todir && mount -o /dev/<volume> <target_directory> # mounts target directory
$ unmount <target_directory> # unmounts the mounted volume at the target directory
$ df -h # lists disks available to the OS
```


#### EC2 Metadata:

- Get public IP address or other meta-data about the instance (not user):
- ```curl http://169.254.169.254/latest/meta-data/ ```


Launch Configurations and Auto-scaling:
