# Docker
## AWVS+nessus
docker pull leishianquan/awvs-nessus:v03
docker run -it -d -p 13443:3443 -p 8834:8834 leishianquan/awvs-nessus:v03
docker ps –a
docker start [docker_id]
docker exec -it [docker_id] /bin/bash
/etc/init.d/nessusd start
cp /home/license_info.json /home/acunetix/.acunetix/data/license/

``` 
  # Nessus:
  # https://127.0.0.1:8834/#/
  # nessus username:leishi
  # nessus password:leishianquan

  # Awvs13.0.200625101：
  # https://127.0.0.1:13443/
  # awvs13 username: leishi@leishi.com
  # awvs13 password: Leishi123
```