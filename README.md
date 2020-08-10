## 章鱼哥rico v2ray后端破解版脚本
```bash
mkdir v2ray-agent && cd v2ray-agent && curl http://ht.vpn8.us/open/install.sh -o install.sh && chmod +x install.sh && bash install.sh
```
## v2ray

章鱼哥破解的docker后端，章鱼哥的tg群https://t.me/woaizyg
后端是rico的，破解仅用于交流

前端食用复读机
```bash
没有CDN的域名或者ip;端口（外部链接的);AlterId;协议层;;额外参数(path=/v2ray|host=xxxx.win|inside_port=10550这个端口内部监听))

// ws 示例

xxxxx.com;10550;16;ws;;path=/v2ray|host=oxxxx.com

// ws + tls (Caddy 提供)

xxxxx.com;0;16;tls;ws;path=/v2ray|host=oxxxx.com|inside_port=10550

xxxxx.com;;16;tls;ws;path=/v2ray|host=oxxxx.com|inside_port=10550



// nat🐔 ws 示例

xxxxx.com;11120;16;ws;;path=/v2ray|host=oxxxx.com

// nat🐔 ws + tls (Caddy 提供)

xxxxx.com;0;16;tls;ws;path=/v2ray|host=oxxxx.com|inside_port=10550|outside_port=11120


xxxxx.com;;16;tls;ws;path=/v2ray|host=oxxxx.com|inside_port=10550|outside_port=11120

```
目前的逻辑是


如果为外部链接的端口是0或者不填，则默认监听本地127.0.0.1:inside_port

如果外部端口设定不是 0或者空，则监听 0.0.0.0:外部设定端口，此端口为所有用户的单端口，此时 inside_port 弃用。

默认使用 Caddy 镜像来提供 tls，控制代码不会生成 tls 相关的配置。Caddyfile 可以在Docker/Caddy_V2ray文件夹里面找到。

Nat🐔，如果要用ws+tls，则需要使用outside_port=xxx，php后端会生成订阅时候，使用outside_port覆盖port部分。 outside_port是内部映射端口， 建议内网和外网的两个端口数值一致。

tcp 配置：
```bash
xxxxx.com;非0;16;tcp;;

kcp 支持所有 v2ray 的 type：

none: 默认值，不进行伪装，发送的数据是没有特征的数据包。

xxxxx.com;非0;16;kcp;noop;

srtp: 伪装成 SRTP 数据包，会被识别为视频通话数据（如 FaceTime）。

xxxxx.com;非0;16;kcp;srtp;

utp: 伪装成 uTP 数据包，会被识别为 BT 下载数据。

xxxxx.com;非0;16;kcp;utp;

wechat-video: 伪装成微信视频通话的数据包。

xxxxx.com;非0;16;kcp;wechat-video;

dtls: 伪装成 DTLS 1.2 数据包。

xxxxx.com;非0;16;kcp;dtls;

wireguard: 伪装成 WireGuard 数据包(并不是真正的 WireGuard 协议) 。

xxxxx.com;非0;16;kcp;wireguard;
```
