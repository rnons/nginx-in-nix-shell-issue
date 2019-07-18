I have a `nginx.conf` that looks like this

```
    server {
        listen 3000;
        server_name ~^(?<sub>.+)\.localhost$;
        root www/$sub;
    }
```

And `www/hello/index.html` contains only `hello world` text.

The idea is `http://hello.localhost` will be served from `www/hello` directory. Using system-wide nginx works fine, however, when I run nginx in nix-shell, I get 500 error without any more error message.

## run nginx in nix-shell

```
nix-shell -p "nginx" --run "nginx -p . -c nginx.conf"
```

```
% curl hello.localhost:3000

<html>
<head><title>500 Internal Server Error</title></head>
<body>
<center><h1>500 Internal Server Error</h1></center>
<hr><center>nginx/1.16.0</center>
</body>
</html>
```

## run system wide nginx

```
sudo nginx -p . -c nginx.conf
```

```
% curl hello.localhost:3000

hello world
```
