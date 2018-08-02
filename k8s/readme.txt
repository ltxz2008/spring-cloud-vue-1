mkdir -p /root/test/eureka/  && cp  *.jar   /root/test/eureka/   && cp  docker/Dockerfile  /root/test/eureka/ 
mkdir -p /root/test/config/  && cp  *.jar   /root/test/config/   && cp  docker/Dockerfile  /root/test/config/ 
mkdir -p /root/test/zipkin/  && cp  *.jar   /root/test/zipkin/   && cp  docker/Dockerfile  /root/test/zipkin/ 
mkdir -p /root/test/simple/  && cp  *.jar   /root/test/simple/   && cp  docker/Dockerfile  /root/test/simple/ 



docker build -t eureka:v1.0.0 .   &&  docker save eureka:v1.0.0 -o eureka-v1.0.0.tar  && scp eureka-v1.0.0.tar node02:/root/  && scp eureka-v1.0.0.tar node03:/root/ 
docker build -t config:v1.0.0 .   &&  docker save config:v1.0.0 -o config-v1.0.0.tar  && scp config-v1.0.0.tar node02:/root/  && scp config-v1.0.0.tar node03:/root/ 
docker build -t zipkin:v1.0.0 .   &&  docker save zipkin:v1.0.0 -o zipkin-v1.0.0.tar  && scp zipkin-v1.0.0.tar node02:/root/  && scp zipkin-v1.0.0.tar node03:/root/ 
docker build -t simple:v1.0.0 .   &&  docker save simple:v1.0.0 -o simple-v1.0.0.tar  && scp simple-v1.0.0.tar node02:/root/  && scp simple-v1.0.0.tar node03:/root/ 



[root@k8s-admin ~]# kubectl run --rm -it curl --image="docker.io/appropriate/curl" sh
[root@k8s-admin ~]# kubectl run --rm -it curl --image="gaozhi/mysql-client-alpine" sh 


[root@k8s-admin ~]# kubectl apply -f k8s-eureka.yam
[root@k8s-admin ~]# kubectl apply -f k8s-config.yam
[root@k8s-admin ~]# kubectl apply -f k8s-zipkin.yam
[root@k8s-admin ~]# kubectl apply -f k8s-simple.yam
[root@k8s-admin ~]# kubectl get pod,svc,ing -o wide
