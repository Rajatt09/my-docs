## Setting up node js in ubuntu

(i) **Open your terminal and run the below command.**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

This command downloads and runs the NVM (Node Version Manager) installation script for version 0.39.3. NVM allows you to easily install and manage multiple versions of Node.js on your system.

(ii) **To use it, you must first source your .bashrc file:**
Restart your terminal or run `source ~/.bashrc` (or `~/.zshrc` if using Zsh).

```bash
source ~/.bashrc  # for bash (ubuntu)
```

(iii) Verify installation with:

```bash
nvm --version
```

- Now install node on your machine

```bash
nvm install v14.10.0 # for specific version of node
nvm install --lts    # for installing latest version of node
```

---

## Setting up nginx

Nginx is a open source software for web serving, reverse proxying, caching, load balancing, media streaming and more. It started out as a web server designed for maximum performance and stability.In addition to its http server capablities, Nginx can also function as a proxy server for email (IMAP, POP3 and SMTP) and reverse proxy and load balancer for HTTP, TCP and UDP servers.

- By default node etc not given heavy access like running on port 80 for http and 443 for https hence while requesting one need to use http://machine_ip:3000 if its node server running on 3000 he can't directly run it on 8080 so to avoid this port in url. for that it needs something as intermediate which can direct incoming request to their correct server if there are many insatnces running like on 3000, 4000 etc.

- Hence one can use nginx serving as reverse proxy here which default run on 80 (http).

### Installing Nginx

```bash
sudo apt update
sudo apt install nginx
```

```bash
sudo nginx -s reload # for re-running nginx
```

This will start a nginx server on port 80.

- For further configurations one need to change the config file of nginx (like creating reverse proxy).

```bash
sudo vi /etc/nginx/nginx.conf   # opens configuration file of nginx
```

- Creating reverse proxy

```bash
#paste below code in nginx.config

events {
 # Event directives...
}

http {
server {
    listen 80;
    server_name your_domain_or_public_ip;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    }
}

# for more servers add other server in http {server{} server{}}
```
