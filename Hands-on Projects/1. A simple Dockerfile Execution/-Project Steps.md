## A simple Dockerfile Execution
In this demo, we could see how from dockerfile the image is build, container is pushed to public registry.

## Project Steps Followed:

#### 1. Create an EC2 instance.
#### 2. SSH into that EC2 Instance
#### 3. Docker Installation

  - Update Packages : `sudo apt update`

  - Install Docker : `sudo apt install docker.io -y`

  - Check Docker version : `docker --version`

  - Start Docker Service : `sudo systemctl start docker`

  - Enable Docker at boot : `sudo systemctl enable docker`

  - Check Docker status : `sudo systemctl status docker`

  - Give Docker Permission to Current User : `sudo usermod -aG docker ubuntu`

#### 3. Create a Dockerfile for app.py

<img width="262" height="62" alt="1 ls" src="https://github.com/user-attachments/assets/172ee719-f0d4-4201-bf53-b2ee9b0437fa" />

---
#### 4. Buid Docker Image using,
- `docker build -t myfirstdockerimage .(dockerimage)`
<img width="465" height="192" alt="2 dockerbuilt" src="https://github.com/user-attachments/assets/57b4cd1c-8f17-4307-b6a1-29cb9aba83f4" />

---
#### 5. Verify Docker Images
- `docker images`
<img width="737" height="125" alt="3 dockerimages" src="https://github.com/user-attachments/assets/a701faa5-1083-4cbf-aa84-33801502c183" />

----
#### 5. Run Docker Image
- `docker run it myfirstdockerimage:latest`
<img width="568" height="43" alt="4 runit" src="https://github.com/user-attachments/assets/c97e28cd-b0e2-4023-b5c6-783d318589df" />

---
### Pushing Docker Images to Docker Hub

#### 1. Login to Docker Hub

<img width="729" height="244" alt="6 dockerhublogin success" src="https://github.com/user-attachments/assets/2127e9fb-ecb1-468c-a18e-a8a38ebf37cb" />

---
#### 2. Tag the Docker image uaing below command,

<img width="823" height="26" alt="7 dockertag" src="https://github.com/user-attachments/assets/0b00106a-27fb-493f-a9c6-bfb5ade7638d" />

----
#### 3. Push the Docker image to DockerHub
<img width="803" height="139" alt="5 dockerpush" src="https://github.com/user-attachments/assets/bc067960-25cc-4e37-8ecc-4a1143a7af80" />

--
#### 4. Confirmed Docker image pushed to Docker Hub
<img width="1354" height="332" alt="8 dockerhubverify" src="https://github.com/user-attachments/assets/899dff0d-8fc7-4d19-8972-9fae5235a180" />

----
