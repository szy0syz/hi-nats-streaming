# hi-nats-streaming

>nats-streaming learn

## Demo-01

验证 `nats` 的消息稳定性

```bash
docker network ceate stan

docker run \
--network stan \
-p 4444:4444 \
--name server \
--volume /tmp/stan-demo:/data/msg \
nats-streaming -p 4444 --dir /data/msg --store file -DV
```

```bash
docker run \
--network stan \
--rm -it synadia\nats-box:latest

stan-pub --server server:4444 foo "hello foo"
# 发送命令同时此时立即关闭服务端，保证服务端 “没出现有消息” 的日志
# 消息会丢失吗？

stan-sub --server server:4444 foo
# 消息出现了！！！
```
