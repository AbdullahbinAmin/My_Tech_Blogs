# Setting up AWS EC2 Instance

To set up the AWS EC2 Instance, clearly follow the following steps:
- Open your favourite Browser.
- Go to the website: [aws.amazon.com](https://aws.amazon.com/)
![image](https://github.com/user-attachments/assets/f2550f47-7671-4655-ba49-00eac067203e)
- Click on "Sign In to the Console." After clicking, you will see the following page:
![image](https://github.com/user-attachments/assets/300cba5b-1c66-4379-a0da-232a8b2483db)
- On this page, click on "Sign in using root user email" if you already have an account; if not, then click on "Create a new AWS account"
- On the next page type your "Root user email address" then click "Next".
- Type your Password then click "Next."
- If your account is secured using MFA, then finish signing in by typing your MFA code and then "Submit" it.
- Now you will see the page look like this:
![image](https://github.com/user-attachments/assets/daa0e489-b0f5-4b32-85bc-b2adf1a280f2)
- In the AWS search bar, search for "EC2", you will see the page below:
![image](https://github.com/user-attachments/assets/2ea9376f-7d5b-4778-b0fd-65b207743770)
- Click on "Launch Instance." You will see the page as given below:
![image](https://github.com/user-attachments/assets/608e075a-2e71-41c8-9a4d-c8f430c948f9)
- To create your first EC2 Instance, follow the complete instructions as follows:
  - Name and tags: Docker-Mastery
  - Application and OS Images (Amazon Machine Image): Ubuntu Server 24.04 LTS (HVM), SSD Volume Type
  - Instance type: t3.micro (Default)
  - Key pair (login): Click on "Create new key pair".
    - Key pair name: DevOps (You can type anything)
    - Key pair type: RSA
    - Private key file format: .pem
   ![image](https://github.com/user-attachments/assets/f63ad20c-9026-4790-b92b-b42163dc5ea3)
  - Now click on "Create key pair" and then save the .pem file where you want to save.
  - Network settings: Leave it Default. Click on the "Allow HTTPS traffic from the internet" and "Allow HTTP traffic from the internet" as in the below image:
 ![image](https://github.com/user-attachments/assets/3ad167e0-9148-4e55-8abc-1db509e3fb8c)
- When you go to the last, you will see the "Launch Instance" button; click to create your first EC2 instance. You will see the success message "Successfully initiated launch of instance."
![image](https://github.com/user-attachments/assets/29aab15c-6ffa-4022-942c-c50fc1c7b481)
- Now in the last of this message page, click on "View all instances."
- You successfully launched your first EC2 instance
![image](https://github.com/user-attachments/assets/af8ccd91-ec8d-429f-b405-2b8f23a1e635)

----

## How to Access My First EC2 Instance?
To access your first EC2 Instance, there are many ways to access your machine; we will follow the SSH client, which is one of the methods to access our machine, with the below-given instructions:
- First, tick the check box of your EC2 instance machine; you will see the "connect" button on the top right of your window. Click on it
![image](https://github.com/user-attachments/assets/a91a796f-1888-4166-b48e-f2e9bb9b0c3e)
- When you click on it, on the next page you will see the following page:
![image](https://github.com/user-attachments/assets/0e295be4-dfd6-4a1c-b11d-ac8e45509ce4)
- You will see the public IPv4 address and username on this page; copy this IPv4 address (it will be used in the future), and remember the username "ubuntu"
- Now, to access this machine locally on your computer, download the MobaXterm application on your local host machine.
- Download the MobaXterm Machine from this website:  Mobaxterm
- Once you download it and install it, open it, and you will see the interface of this application as below:
![image](https://github.com/user-attachments/assets/a880a17b-28d6-4a32-8d1c-f1af0ea4c206)
- Click on the "Session" icon in the top left corner. You will see the pop-up window:
![image](https://github.com/user-attachments/assets/d81208d4-a1c4-43fa-a9dd-0ee449e92a36)
- Now click on the SSH icon in the top left corner. In the "Remote Host" paste your IPv4 address that you copied earlier. Tick the check box of "Specify username" and type the username that you remember earlier or type "ubuntu"
- Click on Advanced SSH settings, tick the check box of "Use private key" and import the file of the key pair that you saved earlier and click "OK".
![image](https://github.com/user-attachments/assets/f7c67b55-5da6-43f0-9d27-4ff0fb9b096e)
- It will ask about the identity to accept this session, as you can see in the image below. Accept it.
![image](https://github.com/user-attachments/assets/9189a2f8-91da-47f9-9b6e-0593f1c8f35f)
- You will see that MobaXterm is successfully connected to our EC2 Instance machine.
![image](https://github.com/user-attachments/assets/c2979764-edd5-47de-8e9f-9e78db917ec3)
Now you are all set up the EC2 Instance Machine Successfully. Congratulations! 

---
For more Tech Blogs, You can follow me on:
- [Linkedin](https://www.linkedin.com/in/abdullahbinamin/)
- [Youtube](https://www.youtube.com/@AAA-Tech-1)
- [GitHub](https://github.com/AbdullahbinAmin)
