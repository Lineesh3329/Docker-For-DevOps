# Project on Docker Network

## Execution Steps
#### 1. Launch EC2 Instance
#### 2. SSH into that EC2 Instance
#### 3. Install Docker in this EC2 Instance
#### 4. Clone the github repository
#### 5. Build image from Dockerfile
#### 6. Create `Customer Container` and `Savings Conatiner`
<img width="992" height="154" alt="1  create container" src="https://github.com/user-attachments/assets/f70d4941-dbcc-4779-88dd-fd444bb72410" />

----
#### 7. Checking Ips of Customer & Savings container
- `docker inspect <container id or name>`
- Though these containers are in same subnet- Bridge Network(default) so the Ips of these containers are same. 
<img width="833" height="335" alt="2  IP Customer" src="https://github.com/user-attachments/assets/6441a688-99e8-44b5-a38f-ee06447b62d2" />
<img width="922" height="375" alt="2  IP Savings" src="https://github.com/user-attachments/assets/f275e0d5-d02e-4f47-9c44-22839005af63" />

-----
#### 8. Login to `Savings` container and ping `Customer` container.
<img width="754" height="461" alt="3  container --container" src="https://github.com/user-attachments/assets/3b67969b-16b1-4074-be4e-87eafc0720b1" />

- Ping customer cotainer

<img width="601" height="253" alt="4  ping customer from ssavings" src="https://github.com/user-attachments/assets/99c68a51-0bcd-4d2e-967f-ebf690e7ea76" />

----
#### 9. Create `Locker Container` and connecting to `Custom Bridge Network`
- create Locker contaier
<img width="1046" height="157" alt="5  locker" src="https://github.com/user-attachments/assets/eb99eacb-8395-43f1-beec-dbee56881bee" />

- Creating Custom Bridge Network
- Connecting Locker Container to Custom Bridge Network
<img width="633" height="155" alt="6  Custombridge" src="https://github.com/user-attachments/assets/5f5fbf08-a46b-4211-94d8-9421e04ebf9f" />

----
#### 10. Check Ip of `Container Locker`
- docker inspect `Locker`
<img width="766" height="346" alt="7  IP Locker" src="https://github.com/user-attachments/assets/cf12cd9e-4421-4ff8-9d5f-102b565310ee" />

#### 11. Ping `Locker` container from `Savings` container
<img width="459" height="60" alt="8 1 ping locker from savings" src="https://github.com/user-attachments/assets/9cbf80a3-3efe-42e4-9324-5a0d130d230b" />

------
