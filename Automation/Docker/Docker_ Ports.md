# Multiple containers with different ports [video](https://www.youtube.com/watch?v=FT7zkZ_WPas)
- What exactly happens whe you use `-p` after `docker run`?
- Manually chosen ports vs dynamically allocated ports

`docker run -d --name nginx-port80 -p 80:80 nginx`
`docker ps`
```
CONTAINER ID   IMAGE                COMMAND                  CREATED             STATUS          PORTS                                       NAMES``
5e7a93df10ea   nginx                "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes    0.0.0.0:80->80/tcp, :::80->80/tcp   nginx-port83
```



To forward random port to port 80 on the host
`docker run -d --name nginx-dev -p 80 nginx`
`docker ps`
```
CONTAINER ID   IMAGE                COMMAND                  CREATED             STATUS          PORTS                                       NAMES
11b388f7e034   nginx                "/docker-entrypoint.…"   6 seconds ago       Up 6 seconds    0.0.0.0:49153->80/tcp, :::49153->80/tcp     nginx-dev
5e7a93df10ea   nginx                "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes    0.0.0.0:80->80/tcp, :::80->80/tcp   nginx-port80
```
To manually allocate port:
`docker run -d --name nginx-dev -p 40000:80 nginx`

Go to `nginx-dev` modify file and reload web browser
`docker exec -it nginx-dev /bin/bash`
```
root@11b388f7e034:/# cd /usr/share/nginx/html/
root@11b388f7e034:/usr/share/nginx/html# echo "Hello World" > index.html
```

If you are happy with the changes, we can commit those changes:
```
docker commit --message "Dev changes commited" 11b388f7e034
sha256:61cb86949e33105ac687829e35b1dfc1602d7e2021e7da0c0ed08e515f747fa7
```

It created a new image that starts with: 61cb86949e33
`docker images`
```
REPOSITORY    TAG       IMAGE ID       CREATED              SIZE
<none>        <none>    61cb86949e33   About a minute ago   142MB
nginx         latest    fa5269854a5e   7 days ago           142MB
```

Now we can tag it:
`docker tag 61cb86949e33 vitaly/custom-nginx:v1.0.1`
```
docker images
REPOSITORY            TAG       IMAGE ID       CREATED         SIZE
vitali/custom-nginx   v1.0.1    61cb86949e33   3 minutes ago   142MB
nginx                 latest    fa5269854a5e   7 days ago      142MB
```

Now we can push this image to docker hub

# What is `docker port` comamnd?
**Manual vs Dynamic port allocation**
To see which random port was assigned to `nginx-dev`
```shell
docker port nginx-dev
80/tcp -> 0.0.0.0:49153
80/tcp -> :::49153
```
You can access content that is serverd on port 80, by specifying  port  49153

Different port can be allocated:
`docker run -p  40000:80 -d nginx`