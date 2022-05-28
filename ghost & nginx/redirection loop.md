Add http2 after ssl in /etc/nginx/sites-enabled/example.com.conf server block:

```nginx
server {
    listen 443 ssl http2; # Add http2 here
    server_name example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    include snippets/ssl-params.conf;

    location / {
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_pass http://127.0.0.1:2825;
    }
}
```

If cloudflare is being used change the ssl setting from flexible to strict.

