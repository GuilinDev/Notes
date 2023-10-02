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
62. A retail company -> transit VIF + DX-B + cross-Region routing
63. 