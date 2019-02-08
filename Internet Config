# Simulating the internet
For simulating the internet, we simply ran two docker containers. Each docker container ran its own webserver on a different port. 
The ports that we used were:
 - 8080 (this was allowed in the Firewall)
 - 8181 (this was blocked in the Firewall)
 
## Running the docker containers
 
For running the webserver at port 8080, this simple command will be sufficient:
```
sudo docker run -itd -p 8080:8080 --rm --name app8080 mslotboom/app8080 
```

For running the webserver at port 8181, the following command will be sufficient:
```
sudo docker run -itd -p 8181:8181 --rm --name app8181 mslotboom/app8181
```
