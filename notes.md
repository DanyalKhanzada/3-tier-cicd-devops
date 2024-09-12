## 1. Local Deployment Setup

1. sudo-apt-get update
2. Nodejs Download - https://nodejs.org/en/download/package-manager

## 2. Setup Environment Variables

1. Cloudinary
2. Mapbox 
3. MongoDB (Collection) - Cloud database > Container

cloudinary.config({ 
        cloud_name: 'diax8boyn', 
        api_key: '876432814896329', 
        api_secret: 'sewZXU-P9wY0UCeL9ANeHBZygLw' 
    });

CLOUDINARY_CLOUD_NAME=diax8boyn
CLOUDINARY_KEY=876432814896329
CLOUDINARY_SECRET=sewZXU-P9wY0UCeL9ANeHBZygLw
MAPBOX_TOKEN=sk.eyJ1IjoiZGFueWFsa2hhbnphZGEiLCJhIjoiY20wMXNjbW9rMWRyejJybzRydDl0b3A1biJ9.RC6Yj3BzO0IH32D1Zc_E2g
DB_URL:"mongodb+srv://danyalkhanzada:FU53JtEDJ8xEoGpg@danyal-devops.1dnpo.mongodb.net/?retryWrites=true&w=majority&appName=danyal-devops"
SECRET:devopsdanyal

## 3. Create Database

1. MongoDB (Collection) - Cloud database > Container
    - Created cluster on MongoDb
    - Create username and password
    - Went to network access under security and changed created IP address to 0.0.0.0/0 so i can access it from anywhere. 
    
    - it is connected to the database after putting in the .env file with Cloundinary text above


2. App deployment on DEV Environment
    - two Ec2 instances are created. 1. for Jenkins with T2.large 2. SonarQube with T2.Medium
    - download Java in the instance - sudo apt install openjdk-17-jre-headless -y
    - installing jenkins on the jenkins ec2 instance and created script directory where excuetable code is pasted from jenkins install website for ubuntu
    - ./jen.sh executed the transaction
    - installing docker on the ec2 
    - opened browser and put Publicip:3030 and copies the jenkins user /var/lib/jenkins/secrets/initialAdminPassword
    - Ran command sudo cat /var/lib/jenkins/secrets/initialAdminPassword to get the password and pasted it on browser to get into jenkins
    - changed the permission on terminal to " sudo chmod 666 /var/run/docker.sock "

    - SonarQube - Ec2 instance 
    - Downloaded Docker to create an image
    - docker run -d --name sonar -p 9000:9000 sonarqube:lts-community 
     it will run on port 9000

     - login passowrd sonarqube - admin pwd danyal007
    - Jenkins - danyal pwd danyal007

    - Downloaded in jenkins following plugins
            - Kubernetes , kubernetes cli, docker, docker pipelines, sonarqube, 

    - trivy plugin is not available. downloading trivy directly
    sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy

- created as script and pasted the above command and ran the script ./tri.sh (where the script is savd)

- configure tools on jenkins server by going to manage jenkins -> tools and thn configured all of them 

next step: configure sonarqube server inside jenkins
from user admin on sonarqube - create a token -> copy token
copy the token and go to jenkins and manage jenkins -> credential -> add new credentials -> select secret text and paste it. 

next step : start creating pipeline

ill have to resrart again
