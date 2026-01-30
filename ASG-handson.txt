Here in ASG we have option called launch instance from template, so we don't required to create an instance. ASG will create instances for us.

ASG HANDS ON

First we have to create a launch template from an AMI
then we have to create target group.
(here we have to select instances which we are tagetting. but in this case we are not selecting anything beacuse we are creating instance from ASG)

after that we have to create load balancer
(here we usually select target groups and security group which is created for ALB) 

then we will create an ASG 
 -here we select mainly launch template
 -select availabilty zones
 -select ALB(taget group)
 -check health checks and enable as per your requirements
 -select how many instance you want 
 -next select desired capacities for scale in min and max 
 -select when you will have scale in like cpu utilization cross 70% like that

after creating ASG then check DNS in target group is your website working or not
