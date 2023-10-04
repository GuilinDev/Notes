### 159
1. Revamping -> SQS
2. Windows + Linux -> Systems Manager
3. CloudFront, API Gateway, Lambda + CLI -> AWS SAM + Code Deploy + CloudWatch
4. SCP 1111-1111-1111 -> IAM + S3
5. Finacial Linux EC2, I/O -> RDS + read replica
6. CloudFormation with RDS, EBS -> DeletionPolicy
7. EC2 with ALB, EFS, blog -> CloudFront + S3
8. IoT platform -> 1) Kinesis/Lambda, 2) DynamoDB
9. migrate legacy to AWS -> 1) ENI/S3; 2) EC2/IP/AMI
10. 4kb, 120 days -> DynamoDB TTL
11. AWS Marketplace -> IAM root level
12. NET 200,000 daily users -> CloudFormation , ALB, Multi-AZ
13. (OU) -> SCP/OU
14. TCP/SO -> NLB/alias
15. multiple AWS accounts -> 1) new VPC in account B, 2) new VPC in account B
16. upload short videos -> S3/SQS/Rekognition
17. monolithic, CI/CD -> CI/CD, URLS
18. Organizations with a single OU -> OU, root SCP
19. weather service -> 1) S3 bucket in us-east-1, 2) Lambda@Edge/S3 bucket
20. NA Company East Coast -> ALB + failover
21. A company AWS Lambda -> AWS CLI update-alias
22. An AWS partners -> ARN/ID
23. A solution architect needs -> SQS + S3 bucket
24. A security engineer -> Secretes Manager with RotationSchedule
25. A company two-tier -> Aurora Replicas + round robin
26. A company..internal cloud billing -> AWS Budgets/organization's master account
27. on-premises monitoring solution using fa PostgreSQL -> 1) Kinesis Firehose + Lambda, 2) ElasticSearch + Kibana
28. AWS Organizations to manage multiple AWS accounts -> master account + CloudFormation automatic deployment
29. A life Science company + SAN -> AWS DataSync
30. CIDR -> public IP + Elastic IP
31. hybrid DNS solution -> Route53 inbound Resolver + all VPCs
32. A startup -> IAM role
33. Windows file server -> FSx
34. several projects on several AWS accounts -> 1) AWS Config rule; 2) SCP; 3) AWS Config aggregator
35. many AWS accounts and uses AWS Organizations to manage -> 1) resource sharing ; 2) OU + each subnet
36. large company EC2 Linux -> Auto Scaling Terminate process + session manager
37. Migrate from VMware to on-premises data center -> VMware vSpehere
38. multiple AWS accounts and Regions -> 1) IPv4 CIDR; 2) IAM role
39. patching processing -> Systems Manager
40. proprietary stateless ETL -> AWS Fargate
41. 50 AWS accounts -> 1) AWS Resource Access Manager; 2) AWS CloudFormation Stack Sets
42. finance company hosts a data lake in S3 -> SFTP server to AWS Transfer
43. balance traffic across a group of Amazon EC2 instances -> Place the EC2 behind ALB + provision a third-party SSL
44. several workloads in a single AWS account -> IAM policy + IAM role + IAM service
45. global offices has a single 1 Gbps AWS Direct -> provision a Direct Connect gateway
46. a large number of AWS accounts -> VPC prefix list
47. multiple DevOps teams -> 1) AWS IAM; 2) Remove default FullAWSAccess SCP; 3) OUs;
48. ALB, RDS, SIA -> Store Docker images in ECR
49. NodeJs, MySQL -> Aurora MySQL + AWS DMS + RDS Proxy
50. EC2 instance, log files -> Systems Manager + EventBridge (CloudWatch Events, not SNS)
51. 72-hour run/LARGEST overall cost reduction -> S3 Intelligent-tiering + FSx for Lustre
52. on-premises/NoSQL MongoDB -> DocumentDB with appropriately sized instances
53. Multi-AZ VPS/Cost Explorer -> interface VPC endpoints + VPC endpoint policy
54. sequel fora -> create another S3 bucket in a new Region
55. OU -> Organizations management account
56. A company's factory -> 1) Activate the user-defined; 2) Create a cost category; 3) Enable Cost Explorer
57. AWS WAF -> AWS Firewall Manager
58. analyze a company's Amazon EC3 instances -> Install the Amazon CloudWatch agent on the EC2 instances +  AWS Compute Optimizer
59. single AWS Region + SQS -> 1) Deploy SQS Lambda; 2) Subscribe the SQS in each Region to the SNS topic
60. video streaming company -> 1) Enable S3 Transfer; 2) break videos into chunks
61. A company is storing data in several Amazon DynamoDB -> 1) API Gateway REST API; 2) API Gateway HTTP API + Lambda
62. A retail company on-premises data center in Europe -> transit VIF + DX-B + cross-Region routing
63. REST API/PUT -> 429
64. A retail company S3 bucket -> 1) Account A, set S3 bucket policy; 2) Account B, set permissions of User DataProcessor;
65. many AWS accounts/IP CIDR -> customer-mamaged prefix list
66. AWS WAF -> Set the action of the web ACL rules to Count Enable AWS WAF logging
67. CMK -> kms:GenerateDataKey
68. Cost Explorer -> IAM policy + IAM group + IAM accounts
69. electronic document management system -> 1) Enable S3 Transfer Acceleration; 2) Change the API Gateway Regional endpoints to edge-optimized endpoints
70. PII -> SSE-KMS, S3 bcket policy to deny unencrypted PutObject requests
71. SaaS/REST API/429 -> API Gateway account limit for calls per second
72. two OUs: Research and DataOps -> 1) SCP + aws:RequestedRegion; 2) SCP + ec2:InstanceType
73. S3 gateway VPC endpoint
74. video processing -> AWS Snowball Edge Storage Optimized device
75. Windows Amazon EC2 -> FSX
76. digital marketing + KMS -> 1) bucket policy that includes read permissions; 2) Update the custom KMS key policy; 3) Update the strategy_reviewer IAM role to grant read permissions 
77. MySQL -> read replicas on Amazon RDS, cross-Region read replicas
78. external audit -> CloudTrail + AWS identity and Access Management Access Analyzer
79. work remotely at their homes -> VPN endpoint + internal applications
80. order-processing/Rabbit MQ -> AMI + Amazon MQ + EKS
81. hundreds of AWS accounts/Reservated instances -> 1) all AWS accounts with all features enabled; 2) SCP
82. MFA -> 1) AWS Control Tower; 2) transit gateway; 3) AWS SSO
83. MySQL -> RDS Proxy; 2) Lambda function
84. DynamoDB -> during peak period + researved RCU/WCU
85. third-party SaaS -> PrivateLink
86. ALB -> provision an ALB
87. AWS Direct Connect connection -> 1) transit gateway; 2) transit gateway attach; 3) private subnets
88. RDS Multi-AZ DB -> RDS proxy
89. several AWS accounts -> 1) centralized account + Lambda service as a trusted entity; 2) other AWS accounts with minimal permissions
90. large number of archived documents through VPN -> S3 One Zone-Infrquent Access
91. forms-processing application -> AWS Step functions + Amazon Textract
92. adventure company -> S3 Intelligent-Tiering
93. A company has an asynchronous HTTP -> API Gateway endpoint + Route 53
94. A company is hosting a critical application on a single Amazon EC2 instance -> 1) ELB + Auto Scaling group; 2) DB instance for Multi-AZ deployment; 3) ElastiCache + Multi-AZ
95. monolithic REST-based API -> Separate API into Lambda functions
96. unstructured data in S3 -> AWS Glue Data Catalog + Athena
97. video processing company with images -> 1) ECR; 2) ECS + Fargate
98. auditing the security setup -> IAM database
99. refactor application as microservices in 2 environments ->  ECR + 2 ECS with Faragate
100. AWS Organizations allows experiment on AWS -> 1) AWS Budgets; 2) SCP to deny; 3) AWS Budgets alert + SNS;
101. The workloads run on Linux and Windows -> 1) AWS Application Discovery Agent; 2) AWS Migration Hub; 3) recommend instance types + Migration Hub
102. three-tier web application -> 1) S3 + CloudFront; 2) Rehost the Java appliation in Beanstalk; 3) AWS DMS
103. A publishing company -> 1) production account, IAM policy + S3 bucket; 2) production account, Attach the new policy; 3) in development account, create a group + IAM policy
104. fleet of AWS EC2 -> SNS
105. A company uses an on-premises data analytics platform. -> three instances
106. A company has created an Amazon CloudFront distribution with two Amazon S3 buckets as origins -> OAI + S3 bucket policy
107.  management account 
108. CloudFront
109. com.amazonaws.region.elasticloadbalancing VPC interface endpoint 
110. API endpoint from 
111. AWS Organizations and AWS CloudFormation StackSets. 
112. In the AWS Billing and Cost Management console, use the organization's management account 
113. oute 53 Resolver outbound e + AWS RAM
114. 1) Amazon EventBridge rule 2) Invoke an AWS Step Functions 3) SNS
115. Use AWS Transfer Family to create an FTP
116. 1) RDS Proxy 2) Migrate the database to Amazon Aurora MySQL 3) Create an Amazon Aurora Replica
117. IAM role + DBA-Secret + DBA-Admin
118. Use the AWS Schema Conversion Tool
119. Provision an Aurora Replica in a different Region
120. Use an Amazon DynamoDB table to store the spam numbers
121. Turn on SSE-S3 on both S3 buckets.Use S3 Batch Operations
122. Use AWS Control Tower
123. 1 Deploy the security 2）Provision a Gateway Load Balancer
124. Lambda function that starts instances
125. Glue + Invoke an AWS Lambda function
126. Configure scale-in protection for the instances during processing
127. Increase capacity
128. CloudWatch console + "like 198.51.100.2"
129. Attach a rol
130. 1) ELB + Auto Scaling group 2) Modify the DB instance to create a Multi_AZ deployment 3) Create a replication group for the ElastiCache for Redis cluster. Enable Multi-AZ on the cluster
131. AD Connector to connect to the company's on-premises Active Directory Configure IAM Identity Center and set the AD Connector 
132. SSO + Active Directory
133. failover record
134. 1) Activate the user-defined cost allocation tags 2) Create a cost categor 3) Enable Cost Explorer
135. 1) Create an Amazon S3 bucket. 2)  Add a custom error response
136. 1) Create an AWS Lambda function 2) Create an Amazon CloudFront distribution 3) Create an SSL certificate
137. 1) Configure the loT 2) Write the metadata to Amazon DocumentDB 3) Use AWS Step Functions 
138. Provision a transit gateway in an account in each OU.
139. AUTH token + AWS Secrets Manager
140. Amazon Pinpoint 
141. 1) Create an Amazon S3 bucket.  2) Add a custom error response 
142. SQS
143. Add a security group rule to the ALB to allow traffic from the AWS managed prefix list for CloudFront only
144. Set up AWS IoT Core 
145. AWS Databnse Migration Service (AWS DMS) to rehost the database. 
146. ECR + ECS + Fargate
147. S3 event notificatin + Lambda function
148. 1) bucket policy to allow a user 2) IAM policy in the destination account 3) s3 + destination account
149. VPC peering + multi-Region
150. 1) Associate an AWS Lambda function 2) Modify the S3 bucket resource 
