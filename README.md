git clone https://github.com/opencr/docker-ngrok.git
cd docker-ngrok
docker build -f ./Dockerfile -t liuhenghuo/ngrok:latest .

docker run --rm -it -e DOMAIN="ng.l0411.com" -v /data/ngrok:/myfiles liuhenghuo/ngrok sh /build.sh

docker run -idt --name ngrok-server \
-v /data/ngrok:/myfiles \
-p 8082:80 \
-p 4432:443 \
-p 4443:4443 \
-e DOMAIN='ng.l0411.com' liuhenghuo/ngrok /bin/sh /server.sh
