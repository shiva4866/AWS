
Elastic Block storage :
-------------------------------------------------------------------------
1)storage volume to ec2 instance 
2)ability to install any thing on it.
3)Virtual hard disk in the cloud.(production workload)
4)exists across multiple disk inside same availability zone.(backup/hardware failures)
5)scalable

types: 
---------------------------------------------------------------------
solid state drive:gp2(general purpose): 
gp3 : (boot device volumes for installing OS).(both gp2 and gp3)
High performance ,low cost .(gp3 = gp2 * 4 speed)

io1 / io2 : expensive , high performance , for io intensive


Hard disk drive:(HDD)

st1 : Magnetic storage for hard disk / low cost HDD Volume.
it can't be boot volume.
(big-data /warehousing)

cold HDD : (cost reduction) can't be boot volume

IOPS :1) number of read/write operations
      2)important metric for quick transaction operation,low latency,transactional workloads.

Throughput:==>number of bits read.written per second .important metric ==>for large datasets, largeI/O sizes , complex queries.

==>the ability to deal with large datasets.
==>choose throughput optimized HDD(st1).


==>lsblk list all block devices.


Volumes and snapshots:
----------------------------------------------------------------
Volumes => virtual hard disk 
==>ec2 instance need atleast one EBS Volume.(root device volume where OS is installed).


Snapshot :1) it exists on S3 .
          2)Snapshots are photograph of VHDD.
          3)Snapshots are point in time.(When you take a snapshot , it is a point in time copy of volume).
          4)Incremental ( this means that data that has been changed is moved to s3 . this saves dramatically on space and time it takes to take a snapshot).
          5)first snapshot takes more time than second.
          6)EBS and EC2 should be same in Availability Zone.
          7)Resize/change on the fly need not to restart.

Snapshots are used to copy EC2 instances from one region to another.


Protecting our EBS Volume with encryption.
------------------------------------------------------------------------
==>use AES-256.
==>Data at rest , Data at flight , All Snapshots ,All volumes are encrypted.
==>Minimal effect fon latency.
==>Copying an unencrypted snapshot allows encryption.
==>Snapshots of encrypted volumes are encrypted by themselves.
==>root volumes can be encrypted on creation.


4 steps to Encrypt an Unencrypted Volume.
-------------------------------------------------------------------------
1)Create a snapshot of the unencrypted root device volumes.
2)Create a copy of snapshot and select the encrypt option.
3)Create AMI from encrypted snapshot.
4)Use the AMI to launch new Encrypted instances.


EC2 Hibernation
-------------------------------------------------------------------------
==>on termination the root device voulme is terminated .
==>On hibernation EC2 instance , OS suspends the disk after saving the ==>contents from instance memory(RAM) to your amazon root volume.AWS persisits any EBS root and attached volume. 
==>on start EBS Voulme is restored and RAM is reloaded.
==>it preserves the in-memory RAM on persistent storage(EBS) for RAM < 150 GB.
==>much faster to boot up not need to reload the OS.
==>instance can't be hibernated for more than 60 days.
==>On demand insances and reserved instances.



EFS (Elastic File System)
-------------------------------------------------------------------------
==>Managed NFS(Network file system) that can be mounted on many EC2 instances.
==>EFS works with EC2 instances in multiple AVailability Zones.
==>Highly scalable and available , and expensive.

Usecases :1) Content Management , Web servers .
Use NFSv4 protocol
2)Compatible with Linux-based AMI(Windows not supported at this time).
3)Encryption at rest using KMS.
4)File System scales automatically no capacity planning required.



Storage Tiers :
-------------------------------------------------------------------------
Standard : for frequently used files.
Infrequently accessed : for files not frequently accessed.


FSx Overview :
-------------------------------------------------------------------------
FSx for Windows :
 ------------------------------------------------------------------------
 Amazon FSx for Windows File Server Provides a fully managed native Microsoft Windows File System so you can easily move your Windows based applications that require file storage to AWS.

FSx vs EFS
------------------------------------------------------------------------
FSx :
   ---------------------------------------------------------------------
   ==>A managed Windows server that runs Windows Server Message Block(SMB) based file services.
   ==>Designed for windows and windows applications.
   ==>Supports AD users , access control lists,groups,policies,along with Distributed File System namespaces and replication.

EFS :
    1)A managed NAS Filer for EC2 instances based on Network file system version 4.
    2)One of the first network file sharing protocols native to UNix and linux.



FSx for lustre:
-------------------------------------------------------------------------
==>A fully managed file system that is optimised for compute-intensive workloads.
==>High Performance computing , Machine Learning , Media data processing workflows.
==>Electronic Design automation.


Overview :
-------------------------------------------------------------------------EFS : 
      distributed ,highly resilient storage for linux instances and linux based applications.
Amazon FS for Windows:
      when we need centralised storage for window-based applications,such as sharepoin,Microsoft SQL Server, or any other native Microsoft Application.
Amazon FSx for lustre :
      high speed , high capacity distributed storage.
      used for High Performance Computing , financial modeling etc.
      FSx can directly store data on S3.


AMI
-------------------------------------------------------------------------
      Amazon Machine Image (AMI) provides state information required to launch an instance.
      You must specify an AMI when you launch an instance.

      Five things to specify for AMI.

      1)Region,OS,Architecture(32 / 64 bit ),Launch Permissions , Storage for root device(root device Volume).

==>All AMIs are either backed by Amazon EBS(the root device for the instance launched from the AMI is an AMazon ABS volume created from an Amazon EBS snapshot). or Instance store(the root device for the an instance launched from AMI is an instance store volume created from template  stored in Amazon S3).


Instance Store Volumes:
-------------------------------------------------------------------------
==>also called ephemeral storage.
==>Instance store Volumes can not be stopped .
==>if host fails / delete instance you will loose data.
==>reboot does not cause data to be lost.

EBS Volumes
-------------------------------------------------------------------------

1)EBS-backed instances can be stopped . we will not lose data if instance is stopped . reboot does not cause data to be lost.

2)By default , the root device volume will be deleted on termination . However , you can tell AWS to keep the root device Volume with EBS volume.

AWS BAckup
-------------------------------------------------------------------------
Consolidation : Backup allows you to cosolidate your backups across multiple AWS services , such as EC2 ,EBS , EFS , Amazon FSx for lustre and AWS storage gateway,DataBase (RDS, DynamoDB).

AWS Backup with Organisations:
------------------------------------------------------------
Backup can be used with AWS Organisations to back up multiple AWS Accounts in your organisations.
It gives you centralized control across all AWS services , in multiple Accounts across entire AWS Organisation.


Advantage :
------------------------------------------------------------------
1)Central Management.
2)Automation.
3)Improved Compliance.
