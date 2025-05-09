# 🚀 Automated Web App Deployment with Git Pull and Nginx on Ubuntu EC2

This project demonstrates how to automatically deploy a simple web application from a GitHub repository to an AWS EC2 instance running Ubuntu, and serve it using the Nginx web server. It uses `git pull` for deployment and configures Nginx as a reverse proxy.

---

## 🛠 Tools & Technologies

- 🐧 Ubuntu (Linux)
- ☁️ AWS EC2 Instance
- 🔐 SSH (Secure Shell)
- 🌐 Nginx Web Server
- 🧠 Git & GitHub
- 🖥️ Terminal (Bash)

---

## 🚀 Project Overview

This project includes:

- Setting up an Ubuntu EC2 instance
- Installing Git and Nginx
- Cloning a GitHub repository into `/var/www`
- Configuring Nginx to serve the app from the cloned repository
- Using `git pull` to fetch and deploy updates automatically
- Using `git push` to put the files into the repository
- Ensuring public access to the website via EC2 public IP

---

## 📋 Step-by-Step Guide

### ✅ 1. Launch EC2 and SSH In

- Create a new EC2 instance using Ubuntu (preferably Ubuntu 22.04).
- Open Inbound rules for ports **22 (SSH)** and **80 (HTTP)**.
- Connect using:
```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

### ✅ 2. Update System and Install Required Packages
```
sudo apt update && sudo apt upgrade -y
sudo apt install git nginx -y
```

### ✅ 3. Clone Your GitHub Repository
```
cd /var/www
sudo git clone https://github.com/orvencasido/Automated-Web-App-Deployment-with-Git-Pull-and-Nginx-on-Ubuntu-EC2.git
```

### ✅ 4. Configure Nginx to Serve Your Web App
```
sudo nano /etc/nginx/sites-available/webapp
```

```
server {
    listen 80;
    server_name Orven_Server;

    root /var/www/Automated-Web-App-Deployment-with-Git-Pull-and-Nginx-on-Ubuntu-EC2;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
``` 

#### Enable It:
```
sudo ln -s /etc/nginx/sites-available/webapp /etc/nginx/sites-enabled/
sudo unlink /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl restart nginx
```

### ✅ 5. Test Deployment
- Add an `index.html` inside the cloned repo.
- Visit `http://<your-ec2-public-ip>` and you should see your page.

### ✅ 6. Pull Updates Automatically
```
cd /var/www/Automated-Web-App-Deployment-with-Git-Pull-and-Nginx-on-Ubuntu-EC2
sudo git pull
```

## 📸 Example Output
```
$ curl http://<your-ip>
<!DOCTYPE html>
<html>
  <head><title>Nginx As Web Server In EC2</title></head>
  <body><h1>Sample Web Server! Using EC2 and Nginx!</h1>
    <h6>Orven Casido Devops Enthusiast</h6>
  </body>
</html>

```

## 📎 Commands Reference
- `sudo systemctl restart nginx`	Restart Nginx to apply config changes
- `git pull`	Fetch and merge latest changes
- `sudo nginx -t`	Test Nginx config for syntax
- `sudo ln -s`	Create symbolic link for site config

## 💡 Real-World Use Cases
- Lightweight continuous deployment setup
- Hosting a static website or frontend from GitHub
- Practicing reverse proxy configurations

## 📚 Learning Outcomes
- GitHub-based deployment using EC2
- Nginx reverse proxy setup
- Basic Linux file structure for web hosting
- Practical Git usage in production

## 🧑‍💻 Author
Orven Casido – techwithorven.xyz

