Create a VPC
---

In the AWS management console select the region
that we want to create the VPC in because it's a regional service.
We then create a VPC and we need to specify the CIDR block for that VPC. And then we're going to deploy some subnets. And those subnets each get attached to an availability zone. So I create my three public subnets and each of those will need an IP address block from the CIDR address block of the VPC. And we'll then need three private subnets and each of those will also need its own IP address range.

![vpc](/image/1.png)

I use the IPv4 Subnet Creator from [network00.com](https://network00.com/NetworkTools/IPv4SubnetCreator/) to work out the address block and the subnets that are going to be within that address block. So I chose 10.0.0.0 with a slash 16 subnet mask, and that's going to give more than 4,000 hosts per subnet. And we're going to use six of these for these six subnets that we create in our new VPC.

![subnets](/image/2.png)

Go over to the AWS management console and start building this out.
In the AWS management console and I'm choosing North Virginia.
![console](/image/3.png)

Let's go to VPC. In the VPC management console, you'll see there's a VPC wizard.
![wiz](/image/4.png)
it gives you a few different options for creating certain topologies. You can have a VPC with a single subnet, VPC with public and private subnets. A VPC with public and private subnets and hardware VPN access. Or a VPC with a private subnet only and a hardware VPN access.
![wizard](/image/5.png)
 We're not going to do that. We're going to do it manually.

So, let's choose create VPC. We can see we have the default VPC here, but we're going to create our own. So, let's choose create VPC.
![create](/image/6.png)
And then specify my CIDR address block.That's going to be 10.0.0.0/16. For now, we're going to leave the No IPv6 CIDR block.

Now, tenancy, what this means is you can change from default to dedicated. If you do that, when you launch EC2 instances into your VPC, they'll be on dedicated hardware. That's going to cost you a lot more money. So we're going to leave that as default and choose create VPC.

![ec2](/image/7.png)

So we now have a VPC, we've got a VPC ID.

![newVPC](/image/8.png)

The tenancy is default and this is not a default VPC. We get a DHCP option set. We can see our CIDR block, DNS hostname is disabled and then we've got a route table.
Every VPC has a main route table and we're going to edit that one and create our own. DNS resolution is enabled and it has a network ACL, which is assigned, That's essentially a subnet level firewall.


So lets create our subnets. We can see that we have six subnets that exist already and these are in the default VPC.

![subcreate](/image/9.png)

If you scroll across a little bit further, you'll see that in the availability zones, There are six availability zones in this region, the US-East 1A through to 1F.

![avail](/image/10.png)

We're going to create three public subnets and three private subnets and I'm going to split those across A, B, and C. So let's choose create subnet. We now have to specify the VPC, so make sure you choose the one with the custom CIDR block.

![choose](/image/11.png)

For the subnet name, what I'm going to do is I'm going to choose the availability zone and then I'm going to call it either public or private. So this is going to be a public subnet and then -1A. I'm not going to add anything else. Just create the subnet.

![1a](/image/12.png)

So that's our public subnet.

The only other thing I need to do for a public subnet is I need to modify the auto-assign IP settings. I'm going to select this option here, enable auto assign public IPv4 address.
![auto](/image/13.png)

![save](/image/14.png)

That means that every EC2 instance that we launch into the subnet will get a public IP address. Click on save.

The other thing that we need to do, which I'll do in another lesson, is create an Internet gateway, attach it to the VPC and specify in the route table.

So we just need to go in and do exactly the same thing for all the other subnets. So again, I come in, I'm going to call this one public-1B, specify 1B as the availability zone,

![1b](/image/15.png)

Then go back to [network00.com](https://network00.com/NetworkTools/IPv4SubnetCreator/)

![net00](/image/16.png)

Copy my next subnet block.
Paste that in and then click on create subnet.
![pastein](/image/17.png)

I'm not going to show you every single one of these, it's the same process for all six. just create three public and three private. Just remember, for the public subnets, you need to modify the auto-assign IP settings. I've finished creating all my subnets now, so I've now got a private 1A, 1B, and 1C and public 1A, 1B, and 1C.

![finish](/image/18.png)

If we scroll across the public subnets, should..have the auto-assign public IPv4 address set to yes. Make sure that that's definitely the case.

![auto assign](/image/19.png)

next I will show how to attach an Internet gateway to the VPC to create a separate route table for the private subnet.
