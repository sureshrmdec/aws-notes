## CloudFront

- CDN (content delivery network):
  - System of distributed servers that deliver webpages or other web content to users based on geographic locations of the user


### Cloud Front Terminology:
-  Edge location - location where content will be cached (separate from AWS regions/AZ) - currently 50 edge locations
-  Origin - this is the origin of all files that the CDN will distribute. Can be S3, EC2, Route53 and Elastic Load Balancer
-  Distribution - name given to the CDN that consist of edge locations
-  Web Distribution - typically used for websites
-  RTMP - used for media streaming
- Objects are cached for the life of the TTL, can clear cache but will be charged


### Create Distribution Options:
- Restriction Viewer Access using signed URLs or signed Cookies
- A CDN can have multiple origins - e.g. a CDN can have multiple S3 buckets provisioning data

### Types of CloudFront Distributions:
1. Web distribution - typically used for websites
1. RTMP - used for media streaming
