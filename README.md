# pong-config-example

- [中文](README.md)
- [English](readme_en.md)


## 独立启动

独立启动模式支持所有的协议


## web server

尽管pong-go 独立于 web server，但不是所有的web server都能与之和谐配合，主要是 tls 不能正确的握手.
 
本项目的配置模板样例，对代理协议 pong , socks5, qsocks, shadowsocks,vless 通用




### caddy2

#### caddy standard

support http2, websocket 

    - h2   <--->   caddy2   <--->  h2c   
    - wss  <--->   caddy2   <--->  ws   

#### caddy with caddy-layer4

tcp,tls,http,https,http2,h2c,h3,ws,wss... should be supported


### nginx
  
    - wss  <--->  nginx  <--->  ws


### apache



## proxy protocol 

###  shadowsocks

不支持加密

###  vless

不支持加密

###  socks5

不支持验证


### qsocks 

qsocks 是socks5的简化版，去掉了握手过程, ver号 为 0x07

头部结构
 
    +------+------+------+-----------+-----------+
    |  VER |  CMD | ATYP | DST.ADDR  |  DST.PORT |
    +------+------+------+-----------+-----------+
    |   1  |   1  |  1   | Variable  |    2      |
    +------+------+------+-----------+-----------+
 
local 发送头部后，继续发送需要转发的数据

remote 收到头部后，打开dst网络连接，打开失败直接关闭，打开成功后开始relay