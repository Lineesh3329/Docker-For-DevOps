# Demo on Docker Volume

## Project Steps
#### 1. Launch EC2 Instance
#### 2. SSH into that EC2 Instance
#### 3. Install Docker in this EC2 Instance
#### 4. Clone the github repository
#### 5. Volume Creation**

  - Command: `docker volume create (volume name)`
<img width="657" height="58" alt="1 createVol" src="https://github.com/user-attachments/assets/6c729ebb-67e2-4be5-b293-800ff0bf3162" />

------
  - Command: `docker volume ls`
<img width="563" height="58" alt="2  ls Volume" src="https://github.com/user-attachments/assets/9e9b6ec5-536e-4b38-95e6-7ee84b253568" />

-----
#### 6. Inspect Volume to view details of volume

   - Command: `docker volume inspect (volume name)`
<img width="629" height="199" alt="3  inpect Volume" src="https://github.com/user-attachments/assets/d8e8b593-c98c-482c-9e10-0078a6b1a9cb" />

----

#### 7. Build image from Dockerfile
<img width="859" height="44" alt="4  rundocker" src="https://github.com/user-attachments/assets/c485c35f-da60-44c7-a9ea-52c715da82fc" />

-----
#### 8. Mount Docker volume to the specifuc container in the detached mode
#### 9. List Container to verify- `docker ps-a`
#### 10. Inspect Container `docker container <contaainer id>`
- command: `docker run -d --mount source=(volume name), target=/app (image name)`
<img width="1120" height="440" alt="5  run,ps,inspect" src="https://github.com/user-attachments/assets/c052eaae-e642-4d12-9b5e-0de23b4199b2" />

------
#### 11. Verify Volume mounted in the container
<img width="663" height="181" alt="6  Mounts confirm" src="https://github.com/user-attachments/assets/24e1ed71-0470-4477-a946-db4f4043f430" />

-----
#### 12. Here we confirm that the volume cannot be deleted unless container deletion.
<img width="1042" height="39" alt="7  rm volume" src="https://github.com/user-attachments/assets/ad7591a0-a61d-40c8-bae0-e7d14a0bb72a" />

---
#### 13. Here we verified that after deletinng container the attached volume able to delete. 
<img width="903" height="120" alt="8 1 final" src="https://github.com/user-attachments/assets/d21a5693-157e-41e7-9f5c-c6af990ee07a" />
<img width="614" height="73" alt="8 2 final" src="https://github.com/user-attachments/assets/eb7a6239-f04a-4cd9-8605-c6c54975cdb5" />

-----
----

