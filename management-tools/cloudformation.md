### Resources

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html

### Templates

A template is a declaration of AWS resources that make up a stack, stored as a JSON file. Cloudformation interprets the JSON file to declare resources.

#### Template Structure

Format Version: optional, specifies the AWS Cloudformation template version to which the template conforms. Not the same as the API and WSDL version.

Resource Properties:
Additional option that are specified for creating a resource, e.g. specifying an AMI.

Resource Attributes:
- CreationPolicy - prevent a resource from indicating it has completed creation until AWS CloudFormation receives a specified number of success events or timeout period is exceeded
- DeletionPolicy - allows the preservation or backup of a resource when the stack is deleted
- DependsOn - specifies the creation of a specific resource after the creation of another resource
- Metadata - enables you to associate structured data with a resource
- UpdatePolicy - specify rolling updates or 

Intrinsic Functions: used to select or join values in the template

Pseudo Parameters: 

Helper Scripts: 

