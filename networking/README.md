⚡ Launching an NGINX Web Server on Amazon EC2 ☁️
Today I set up an NGINX web server on an Amazon EC2 instance and connected it to my domain, jabz.uk, that I bought through Cloudflare. Here’s exactly what I did.

🟢 Step 1: Launch EC2 and SSH In
I launched an Amazon Linux 2 EC2 instance (t3.micro).


Security group rules:


🔑 Port 22 (SSH) – my IP


🌐 Port 80 (HTTP) – 0.0.0.0/0


To SSH in I used:

 ssh -i ~/.ssh/jabz.uk.pem ec2-user@3.8.204.202


At first it didn’t work because of the key permissions. I fixed it by moving the .pem file to WSL home folder and running chmod 400 ~/.ssh/jabz.uk.pem.
<img width="1913" height="860" alt="Screenshot 2025-11-26 182313" src="https://github.com/user-attachments/assets/509f0d1a-9434-4298-916d-9fb6a11734c2" />



🟡 Step 2: Install NGINX
Updated the system: sudo yum update -y


Installed NGINX: sudo yum install -y nginx


Started it: sudo systemctl start nginx


Made it start on boot: sudo systemctl enable nginx


Checked it was running with systemctl status nginx



🔵 Step 3: Make Sure HTTP is Open
Double-checked the security group: port 80 (HTTP) was open to 0.0.0.0/0.


Ran curl http://localhost on the EC2 instance to make sure NGINX was working.


Initially it didn’t work because I accidentally tried HTTPS (port 443), but switching to HTTP fixed it.



🟣 Step 4: Set Up Cloudflare DNS
Logged into Cloudflare and created an A record for jabz.uk pointing to 3.8.204.202.


Turned off the proxy (grey cloud) because I didn’t have SSL yet.


Also added a www record pointing to the same IP.
<img width="1411" height="105" alt="Screenshot 2025-11-26 182533" src="https://github.com/user-attachments/assets/fdc3755c-28ec-470c-a23d-a9c16dd21fad" />



🟠 Step 5: Check DNS
On my PC ran nslookup jabz.uk 1.1.1.1


At first I got a timeout, so I changed my PC’s DNS to 1.1.1.1 / 8.8.8.8 and flushed the cache (ipconfig /flushdns)


After that nslookup jabz.uk returned 3.8.204.202



🔴 Step 6: Test the Website
Opened http://3.8.204.202 in the browser → NGINX page showed up ✔️


Opened http://jabz.uk → also worked ✔️


And thats how i completed my first assignment on CoderCo, it was hard but I was able to complete it and its very reliving to see your website working at the end.
<img width="1920" height="1080" alt="Screenshot 2025-11-26 182057" src="https://github.com/user-attachments/assets/e70ca834-1bc2-4daf-944c-20f5d3593bd9" />


