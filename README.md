# nodejs-loadbalancer

Implementing load balancer using nginx

### Steps

1. Delete or move `defualt` file in `/etc/nginx/sites_enabled`

```bash
cd /etc/nginx/sites_enabled
sudo rm default
```

2. create a `.conf` file in `/etc/nginx/conf.d/`
   
   > load-balancer.conf
```text
  upstream nodejs {
        server localhost:5001;
        server localhost:5002;
        server localhost:5003;
    }

    server {
        listen 80;
        server_name localhost;
        location / {
            proxy_pass http://nodejs;
        }
        location /server1 {
            proxy_pass http://127.0.0.1:5001;
        }
        location /server2 {
            proxy_pass http://127.0.0.1:5002;
        }
        location /server3 {
            proxy_pass http://127.0.0.1:5003;
        }
    }

```

3. Restart nginx server
```bash
systemctl restart nginx.service
```
