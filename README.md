# nginx lab 

Getting the image:

```
docker pull nginx
```

Run the bare image:

```
docker run -d -p 80:80 nginx
curl localhost
```

You should get the **Welcome to nginx** web page.

Configuration directives's hierachy:
- `main` context contains `events` and `http`
- `http` contains `server`
- `server` contains `location`


Loading a minimal configuration (see `./nginx.conf` for details):
```
docker run -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
```

Then you should be able to get:
- http://localhost
- http://localhost/images/example.png

Proxy server (see `nginx-proxy.conf`):

```
docker run -v $(pwd)/nginx-proxy.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
curl localhost
```

Match request path with regex (see `nginx-regex.conf`):

```
docker run -v $(pwd)/nginx-regex.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
```

- http://localhost/example.png

