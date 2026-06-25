# Docker- Multistage Build vs Without Multistage Build Dockerfile
---
## Project Steps

#### 1. Launch EC2 Instance

<img width="1150" height="191" alt="1 Ec2" src="https://github.com/user-attachments/assets/18299c91-487f-4040-aa6d-160c9529fd13" />

----
#### 2. SSH into that EC2 Instance
<img width="681" height="635" alt="2 ssh" src="https://github.com/user-attachments/assets/b705a752-3101-4aa5-a9a1-bdc97c76e72a" />

---
#### 3. Install Docker in this EC2 Instance
<img width="1353" height="491" alt="3  docker install" src="https://github.com/user-attachments/assets/ed7f03ac-c11c-4969-a2fa-120c483d7726" />

----
#### 4. Clone the github repository
<img width="772" height="326" alt="4  gitclone" src="https://github.com/user-attachments/assets/583ff078-d4d5-410f-a917-3af9c69cfb4e" />

----
#### 5. Build Dockerfile Image Without multistage
<img width="1239" height="296" alt="5  build womultistage" src="https://github.com/user-attachments/assets/1d3be819-5b4a-42db-ae02-79d725fa307f" />
<img width="434" height="111" alt="6" src="https://github.com/user-attachments/assets/b5c4e219-834a-4efd-b1d9-2c9266df559c" />

-----
#### 6. Build Multistage Dockerfile Image
<img width="969" height="499" alt="7  build multistage" src="https://github.com/user-attachments/assets/3580e026-51f7-4c3e-83ca-9a224e8a8fdc" />

----
#### 7. Verify Docker Images
<img width="823" height="106" alt="8  images" src="https://github.com/user-attachments/assets/492f724f-0758-4181-b66f-442ea015912b" />\

-----
### Comparision
- Here we could confirm that Mullti stage docker file image size(1.47 MB) is lesser than normal docker file image size (249 MB).
------
