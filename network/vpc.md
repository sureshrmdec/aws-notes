# VPC

- 5 VPCs per region by default
- 1 Internet Gateway per VPC
- A VPC spans all availability zones in the region
- Subnets that have a route to a Internet gateway are known as public subnets, likewise subnets that don't have a route to the Internet gateway are private subnets
  - If a subnet does not have a route to the Internet gateway, but has its traffic routed to a virtual private gateway for a VPN connection, it is known as VPN-only subnet.
- Instances within public subnets that need to communicate with other parts of the internet must have a public IP address assigned to them.
-


## Highly Avaliable Architecture

- Architecture suggestion: at least 2 private and 2 public subnets for high availability as a subnet can only be associated with an availability zone.
- ELB's are required in 2 or more public subnets in 2 or more availability zones to ensure high resiliency
- Put Bastion hosts behind autoscaling groups with a minimum size of 2. Use Route53 to automatically failover if one bastion host fails.
- For NAT instances, a NAT instance is needed in each public subnet, with their own IP address and there needs to be a script to ensure failover between the two. Use NAT gateways instead.


## NAT Instances

- when creating NAT instance, disable Source/Destination check 
  + EC2 instances perform source/destination checks by default, as a NAT instance sits between the source or destination EC2 instance, this check must be disabled to route traffic through the instance.
- must be in a public subnet
- must be a route out of private subnet to the NAT
- amount of traffic the NAT instances supports, depends on the instance size. Bottlenecking is solved by increasing the instance size
- can create high availabilit using Autoscaling Groups, mutliple subnets in different AZ's and script to automate failover

## NAT Gateways

- newer
- preffered by enterprise
- scale to up to 10Gbps
- no need to patch
- not associated with security Groups
- automatically assigned a public ip addresss
- need to update route tables



| Network Access Control Lists | Security Groups  |
|--------|--------|
|    operates at the subnet level (second layer of defence)    |        |
| supports allow and deny rules | Only Allow rules |
| is stateless: return traffic must be explicity allow by the rules | Is stateful process |
| all rules evaluated in order 1 subnet per NACL |rules in order (like IPTables) |


## Bastion Hosts

- used to securely administer EC2 instances

## VPC FlowLogs

- logs all activity that occurs within a VPC to CloudWatch

## VPC Limits

https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Appendix_Limits.html
- VPCs per region: 5 (can be extended by a request)
- Subnets per VPC: 200 (can be extended by a request)
- Elastic IP addressses per region: 5
- Flow logs per single network interface, subnet or single VPC: 2
- Customer gateways per region: 50, all other types of gateways have a limit of 5
- NACLs per VPC: 200
- Rules per ACL: 20
- Network interfaces per region: 350
- Route tables per VPC: 200
- Security groups per VPC: 500
- Rules per security group: 50
- Security groups per network interface: 5
- Active VPC peering connections per VPC: 50

## Setting Up A VPC

1. Go 'Your VPCs' in the AWS VPC Dashboard and hit Create VPC
  2. Main route table, default Security Group and default NACL are created when the VPC is made  
2. Name the VPC and specify a CIDR block consisting of private class IP address 10/172/192 CIDR blocks. After creating a VPC subnets can be added as CIDR subsets of the VPC CIDR block. (Each subnet must reside within 1 AZ.)
  3. #### Subnetting
    1. From /16 to /28 netmask (16 to 65,536 addresses)
    2. Private (non-publicly routable) IPv4 addresses:
      3. 10.0.0.0 - 10.255.255.255 (10/8 prefix)
      4. 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
      5. 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)
    6. Subnetting example:
        7. 10.0.0.0/16 (supports 65k address) this can be broken into 2 subnets, 10.0.0.0/17 and 10.0.128.0/17, being the network addresses of the 2 subnets.
        8. 10.0.1.0/24 and 10.0.2.0/24 might be more common examples of subnetting
        9. Important:
          10. x.0.0.0 is a network address;
          11. x.0.0.1, x.0.0.2 and x.0.0.3 are reserved by AWS
          12. x.0.0.255 is a network broadcast address
  13. #### Subnet Routing
    14. https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Route_Tables.html
    14. Each subnet must be associated with a route table, which specifies the allowed routes for outbound traffic leaving the subnet
    15. An Internet gateway must be attached to the VPC to allow public subnets to route their traffic to it
    16. A subnet can only be associated with one route table, but mutliple subnets can associate with the same route table
    17. Subnets not explicitly associated with a route table are implicitly associated with the main route table that comes with the VPC
    18. To make a route, in the route table specify a destination CIDR and a target
    19. To best protect the VPC, the main route table is left in its original state and each new subnet is explicitly associated with one of the custom route tables. (This ensures explicity control.)
    20. More traffic is routed to more specific destinations over less specific destinations, e.g. 0.0.0.0/0 vs 172.32.1.0/24 (more specific destination)
    21. Remember to select auto-assign public IP address for instances that reside in public subnets
  14. #### Configuring Security Groups
    15. Create Security Groups in the VPC dashboard:
      16. Can specify rules such as allowing all source traffic from 0.0.0.0 to reach SSH; but only allowing traffic from certain subnets to reach ports like 3306 (MySQL)
  16. #### Adding NAT Gateway/Instance
    17. Deploy NAT Gateway into public subnets
      18. For NAT instances, apply a SG and in the private route table create an route that routes traffic from the internet (0.0.0.0) to the NAT instances
      19. NAT Gateway:
        20. Create NAT gateway in public subnets
        21. Assign it a public IP
        22. Edit Route Tables and add external internet traffic to target that NAT Gateway
  18. #### Network ACL
    19. Create new NACL with name and assign to VPC
    20. All inbound and outbound traffic is denied by default*
    21. Assign NACL with the subnets that are required (this will deassoicate the default NACL)
    22. Edit rules to allow Ports/IPs and Types to be assigned to the rules of the NACL, which are evaluated in order.
### Cleaning up


### VPC Peering

- allows connection between VPCs within a single region
- transitive peering is not supported
- CIDR blocks of different VPCs cannot overlap or match

