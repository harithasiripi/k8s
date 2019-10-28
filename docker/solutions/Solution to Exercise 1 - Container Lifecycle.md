# Solution to Exercise 1 - Container lifecycle

## Step 1: Creating a container

Start a container with:

```bash
docker run -it busybox
top
```

You will now see the processes inside your container:

```bash-output
  PID  PPID USER     STAT   VSZ %VSZ CPU %CPU COMMAND
    1     0 root     S     1248  0.0   1  0.0 sh
   10     1 root     R     1240  0.0   0  0.0 top
```

## Step 2: Executing commands in containers

Start another shell into the container by issuing the following command. You will need your container's ID or its simple name.

```bash
docker exec -it <your container ID or Silly_Name> /bin/sh
```

Using the example above, it would be:

```bash
docker exec -it 567d71edcab0 /bin/sh
```

Perform `ps` or again `top` to see the processes that run in there.
If you started top, quit by pressing `q`. Detach from container using `ctrl + p` and then `ctrl + q`.

## Step 3: Getting logs of a container

`docker logs <your container ID or Silly_Name>`  displays the logs present at the time of execution as [documented](https://docs.docker.com/engine/reference/commandline/logs/). In our case it displays the `top` output, and if you run this command several times while container still runs, you'll see the output changes.

## Step 4: Killing containers

Run a new container from the nginx image:

```bash
docker run -d nginx
```

Perform `docker ps` to see the running containers.
Perform `docker stop <your container ID or Silly_Name>` (e.g. `docker stop 94cb514de45e`) to end your container.

## Step 5: Clean up

Unless you want to use the command `docker rm $(docker ps -aq)` (which REALLY deletes ALL the containers - and this might be dangerous !), you may also perform: `docker ps -a` to see a list with all the running & exited containers and then delete multiple of them with one command: `docker rm <container1> <container2> <containerN>`.

**Shortcut:** If you want to remove all containers, you can do it with these commands (use with caution).

```bash
docker container prune
```

or

```bash
docker rm $(docker ps -aq)
```
