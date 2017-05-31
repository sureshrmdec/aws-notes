## Security Token Service (STS)

### Overview
Grants users limited and temporary access to AWS resources.
Three sources of authentication for users:
1. Federation (Active Directory)
 - uses SAML and grants temporary access based off Active Directory credentials
 - single sign-on allows users to log in to AWS console without assigning IAM credentials
2. Federation with Mobile Apps
 - use Identity Access Providers (Google, FB etc) to login
3. Cross Account Access
 - allow access to users from one AWS account to an external AWS account using roles and STS policies

#### Rolling your Own Federated Access Architecture
1. Develop an Identity Broker to communicate with LDAP and AWS STS
2. Identity Broker always authenticates with LDAP first, then with STS (or gets an IAM Role associated with that user - the application then authenticates with STS and assumes that IAM role)
3. Application then gets temporary access to AWS resources, includes using an IAM role
