# ECS-Stack
Code for create a ecs stack, using a web server. The following scripts were used to create the ecs cluster and all its dependencies.

* Master
* Vpc Cloud Formation
* Cluster
* ALB
* Launch Configuration
* Task Definition

## Master file
The master.yml file is the main file for the cloud formation, in which all the stacks are created with their respective parameters.

## VPCCloudFormation file
The VPCCloudFormation.yml is the file in which  VPC, security groups and publics and privates subnets are configurated. With this template only 3 publics and 3 privates subnets are created. This file has the following parameters:

* VPCCidr: The CIRD that you will use in your network.
* PublicSubnet1Cidr: the CIDR of the first public subnet.
* PublicSubnet2Cidr: the CIDR of the second public subnet.
* PublicSubnet3Cidr: the CIDR of the third public subnet.
* PrivateSubnet1Cidr: the CIDR of the first private subnet.
* PrivateSubnet2Cidr: the CIDR of the second private subnet.
* PrivateSubnet3Cidr: the CIDR of the third private subnet.
* AvailibityZone1: The first availibity zone in which the subnets will be created.
* AvailibityZone2: The second availibity zone in which the subnets will be created.

## Cluster
The cluster.yml cotains the script to create the ecs cluster, and only has 1 parameter:

* ClusterName: is the name with which the cluster will be created.

## ALB
In the alb.yml file, all the resources for an applicattion load balancer are created. The objects created are a Target Group, a load banlancer listener and a load balancer. The file has the following parameters:

* SubnetsList: are the subnets on which the load balancer will be hosted.
* LBName: is the Load Balancer's name.
* SecurityGroup: is  the Security Group to apply to the Application Load Balancer.
* TGName: Description: Target group's name.
* VPC: is the VPC on which the Application Load Balancer should be deployed.

## Launch Configuration
In the launchCOnfiguration.yml file the objects needed to host the containers are created. The resources created on this file are the following: a Role to permit the instances register to the ecs cluster, an instance profile thas has all the permissions created in the role, a launch configuration that defines how the instances are created and an Autoscaling grup that uses the launch configuration to create the number of instances defined. This file has the following parameters:

* Ami: Ami that will be used to create the EC2 instances.
* SecurityGroup: Security Group to use in the instances created.
* InstancesType: Instance Type to use.
* EC2KeyName: Keys that will be used to connect to the EC2 instances.
* ClusterName: Cluster´s Name to which the instances will be attached.
* AutoScalingGroupName:  Is the Autoscaling Group´s name.
* DesireInstances:  the aumount of instances that will be online.
* SubnetsList: the subnets on which the instances will be deployed.
* TargetGroup: is the target group to which the instances will register.
* AvailibityZone1: is the first availibity zone on which the instances will be hosted.
* AvailibityZone2: is the second availibity zone on which the instances will be hosted.

## Task and Service definition
In the taskDefinition.yml file the task and service for the ecs cluster are created. This file has the following parameters:

* ImageName: Image's name to use into the containers.
* Memory: Amount of memory to use.
* ServiceName: Service's Name.
* AppContainerPort: Container port of app requiring ELB exposure.
* AppHostPort: Host port of app requiring ELB exposure.
* TargetGroup: The target group to which the containers will resgiter.
* ClusterName: Cluster on which the service will run.
* DesiredCount: Amount of containers online.
