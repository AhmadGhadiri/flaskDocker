# A website hosted on Docker

This is a simple website that is using containers to host the website. The website can be built on top of a container and it can be run using that container and a sql container.


## Build

Build the container for the project:
```bash
$ docker build -t flaskdock .
```

## Run the website

1. Run a sql container:
```bash
$ docker run --name ahmadSql -v /home/ahmad/pythonWebApp/data:/docker-entrypoint-initdb.d -e MYSQL_DATABASE=BucketList -e MYSQL_USER=ahmad -e MYSQL_PASSWORD=ahmad -e MYSQL_ROOT_PASSWORD=ahmad -d mysql:5
```

2. Find the host, the default is __172.17.0.2__
```bash
$ docker inspect ahmadSql | grep IPAddress
```

3. Change the host address in the app.py if needed

4. Run the container for the application
```bash
$ docker run -p 5001:80 --link ahmadSql:mysql --volume=/home/ahmad/pythonWebApp:/app flaskdock 
```

5. Open the website in ```http://localhost:5001```

