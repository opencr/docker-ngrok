git clone https://github.com/opencr/docker-ngrok.git

cd docker-ngrok

docker build -f ./Dockerfile -t liuhenghuo/ngrok:latest .

启动容器生成ngrok客户端
docker run --rm -it -e DOMAIN="ng.l0411.com" -v /data/ngrok:/myfiles liuhenghuo/ngrok sh /build.sh

启动容器
docker run -idt --name ngrok-server \
-v /data/ngrok:/myfiles \
-p 8082:80 \
-p 4432:443 \
-p 4443:4443 \
-e DOMAIN='ng.l0411.com' liuhenghuo/ngrok /bin/sh /server.sh

客户端配置
server_addr: "wlniao.cn:4443"
trust_host_root_certs: false
tunnels:
  test:
    proto:
      http: 80

启动客户端命令
ngrok -config ngrok.cfg start test            #启动指定转发配置
ngrok -config ngrok.cfg start-all             #启动全部转发配置
ngrok -config ngrok.cfg 4040                  #启动web转发，随机子域名
ngrok -config=ngrok.cfg -subdomain=test 4040  #启动http转发，子域名：test
ngrok -config ngrok.cfg -proto=tcp 127.0.0.3:3389   #启动tcp转发 本地3389端口，远程随机暴露大端口
