# java-11-dockerfile使用
1. jar 包名称为 `app.jar`
2. lib 位置为 `./lib`
3. `application.yaml` 位置为 `./config/application.yaml`
4. jvm启动参数需添加至环境变量, key为 `JAVA_OPTS`
5. jar包额外参数需添加至环境变量, key为 `PARAMS`
6. 容器工作目录为 `/home` , 所有文件需挂载至此目录
7. 此镜像仅适用于环境隔离, 不适用于频繁删除及启动新容器

## 一般使用流程
1. 在干净的文件夹(例如 `/home/user/a` )下准备以下文件:
    1. 不包含依赖的启动jar包, 并命名为 `app.jar`
    2. 所有的依赖文件, 路径为 `lib/`
    3. 配置文件, 路径为 `config/application.yaml`
2. 启动容器
```shell
docker run -itd -p 50001:8080 \
  -v /home/user/a:/home \
  -e JAVA_OPTS="" \
  -e PARAMS="" \
  --restart=always \
  --name dev \
  fawn/java-11:1.0.0
```
示例启动命令
```shell
docker run -itd -v C:/Users/fawn/Desktop:/home -e PARAMS="--spring.profiles.active=dev" --name dev fawn/java-11:latest
```