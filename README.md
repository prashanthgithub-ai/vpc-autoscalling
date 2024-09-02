# vpc-autoscalling
Deploying an application in a VPC with private subnets on AWS involves several steps to ensure that your application is securely isolated from the internet while still being able to communicate with other resources. Below is a step-by-step guide
    ![Screenshot 2024-09-02 141102](https://github.com/user-attachments/assets/fbb67311-4fca-4061-a387-61f54506ac03)
 Deploying an application in a VPC with private subnets on AWS involves several steps to ensure that your application is securely isolated from the internet while still being able to communicate with other resources. Below is a step-by-step guide
STEP 1:
1Go to aws console and sign-in to aws account
2Choose the vpc through search bar
# Create VPC
Go to the VPC dashboard in the AWS Management Console. Click on “Create VPC”. Provide a name for your VPC, select the CIDR block, and enable DNS support. Create two public subnets and two private subnets, each in a different availability zone of the Mumbai region (1a and 1b). I have selected Mumbai region. You can select anything as you need. Make sure to associate a route table with each subnet and configure the public subnets to have access to the internet through an Internet Gateway 
![Screenshot 2024-09-02 145204](https://github.com/user-attachments/assets/db4df598-8d89-408f-a7ee-f658dcded50c)
You can see all the component connections in preview
As shown in below figure
![Screenshot 2024-09-02 122745](https://github.com/user-attachments/assets/f88b479d-bccb-435c-8520-416501051458)
Creation of an Auto Scaling Group:
automatic scaling of EC2 instancesThey ensure that the right number of Amazon EC2 instances are running to handle the load for your application. This capability allows your application to scale out (increase the number of instances) or scale in (decrease the number of instances) based on predefined conditions or metrics
![Screenshot 2024-09-02 145718](https://github.com/user-attachments/assets/aa5500ac-430b-468a-89c6-f0c74dfae05e)
# instance requried 
![Screenshot 2024-09-02 124822](https://github.com/user-attachments/assets/5ab847a5-7015-4f10-a4ea-ab183ae6adb4)
Creation of Load Balancer and Target Group:
Go to the EC2 dashboard and navigate to the “Load Balancers” section. Click on “Create Load Balancer” and choose the type (e.g., Application Load Balancer). Configure listeners and select the availability zones. Create a target group and add the primary and secondary web servers as targets. Configure health checks and routing settings as needed.
![Screenshot 2024-09-02 150535](https://github.com/user-attachments/assets/931b7d62-14f7-4f32-8aee-7aa9b40637b6)
# Go to instance
Check the instance their 2 private instances are created from auto scalling group
Give the name for 2 private instances as private 1 and private 2 to avoid confusions
Create one public instance named as bastion host as shown in figure
![Screenshot 2024-09-02 150835](https://github.com/user-attachments/assets/4f1734bd-51c9-4563-8f8e-e0ffa0e63014)
# conncet to terminal
![Screenshot 2024-09-02 134750](https://github.com/user-attachments/assets/d66fb7eb-79b8-4c6d-89ab-47e4819c3140)
after conncet private server public server 
we need to type the following commands
1)sudo su -
2)vi pp1.pemfile
3)chmod 400 pp1.pemfile
4)ssh -i "pp11.pem" ec2-user@10.0.138.223
5)systemctl start nginx
6)systemctl status nginx
7)cd/usr/share/nginx/html
8)cd/vi index.html
here we can change the html file
note :repart the above steps for server 2 aslo
affter complted all the above steps go to load balancer dns and copy the dns
![Screenshot 2024-09-02 151756](https://github.com/user-attachments/assets/a6f8a358-cc24-4abb-90a9-fecfedf01a4a)
# copy the  DNS and paste it in browser
