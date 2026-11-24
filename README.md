# AWS-LOAD-BALANCER
# EX 6B AWS LOAD BALANCER
## NAME: Hamdhan
## REG NUMBER: 212225020013
## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.
### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT
<img width="1920" height="1080" alt="Screenshot 2026-11-24 083252" src="https://github.com/user-attachments/assets/68495d5c-d7b4-40d7-a3db-f22b687f7a1c" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 083651" src="https://github.com/user-attachments/assets/5b74785b-43d6-435c-b3bf-fe230fff0a95" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 084246" src="https://github.com/user-attachments/assets/7ad1373c-b179-4038-b31d-ae178930a337" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 084642" src="https://github.com/user-attachments/assets/aa3871de-2e46-45bb-b9e9-7e4a340f6936" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 085725" src="https://github.com/user-attachments/assets/aec9d21f-5663-4c27-ab3c-4b9755e36763" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 085956" src="https://github.com/user-attachments/assets/9e7a696c-6344-49f9-9790-6c321b74cc79" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 091019" src="https://github.com/user-attachments/assets/14416c91-aaa3-488c-b824-602097dcf184" />
<img width="1920" height="1080" alt="Screenshot 2026-11-24 091235" src="https://github.com/user-attachments/assets/ad6794ac-1930-47f1-a61f-2bac79b88293" />


## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
