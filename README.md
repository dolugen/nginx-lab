# nginx lab 

- [Getting the image](#getting-the-image)
- [Run the bare image](#run-the-bare-image)
- [Configuration](#configuration)
- [Proxy server](#proxy-server)
- [Match request path with regex](#match-request-path-with-regex)
- [Load balancing](#load-balancing)

## Getting the image

```
docker pull nginx
```

## Run the bare image

```
docker run --rm -d -p 80:80 nginx
curl localhost
```

You should get the **Welcome to nginx** web page.

## Configuration

Configuration directives's hierachy:
- `main` context contains `events` and `http`
- `http` contains `server`
- `server` contains `location`

Loading a minimal configuration (see `./nginx.conf` for details):
```
docker run --rm -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
```

Then you should be able to get:
- http://localhost
- http://localhost/images/example.png

## Proxy server

See `nginx-proxy.conf`.

```
docker run --rm -v $(pwd)/nginx-proxy.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
curl localhost
```

## Match request path with regex

See `nginx-regex.conf`.

```
docker run --rm -v $(pwd)/nginx-regex.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p80:80 nginx
```

- http://localhost/example.png

## Load balancing

See `nginx-lb.conf`.

```
docker run --rm -d -v $(pwd)/nginx-lb.conf:/etc/nginx/nginx.conf:ro -v $(pwd)/data:/data:ro -p 80:80 nginx
```

Now if you keep reading from http://localhost, it will respond with these responses in round-robin order:

- hello from site 1
- hello from site 2
- hello from site 3
