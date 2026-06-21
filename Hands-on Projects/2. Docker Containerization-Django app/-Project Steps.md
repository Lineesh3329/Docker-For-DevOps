## Project Steps

#### 1. Launch EC2 Instance
- with security group- port: 8080

#### 2. SSH into that EC2 Instance
<img width="698" height="29" alt="ssh into ec2" src="https://github.com/user-attachments/assets/c962f7e7-f65a-4b14-9e34-b6503f927227" />

-----
#### 3. Install Docker in this EC2 Instance
#### 4. Clone the github repository
<img width="803" height="220" alt="gitclone" src="https://github.com/user-attachments/assets/4473e903-9d49-4a52-98dc-36624163dddf" />

----
#### 5. Build Docker Image
<img width="797" height="421" alt="built" src="https://github.com/user-attachments/assets/76f01a94-df6b-42c4-b0d5-f719faccb166" />
<img width="713" height="195" alt="2 built" src="https://github.com/user-attachments/assets/1fbf1070-7a56-472f-b49a-d552c42fd78a" />

----
#### 6. Veriy Docker Images
- using `docker images`
-----
#### 7. Run Docker Image
- using `docker run -p 8000:8000 -it django`
<img width="1208" height="279" alt="run it" src="https://github.com/user-attachments/assets/ffdf6828-d625-4d44-8f77-74d7f7b397a8" />

---
#### 8. Open this browser
- using http://ipaddress:8000/demo/

<img width="1201" height="656" alt="output" src="https://github.com/user-attachments/assets/da44375c-3dad-4504-a896-0e816d606e8d" />

----
- The Docker Image is build through Docker File and Container is created by running Docker Image
- This verified by opening in the browser.
- This container can be pushed to Docker Hub which is publicly viewable. This executed below.
------

### Pushing Docker Container to Docer Hub
#### 9. Login to DockerHub via terminal
<img width="806" height="244" alt="dockerhub" src="https://github.com/user-attachments/assets/8896719f-c857-4b07-ab10-50becc90295b" />

----
#### 10. Tag the Image & Push it to Docker Hub
<img width="938" height="43" alt="push to dochub" src="https://github.com/user-attachments/assets/8bb36a86-632d-4f98-abf9-d135662646b9" />

----
#### 11. Verified in Docker Hub
<img width="1352" height="575" alt="dochunb" src="https://github.com/user-attachments/assets/a5dba33f-4377-4edf-94b8-6dda6ff7b40e" />

----
