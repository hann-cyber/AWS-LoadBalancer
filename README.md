# Implementing a Load Balancer within AWS Cloud
The following is a guide to adding a load balancer to Amazon EC2 instances.

The idea is that you have incoming traffic from multiple users and, rather than straining the load of a single instance, you would like to spread the traffic across multiple instance. An added benefit for using a load balancer is you do not have to display your assets (instances) to the public. Instead, clients will connect to the publicly exposed load balancer, which will automatically direct traffic to your assets evenly and in the background.

1. First step is to make sure you have at least 2 instances running. Here, I have created two separate instances for this demonstration.

<p align="center">
 <img src="https://i.imgur.com/gO625eF.png">
</p>

You'll notice in the following screenshot that each browser is directed to a different public IP address for the varrying instances, which are running on separate machines within AWS. Note: I have a start up script to list the device's hostname on the landing page and
<b>the public IPs are 3.135.212.224 & 18.191.233.29</b>. 

<p align="center">
 <img src="https://i.imgur.com/NhyCt96.png">
</p>

2. Now I'm going to create a load balancer to more evenly divide incoming traffic!

<p align="center">
 <img src="https://i.imgur.com/ELGpwFr.png">
</p>

The following image shows the different types of load balancers and how they work.

<p align="center">
 <img src="https://i.imgur.com/WTdNyxz.png">
</p>

3. I selected the application load balancer option and, as illustrated in the following image, I chose internet facing with IPv4 since I want it available to the public via IPv4 address.

<p align="center">
 <img src="https://i.imgur.com/dvfVe3K.png">
</p>

Under network mapping I opted to deploy the load balancer to all availability zones.

<p align="center">
 <img src="https://i.imgur.com/Z2ZiPjc.png">
</p>

4. Here, I opted to create a new security group. You'll see in the following image I wanted to allow all sources (0.0.0.0/0) access via HTTP on port 80.

<p align="center">
 <img src="https://i.imgur.com/zLOwv0m.png">
</p>

If you're following along you have to hit the refresh icon before your newly created security group is shown.

<p align="center">
 <img src="https://i.imgur.com/gH4jXcg.png">
</p>

5. Back in the configuration menu I have to create a target group for all routed traffic.

<p align="center">
 <img src="https://i.imgur.com/aHbG0fk.png">
</p>

In this case, they will be the 2 EC2 instances I created before starting.

<p align="center">
 <img src="https://i.imgur.com/aL5su4K.png">
</p>

More configuration options.

<p align="center">
 <img src="https://i.imgur.com/Ghr5jjV.png">
</p>

Here I select all the desired instances that are available.

<p align="center">
 <img src="https://i.imgur.com/x0mwnay.png">
</p>

As before, when creating a new policy we hit refresh and select the desired group policy.

<p align="center">
 <img src="https://i.imgur.com/m0lCAhF.png">
</p>

6. Creat the load balancer!

We must wait for the load balancer's state to update from provisioning to active.

<p align="center">
 <img src="https://i.imgur.com/vo4FwON.png">
</p>

Once it's active, a DNS name is provided.

<p align="center">
 <img src="https://i.imgur.com/5RYr3vE.png">
</p>

7. Navigating to the provided DNS name multiple times will provide different results as the loadbalancer is directing traffic to different instances and displaying the startup script from the other host.

<p align="center">
 <img src="https://i.imgur.com/K4u3Th0.png">
</p>

Keep note that the load balancer address is the same unlike the public IPs from step 1.

<p align="center">
 <img src="https://i.imgur.com/jIOpc1d.png">
</p>

Another benefit of using a load balancer is it automatically detects the health status of an available instance. In the event an instance is found to not be available then the load balancer will direct traffic to the next available instance, automatically. You can see the load balancer detect health status in the following images where I intentionally stop an instance to test the load  balancer's efficacy.

<p align="center">
 <img src="https://i.imgur.com/BQMvgT7.png">
</p>

Stopping the instance.

<p align="center">
 <img src="https://i.imgur.com/27iWDpJ.png">
</p>

Load balancer not using the stopped instance:

<p align="center">
 <img src="https://i.imgur.com/kMXyCwC.png">
</p>



Click this [next project link](http://github.com/cyber-hann/AWS-ASG/) to see my next article on Automatic Scaling Groups!
