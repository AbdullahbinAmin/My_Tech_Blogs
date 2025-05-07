  # Building a Basic Docker Image & Pushing it to AWS Elastic Container Registry (ECR)

In this lab, we will:
1.	Install Docker and AWS CLI.
2.	Create an IAM user on AWS and configure AWS CLI with it.
3.	Make a simple website with HTML and CSS.
4.	Create a Dockerfile.
5.	Build and tag a Docker image.
6.	Push it to Amazon Elastic Container Registry (ECR).
Let’s go step by step.

---
## Step 1: Install Docker
Docker helps us package our application and all its files into something called a container. This container can run anywhere.
To install Docker, follow this official guide for Ubuntu:
[Docker Official Website](https://docs.docker.com/engine/install/ubuntu/).

Once installed, check Docker is working:
```
docker --version
```
![image](https://github.com/user-attachments/assets/4a5288f0-fd5f-4576-be22-74b579c8370b)

 
This will show something like:
```
Docker version 24.x.x, build xxxxx
```

## Step 2: Install AWS CLI
AWS CLI lets us talk to Amazon Web Services (AWS) from our terminal.

Install AWS CLI using this command:
```
sudo apt install awscli
```

-	`sudo`: Run the command as an administrator.
-	`apt`: The package manager in Ubuntu.
-	`install`: Tells apt to install something.
-	`awscli`: The name of the software we are installing (AWS Command Line Interface).

![image](https://github.com/user-attachments/assets/540df16e-01f3-4412-81fd-fc34a1cb1efe)


Check installation:
```
aws --version
```
![image](https://github.com/user-attachments/assets/f93f4927-1499-46cd-badf-bfba19255bc3)


## Step 3: Create IAM User on AWS
We need special keys to connect to AWS safely. These are created using IAM (Identity and Access Management).
Steps:
1.	Log in to your AWS Console.

![image](https://github.com/user-attachments/assets/4bb526a2-d2f4-4bf2-a0d2-4d8f00a4ea7f)


2.	Search for IAM in the top search bar.

![image](https://github.com/user-attachments/assets/cda558da-35d6-454c-86d5-972b0b78d34b)

3.	Click Users → then click Add user.

![image](https://github.com/user-attachments/assets/3b3c16ce-75e4-45a9-a9e6-d0639daa5fff)

4.	Name your user (e.g., ecr-user).
5.	Select Access key - Programmatic access.
6.	Click Next → Attach permissions.
7.	Choose Attach policies directly.
8.	Search and select: `AmazonEC2ContainerRegistryFullAccess`


![image](https://github.com/user-attachments/assets/a6c7eb5f-e77b-48ed-820a-66fcbf699183)


This gives full access to push and pull Docker images from ECR.

9.	Click Next → then Create user.

![image](https://github.com/user-attachments/assets/266820e4-7f36-4783-8d8b-2c158b8272fd)

Note:

You will now see two keys:

- Access Key ID
- Secret Access Key

Save them! You will need them for configuration.


## Step 4: Create Your HTML & CSS Files
Let’s make a simple static website.

Example:


index.html
```html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Abdullah's NGINX Site</title>
    <link rel="stylesheet" href="style.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
</head>
<body>
    <header>
        <div class="container">
            <h1>Abdullah's DevOps Hub</h1>
            <nav>
                <a href="#">Home</a>
                <a href="about.html">About</a>
                <a href="#">Projects</a>
                <a href="#">Contact</a>
            </nav>
        </div>
    </header>

    <section class="hero">
        <div class="container">
            <h2>🚀 High Performance Web Server Powered by NGINX</h2>
            <p>Welcome to my fully self-deployed, secure, and beautiful static website — manually configured, no shortcuts.</p>
            <a href="about.html" class="btn">Learn More</a>
        </div>
    </section>

    <section class="services">
        <div class="container">
            <h2>What I Do</h2>
            <div class="cards">
                <div class="card">
                    <i class="fas fa-cloud"></i>
                    <h3>Cloud Engineering</h3>
                    <p>Deploying secure, scalable infrastructure on AWS, Azure, and beyond.</p>
                </div>
                <div class="card">
                    <i class="fas fa-code"></i>
                    <h3>Automation</h3>
                    <p>CI/CD pipelines, bash scripting, and Jenkins automation.</p>
                </div>
                <div class="card">
                    <i class="fas fa-lock"></i>
                    <h3>Security</h3>
                    <p>Implementing CIS Benchmarks, firewalls, and SSL best practices.</p>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <p>&copy; 2025 Abdullah bin Amin. All rights reserved.</p>
    </footer>
</body>
</html>
```

style.css
```css
/* Google Font and basic reset */
body {
    font-family: 'Poppins', sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f6f8;
    color: #333;
}

/* Header */
header {
    background-color: #1e2a38;
    padding: 20px 0;
    color: white;
}

header h1 {
    margin: 0;
    font-size: 24px;
}

header .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 10%;
}

nav a {
    color: #ccc;
    text-decoration: none;
    margin: 0 15px;
    font-weight: 500;
}

nav a:hover {
    color: #fff;
}

/* Hero Section */
.hero {
    padding: 100px 10%;
    background: linear-gradient(135deg, #1e2a38, #283c4a);
    color: white;
    text-align: center;
}

.hero h2 {
    font-size: 36px;
    margin-bottom: 20px;
}

.hero p {
    font-size: 18px;
    max-width: 600px;
    margin: 0 auto 30px;
}      

.btn {
    display: inline-block;
    background-color: #ff6a00;
    color: white;
    padding: 12px 24px;
    border-radius: 5px;
    text-decoration: none;
    font-weight: bold;
    transition: background 0.3s;
}

.btn:hover {
    background-color: #e65c00;
}

/* Services Section */
.services {
    padding: 60px 10%;
    background-color: #ffffff;
    text-align: center;
}

.services h2 {
    font-size: 32px;
    margin-bottom: 40px;
}

.cards {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
}

.card {
    background-color: #f9fafc;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
    max-width: 300px;
    transition: transform 0.3s;
}

.card:hover {
    transform: translateY(-5px);
}

.card i {
    font-size: 36px;
    margin-bottom: 15px;
    color: #007bff;
}

.card h3 {
    font-size: 22px;
    margin-bottom: 10px;
}

/* Footer */
footer {
    background-color: #1e2a38;
    color: white;
    text-align: center;
    padding: 20px;
}
```

Save both files in a folder, e.g., `/home/abdullah/Docker/`.

![image](https://github.com/user-attachments/assets/04206e57-4d02-48fe-b2a5-30c9a810ae7d)


## Step 5: Configure AWS CLI
Now, we will connect your terminal to AWS using the keys you saved earlier.

Run:
```
aws configure
```
![image](https://github.com/user-attachments/assets/9c2655ba-4f86-48ee-846d-177ad5c33d83)

It will ask:
- AWS Access Key ID: Paste it here.
- AWS Secret Access Key: Paste it here.
- Default region name: Type something like us-east-1
- Default output format: Type json

Now your terminal is connected to AWS!

![image](https://github.com/user-attachments/assets/656cd15a-f763-4f89-b4b5-5fea9eb822a8)


## Step 6: Create AWS ECR Repository
1.	Go to the AWS Console.
2.	Search for ECR.

![image](https://github.com/user-attachments/assets/dd1c45d3-996a-478c-8f9d-eff9419dfd83)

3.	Click Create repository.
4.	Give your repo a name (e.g., my-docker-site).
5.	Leave everything else as default.
6.	Click Create repository.

![image](https://github.com/user-attachments/assets/1c829bcb-f082-4183-bb22-a9e34fdaacf9)

 
Now click on your new repository, then click View push commands.

You’ll see 4 commands. Let’s use them one by one.

![image](https://github.com/user-attachments/assets/225ab14a-6e0a-4f48-ae71-6a3c7264affd)


## Step 7: Create the Dockerfile
Inside the same folder where your index.html and style.css are, create a file named Dockerfile (no extension).

Paste this:
```Dockerfile
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Explanation:
- `FROM nginx:latest`

  → Start from the latest version of the NGINX web server.
- `COPY . /usr/share/nginx/html`

  → Copy everything (.) in the current folder into the container’s web directory.
- `EXPOSE 80`

  → Tell Docker to open port 80, which is the default web server port.
- CMD ["nginx", "-g", "daemon off;"]

  → Run the NGINX server in the foreground (do not send it to the background).

![image](https://github.com/user-attachments/assets/4d26cf04-dedf-44cd-b616-d34896a3b754)


## Step 8: Push to AWS ECR
Now, go back to the "View Push Commands" on your ECR page.

You’ll see 4 commands. Let’s understand and run them one by one:


### Command 1: Login to AWS ECR
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.us-east-1.amazonaws.com
```

Breakdown:
-	`aws ecr get-login-password`: Get a temporary password.
-	`--region us-east-1`: Replace with your region.
-	`|`: Pipe means “send the output to the next command”.
-	`docker login`: Log in to Docker with the credentials.
-	`--username AWS`: Username for AWS.
-	`--password-stdin`: Take password from the pipe.
-	`your-account-id.dkr.ecr.us-east-1.amazonaws.com`: Replace with your ECR URL.
 
![image](https://github.com/user-attachments/assets/7e5ec922-1490-49f3-9318-9fd58ecf0661)


### Command 2: Build the Docker image
```
docker build -t my-docker-site .
```

Breakdown:
-	`docker build`: Build a Docker image.
-	`-t my-docker-site`: Give your image a name/tag.
-	`.`: Use the current folder (where Dockerfile is).
 

![image](https://github.com/user-attachments/assets/d513eb4a-6f9a-4674-9a74-5011ce7688bf)


### Command 3: Tag the Docker image
```
docker tag my-docker-site:latest <your-account-id>.dkr.ecr.us-east-1.amazonaws.com/my-docker-site
```

Breakdown:
-	`docker tag`: Give the image a new name (for pushing).
-	`my-docker-site:latest`: The local image you just built.
-	`.../my-docker-site`: The full path to your AWS ECR repo.
 
![image](https://github.com/user-attachments/assets/839e285e-f174-4ef1-89ff-84274a5fb922)


### Command 4: Push the Docker image
```
docker push <your-account-id>.dkr.ecr.us-east-1.amazonaws.com/my-docker-site
```

Breakdown:
-	`docker push`: Upload your image.
-	The long URL is your ECR repository.
 
![image](https://github.com/user-attachments/assets/7cde1060-ef26-4baa-bf64-3ed1854d5dc1)


That’s it! Your website is now stored in AWS ECR as a Docker image.

![image](https://github.com/user-attachments/assets/17f8d027-1a0f-44c6-9b52-e6469e2af3bf)

You can now pull this image from any machine and run it with:
```
docker run -p 80:80 <your-ecr-url>
```
![image](https://github.com/user-attachments/assets/6e8240f2-fdf1-4491-9601-9b9e5013e045)


## Final Thoughts
-	We installed and configured Docker and AWS.
-	We made a basic website.
-	We learned to write a Dockerfile.
-	We pushed the image to AWS ECR step by step.



