EC2 Overview : 1)Elastic compute cloud  

               2)Secure , resizable compute capacity in cloud  

               3)Its  virtual Machine hosted in AWS   

               4)designed t web scale cloud computing easier for developers 

               5)You have complete control over your own instances  



==>Pay for what you use 

==>scale compute capacity in cloud

==>its very fast delivery(in few minutes)


pricing
------------------------------------------------------------------------
1)On - demand (based on hour or second depending on what type of instance you run)

2)Reserved(1 to 3 years) discount upto 72%

3)Spot-purchase unused capacity at discount of upto 90%

4)dedicated-A physical EC2 server dedicated for your use.most expensive



On-demand instances
------------------------------------------------------------------------
1)short time , dont know market react to your product , flexibility , test and dev

2)Reserved => predictability , specific capacity requirements , pay upfront to reduce total computing costs
     Convertible Reserved Instances , (can be changed in the future)


     Scheduled Reserved Instances ==> define time window for capacity requirements,

reserved Instances operate at regional level

save upto 72%

super flexible

3)Spot Instances ==>prices move around with supply and demand

                 ==>applications that have flexible start and end timestamp

                 ==>Image rendering , genomic sequencing , Algorithmic trading engines


dedicated Instances ==> multi-tenant virtualisation is not there(dont share hardware with others)

==>Licensing

==>Reserved

AWS pricing calculator looks at it.



Demonstration
----------------------------------------------------------------------------
1)go to EC2 2)==>Launch Instance 3)select an image ==> choose instance type(t2_micro)  4)fill the values 5)subnet(availability zones) select no preferences

6)add storage(virtual hard disk)

7)add tags(department - applications team)

8)configure security group

9)review 

10)create security key(ssh key) , download security key 

11)launch


connect
-----------------------------------------------------
EC2 instance connect , hit connect

sudo su(root access)

yum update -y(update with latest security patches)

after use terminate the instance



AWS command line interface
----------------------------------------------------------------------------
aws service_name command

eg aws s3 ls ==> list all the s3 buckets

1)Launch instance

2)copy ip address

==>change chmod 400

3)ssh ec2-user@ip_address -i MyNVKP.pem

4)sudo su(root access)

5)yum update -y(update with latest security)

6)aws configure

   create ==>IAM ==>New Group ==>Add create user and that to the group(programatic access)
   paste access key id , secret access key id(remember it or save it)

==>$aws s3 ls

==>$aws s3 mb s3://bucket_name(create bucket)

==>$echo "hello" > hello.txt

==>$aws s3 cp hello.txt s3://bucket_name ( upload file to bucket )



IAM role
----------------------------------------------------------------------------
1)Ask yourself ques whats your role you have been assigned.(role is policy document and can be assigned to any , user or group)

2)its an AWS Identity

3)Roles are temporary.when you assume role you are provided with temporary security credentials for your role session



IAM =>create Role=>select Ec2 =>select s3 policy (s3 full access) => create Role.

1)Launch an instance(in configuration ==>role(the name of role(eg s3Access))

2)connect to EC2 instance

3)aws mb s3://bucket_name

4)aws s3 ls



Basic Human senses => sensors temp , light , sound ==>()

                   =>Linux administered using ssh port 22

                   =>rdp in windows port 3389

                   =>http port 80

                   =>https port 443

security groups : virtual firewalls for ec2 instances

                  by default everything is blocked

                  to let everything int 0.0.0.0/0 for communication , you eed to open up the correect ports


Bootstap scripts : A script which runs when the instance first run

                 ==>yum install httpd -y(installing apache server)

                 ==>yum service httpd start(start the http server)

                 it passes user data to ec2 instances and can be used to install applications as well as do updates and more


Tips
---------------------------------------------------------------------
1)Changes to security groups take effect immediately

2)you can have any number of ec2 instances running within security groups

3)you can have multiple security groups attached to ec2 Instances

4)All inbound traffic is blocked by default

5)All outbound traffic is allowed.


EC2 Metadata and user data
-----------------------------------------------------------------------
metadata = > data about data i.e data about ec2 instances , ip adress(private and public) , hostname
 type command

=>curl http://169.254.169.254/latest/meta-data/local-ipv4|ec2-user@ip-12-31-31-0~|$ curl http://169.254.169.254/latest/meta-data/


we can also write ootstrap scripts


=>user-data is bootstrap script




Networking with EC2
-------------------------------------------------------------------------
ENI(Elastic network Interface) for basic day to day networking.

Enhanced Networking(EN) Uses Single root I/O virtualisation (SR-IOV) to provide high performance

EFA(Elastic Fabric Adapter):Accelerates High performance computing (HPC) and machine learning applications.



An ENI is simply a virtua network card

=>private ipv4

=>public ipv4

=>Many ipv6

=>MAC Address

=>1 or More Security groups


Usecase 
-----------------------------------------------
1)Create Management networking

2)Use network and security appliance in your VPC

3)Ceate Dual-homed instances with workloads/roles on distinct subnets

4)Create low budget , high availability solution


Enhanced Networking(EN):Higher bandwith , lower inter instance latency






Optimise EC2 with placement groups
------------------------------------------------------------------------

1)Cluster Placement Group : Grouping of instances within Single Availability Zone. Recommended for low network latency and high network throughput or both.

2)Spread placement Group : Group of instances that are placed on distinct underlying hardware.

Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other.(backup)

3)Partition Placement Group : Each Partition group has its own set of racks .Each rack has its own network and power source. No Two Partitions
within a placement group share same rack allow you to isolate the impact of hardware failure with your application.


==> A placement group can't span multiple availability zones while others can.

==>Only certain types of instances can be launched in placement group .(compute optimised , GPU,Memory,storage optimised).

==>AWS recommends Homogeneous instances within cluster placement groups.

==>You cant merge placement groups.

==>You can move an instance into placement group but it must be in stopped state before proceeding.(AWS CLI/SDK can do that not via console)







Spot Instances
------------------------------------------------------
1)Unused EC2 instances can be purchased on 90% discount.

2)Used when stateless , fault tolerance or flexible applications

3)Decide Maximum spot price , if price is above your instance is terminated.

4)SPot block ( 1 to 6 hours stops your instance from being terminated)


Spot Instances not used in
---------------------------------------------------------------
Not used in persistent workloads and

Critical Jobs

Databases


