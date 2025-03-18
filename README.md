# 镜像仓库使用方法

[**images.txt**](https://github.com/zhi35/docker-image-pusher/blob/main/images.txt)

```java
mysql:8.4.4
```

1. 在 `images.txt` 添加你需要的镜像（PR方式提交），你可以从 [https://hub.docker.com/](https://hub.docker.com/) 搜索需要的镜像后添加。
2. 新添加镜像，需要等待1分钟同步。之后通过命令 `docker pull registry.cn-shanghai.aliyuncs.com/zhi35com/mysql` 拉取你需要的镜像，如果有版本号，可以添加。如；`mysql:8.4.4`

```yml
mysql:
  image: registry.cn-shanghai.aliyuncs.com/zhi35com/mysql:8.4.4
  container_name: mysql
  command: --default-authentication-plugin=mysql_native_password
  restart: always
  environment:
    TZ: Asia/Shanghai
    MYSQL_ROOT_PASSWORD: 123456
  ports:
    - "13306:3306"
  volumes:
    - ./mysql/my.cnf:/etc/mysql/conf.d/mysql.cnf:ro
    - ./mysql/sql:/docker-entrypoint-initdb.d
  healthcheck:
    test: [ "CMD", "mysqladmin" ,"ping", "-h", "localhost" ]
    interval: 5s
    timeout: 10s
    retries: 10
    start_period: 15s
```

---

- 参考仓库 [@tech-shrimp/docker_image_pusher](https://github.com/tech-shrimp/docker_image_pusher)
