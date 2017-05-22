
### Resources


https://d0.awsstatic.com/whitepapers/AWS_Cloud_Best_Practices.pdf
https://d0.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf

## 4 Pillars


1. Security
2. Reliability 
3. Performance Efficiency
4. Cost Optimisation

### Security 

Data protection:
	- encryption of data in transport (SSL) and at rest
Privilege management:
	- protection of root account credentials
	- how is user access to the AWS console controlled with roles and responsibilities
	- how are third party applications, either human or automated being controlled (roles with IAM)
Infrastructure protection:
	- network and host level boundary protections (NACLs and Security Groups)
	- enforcement of AWS service level protection
	- protection of the integrity of EC2 Operating Systems
- Detective controls
- Capture and analysis of AWS logs

### Reliability 

Basic areas: 
- service limits of AWS for your account
- planning of network topology
- escalation path to deal with technical issues
Change management:
- adapting to changes in times of demand
- monitoring AWS resources
- executing change management
Failure Management:
- planning for failures and recovery after failure occurs


### Performance Efficiency

Instances:
    - selecting the appropriate instance type 
    - continuing evaluation of instance types as more instancse are introduced
    - monitoring performance of instances to ensure that their performance is meeting expectations
    - ensuring quantity of instances matches demand
Storage and Database Solutions:
    - selecting appropriate storage and database solutions that meet requirements
    - ensuring capacity and throughput meet demand
Time and space considerations
- proximity to users; caching data


### Cost Optimisation:

match supply and demand:
	- make sure capacity needs are meet by not substantially exceeded; do not place too much emphasis on capacity planning as it may change 
	- autoscaling
cost effective resources:
	- selecting the appropriate pricing model and resources to meet cost targets
	- reserved instances, AWS Trusted Advisor
Expenditure Awareness:
	- processes to monitor AWS spending, access controls to govern AWS costs
	- decommission resources that are not needed; temporarily stop resources that are not required (dev servers)
	- Cloudwatch Alarms, SNS
Optimising over time:
	- adopting new services to reduce costs over the long term
	- AWS blog, AWS Trusted Advisor

