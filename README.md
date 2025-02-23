# Reverse Proxy with Nginx and Apache2

This project demonstrates how to set up **Nginx as a reverse proxy** to forward client requests to an **Apache2 server** running on port **8585**.

## Project Structure
```
/reverse-proxy-project
│── nginx-config/              # Nginx configuration files
│── apache-config/             # Apache configuration files
│── screenshots/               # Screenshots of the setup
│── index.html                 # Sample website hosted on Apache
│── README.md                  # Project documentation
```

## Ports Configuration
- **Apache2:** Running on `localhost:8585` (default port changed from 80 to 8585)
- **Nginx:** Running on `localhost:80` and forwarding requests to Apache2

## Nginx Proxy Pass Configuration
Add the following configuration to your Nginx server block:

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://localhost:8585;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

## Steps to Run
1. **Change Apache’s port**: Modify the Apache configuration (`/etc/apache2/ports.conf` and `000-default.conf`) to listen on **8585**.
2. **Update Nginx Configuration**: Replace the default Nginx server block with the one above.
3. **Restart Services**:
   ```bash
   sudo systemctl restart apache2
   sudo systemctl restart nginx
   ```
4. **Access the Website**: Open a browser and visit `http://localhost/`.

## Screenshots
Find screenshots of the project setup inside the `screenshots/` directory.

## Learning Outcomes
- Configuring Nginx as a reverse proxy
- Running Apache2 and Nginx simultaneously on different ports
- Understanding `proxy_pass` and request forwarding
  
---
🚀 Happy Coding!
