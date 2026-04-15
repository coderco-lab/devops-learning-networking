 Launching an NGINX Web Server on EC2

This guide shows how to set up an NGINX server on an EC2 instance and link it to your own domain using Cloudflare.

---

## Step 1: Get a domain

Buy a domain through Cloudflare  
Most domains cost between $5 and $10 per year

---

## Step 2: Create your EC2 instance

Go to AWS and open EC2

Launch a new instance with:

- AMI: Amazon Linux 2023  
- Instance type: t3.micro  

Set inbound rules:

- Port 22 (SSH) restricted to your IP  
- Port 80 (HTTP) open to all  
- Port 443 (HTTPS) open to all  

Launch the instance and wait until it is running

---

## Step 3: Copy your public IP

Open your instance details and find the Public IPv4 address  
You will use this to connect and link your domain

---

## Step 4: Connect using SSH

Run this in your terminal:

ssh -i /path/to/key.pem ec2-user@<EC2_PUBLIC_IP>

---

## Step 5: Install and start NGINX

Run:

sudo yum update -y  
sudo yum install -y nginx  
sudo systemctl start nginx  
sudo systemctl enable nginx  

Check it works by opening your public IP in a browser

---

## Step 6: Point your domain to EC2

Log in to Cloudflare and open DNS settings

Create a record:

- Type: A  
- Name: your domain or www  
- Value: your EC2 public IP  

Save the record

---

## Step 7: Check DNS

Run:

nslookup yourdomain.com

You should see your EC2 public IP

---

## Step 8: Update your web page

Edit the default page:

sudo nano /usr/share/nginx/html/index.html

Restart NGINX:

sudo systemctl restart nginx

---

## Step 9: Test your site

Open your domain in a browser  
You should now see your NGINX page live

---

You now have an NGINX web server running on EC2 mapped to your domain
