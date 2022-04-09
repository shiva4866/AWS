AWS Infrastructure:
  Regions : locations contains multiple available zones separated by distances
  Availability Zone : multiple data center
  data center : building with servers
  Edge Location : endpoints for aws for caching content



Who owns what in cloud ? 
----------------------------------------------------
shared responsibility model important for exam 
    AWS Responsibilities :==> security ,regions, AZ ,data centers security and maintenance policies
                           virtualization,hardware management
    your responsibility : security of customer data , your platform , access management
                         network firewall , protect network platform,encryption ,IAM


You are responsible for things whom you can control(can I do this in AWS console)
else AWS is responsible

for encryption both are responsible(shared responsibility)



Service in AWS : 
 Compute : 1)EC2 2)Lambda 3)Elastic beans
 Storage : 1)S3 2)EBS(virtual Hard disk) 3)EFS(Elastic File Storage) 
           4)FSx  5)Storage gateways

 Databases : 1)Reliable way to store and retrieve data in
             1)RDS  2)DynamoDB 3)Redshift

Networking : db comminicate  1)VPCs 2)Direct Connect 3)Route53 4)API Gateways
             5)AWS Global Accelerator

**important read papers
Well architecture framework : 1)Operational Excellence(focuses on running and monitoring systems to deliver business values, and continually improvig process and procedures)
2)security 
3)Reliability
4)Performance efficiency
5)Cost optimization


Identity Access Management : 1)way of granting and accessing level and access to cloud resources to users ,
2)root account : (email address to signup ) , admin permissions : (security is main concers) ( us-east 1 region is default region)



Multifactor Authentication : 1)to secure root account
                             2)Create admin groups stop using root account
                             3) User accounts and assign permissions them



Example of policy document
--------------------------------------
JSON Statement : 
{
    "version": "2012-10-17",
    "statement":[
        {
            "Effect": "Allow",
            "Action": "*",
            "Resources":"*"
        }
    ]
}

1)This provides all access of resources to the account
2)Take policy documents and assign them Groups , Users ,Roles
3)Best practice is to add users to a group and assign them appropriate permissions using JSON statements

==>IAM does not require region selection(It a universally created):
===> Policy ==>create policy (use customs policy eg access to S3 full access , search by roles administrator)
==>on clicking policy you will see the JSON Documents

==>look at JSON Documents before going to exam
--------------------------------------------------------------


Building Blocks of IAM : 
   Users => A physical person
   Group =>Functions such as developers , admin etc contains Users
   Roles =>Internal Usage within AWS

1)its best practice for users to inherit permissions from groups
2)making change at group level than individual level
3)1 Users == 1 Physical Person ( to track the activities) 
4)Only assign a user the minimum amount of privileges they need to do Job

Tips
----------------------------------------------------------------
1)IAM ==> Add user to group they inherit the permissions from group

2)New Users does not have any permissions by default

3)access key id and secret access key are not same as username and password(they are actually used for programatic access)(save download and send them to users). they are generated when allowed programatic access

4)Root account : This is the account created when first set up your AWS account and it has complete admin access. Secure it as soon as possible and dont use it to log in day to day

5)Always set up password rotation : You can create and customise your own password rotation policies.(eg password expires after 90 days , remember last 5 passwords etc ( these are policies))

6)IAM Federation : You can combine your existing user account with aws .   for eg when u log on to your pc (usually using microsoft active directory ), u can use same credentials to log in to AWS if you set up federation

7)Identity Federation : Uses the SAML standard , which is active directory


Policies 
--------------------------------------------------------------------------------------------------------
1)Inline Policies : Policies are defined at user level
2)AWS Managed Policies :An AWS managed policy is a standalone policy that is created and administered by AWS. Standalone policy means that the policy has its own Amazon Resource Name.
