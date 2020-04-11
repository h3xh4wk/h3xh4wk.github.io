# owasp zap - A free web app security tool

Read the getting started
[guide](https://github.com/zaproxy/zap-core-help/wiki/HelpStartStart). The
[getting started
pdf](https://github.com/zaproxy/zaproxy/releases/download/2.7.0/ZAPGettingStartedGuide-2.7.pdf) 
recommened to me by some veterans on slack channel.

Please follow the below steps to start with Owasp ZAP using docker. 

## Installation and Setup

- Get docker

Use the below commands to download and install docker.

```
sudo apt-get update
sudo apt install docker.io
# I am using Kali
# if you run into some errors then update apt repositories using --fix-missing option

```


- Get owasp/zap stable docker image

```
sudo docker pull owasp/zap2docker-stable

```
For more details please refer the [Docker Wiki](https://github.com/zaproxy/zaproxy/wiki/Docker)

I started with using the GUI.

- start ZAP GUI 

```
docker run -u zap -p 8080:8080 -p 8090:8090 -i owasp/zap2docker-stable zap-webswing.sh

```

I saw that there was no console output after issuing the above command. As per
the instructions in Wiki, when I pointed my browser to
`http://localhost:8080/?anonym=true&app=ZAP` I was able to see the GUI in few
seconds.

Subsequent requests can be proxied via `http://localhost:8090`.

## Browser settings - certifcate and proxy

In the Zap GUI, under `Tools-->Options-->Dynamic ssl ceritificates` we need to
generate the root ca certificate and import the certificate into the browser. I
am using firefox and imported the generated certificate into the browser
certificate, so that I do not get SSL warnings.

Note: In my case the generated certicate was on the docker, so I had to copy
the certificate from the ZAP Dynamic Certificates windows into the clip board
and save it to my host machine before importing it into the browser.



## Get Sample application 

planning for owasp juice shop as suggested by mentor. Moreover, using zap on a
realtime application might result in other unfavourable consequences.

```
sudo docker pull bkimminich/juice-shop
docker run --rm -p 3000:3000 bkimminich/juice-shop

```

## What next ?

Next step is to learn about the content and functionality of the target
applicaiton. I will navigate into the main parts of the application and will
review the captured content in ZAP proxy.

I will publish my findings in my next post.

# Some other useful docker and system commands

```bash
sudo docker ps
sudo docker kill <container id> # as recvd from the previous command
sudo service docker status
sudo service docker start # in case the docker service is not running

```

