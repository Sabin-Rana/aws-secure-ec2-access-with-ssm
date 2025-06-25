# **Secure EC2 Access Using AWS Systems Manager (SSM)**

## **Project Overview**
This project demonstrates how to securely access EC2 instances using AWS Systems Manager Session Manager, eliminating the need for exposed SSH ports and key pairs while providing IAM-based access control and encrypted sessions.

## **Implementation Steps with Detailed Screenshots**

### **Step 1: IAM Role Creation for SSM Access**

1. **IAM Dashboard Access**  
   Navigated to IAM service to begin role creation process  
   ![IAM Dashboard showing role creation option](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture1.PNG)

2. **Role Creation Initiation**  
   Selected "AWS service" as trusted entity and "EC2" as use case to create role specifically for EC2 instances  
   ![Role creation interface with EC2 service selected](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture2.PNG)

3. **Policy Attachment**  
   Attached the mandatory `AmazonSSMManagedInstanceCore` policy to enable SSM functionality  
   ![Policy selection screen with AmazonSSMManagedInstanceCore highlighted](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture3.PNG)

4. **Role Naming**  
   Named the role `EC2-SSM-Access-Role` for clear identification  
   ![Role naming screen with completed fields](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture4.PNG)

5. **Role Creation Confirmation**  
   Success notification showing the IAM role was successfully created  
   ![AWS confirmation message for role creation](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture5.PNG)

### **Step 2: Attaching IAM Role to EC2 Instance**

1. **Instance Role Modification**  
   Accessed the role modification option from EC2 instance actions menu  
   ![EC2 instance actions dropdown showing modify IAM role option](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture6.PNG)

2. **Role Selection**  
   Selected the newly created `EC2-SSM-Access-Role` from available roles  
   ![IAM role selection dropdown with target role highlighted](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture7.PNG)

3. **Attachment Confirmation**  
   AWS notification confirming successful role attachment  
   ![Success notification for IAM role attachment](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture8.PNG)

4. **Instance Verification**  
   Confirmed role appears in instance description tab  
   ![EC2 instance details showing attached IAM role](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture9.PNG)

### **Step 3: SSM Agent Verification**

1. **Initial SSH Connection**  
   Established temporary SSH connection to verify agent status (for setup purposes only)  
   ![Terminal showing successful SSH connection](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture10.PNG)

2. **Agent Status Check**  
   Verified SSM Agent was running using systemctl command  
   ![Terminal output showing active SSM Agent status](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture11.PNG)

### **Step 4: Session Manager Connection**

1. **Connect Interface Access**  
   Accessed EC2 connect interface from instance dashboard  
   ![EC2 instance console showing connect button](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture12.PNG)

2. **Session Manager Selection**  
   Chose Session Manager tab for secure connection  
   ![Connect options with Session Manager tab selected](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture13.PNG)

3. **Active Session Demonstration**  
   Established session showing command execution (whoami and ifconfig)  
   ![Browser-based terminal session with command outputs](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture14.PNG)

4. **Session Termination**  
   Properly terminated session using end button  
   ![Session interface showing terminate button](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture15.PNG)  
   ![Termination confirmation dialog](https://github.com/Sabin-Rana/aws-secure-ec2-access-with-ssm/blob/main/Screenshots/Capture16.PNG)

## **Security Architecture**
```mermaid
graph TD
    A[IAM User] -->|Assume Role| B[EC2-SSM-Access-Role]
    B --> C[Session Manager]
    C --> D[EC2 Instance]
    D --> E[CloudWatch Logging]
    style A fill:#f9f,stroke:#333
    style B fill:#bbf,stroke:#333
    style C fill:#9f9,stroke:#333