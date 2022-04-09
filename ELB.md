Elastic Load Balancers
---------------------------------------------------------------------------
ELastic load balancing automatically distributes incoming application traffic across multiple targets (EC2 Instances). This can be done across multiple AZ.


1)Application Load Balancers :
---------------------------------------------------------------------
 Best suited for load balancing of http and https traffic they operate at layer 7 and are application aware.(Intelligent Load Balancing)

2)Network Load Balancers :
-----------------------------------------------------------------------
Operating at the connection layer(Layer 4),Network Load Balancers are capable of handling millions of requests per second , while mainatainig ultra low latencies.

Performance Load Balancers

3)Classic Load Balancers :
------------------------------------------------------------------------
You can load balance HTTP and HTTPS applications and use layer -7 specific features, such as X-forwarded and sticky sessions.

classic /Test/Dev Load Balancers.


Health Checks:
-------------------------------------------------------------------------
Health checks periodically sends requests to the the load balancer's registered instances to test their status.
==>Inservice(HEalthy)
==>OutService(Unhealthy)

load balancer sends requests to healthy instances only.






