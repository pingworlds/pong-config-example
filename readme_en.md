# pong-config-example


- [中文](README.md)
- [English](readme_en.md)


## Standalone boot

Standalone startup mode supports all protocols


## web server

Although pong-go is independent of the web server, not all web servers work in harmony with it, mainly because tls does not shake hands properly.
 
The sample configuration template for this project is generic for proxy protocols pong , socks5, qsocks, shadowsocks,vless




### caddy2

#### caddy standard

support http2, websocket 

    - h2 <--> caddy2 <--> h2c   
    - wss <--> caddy2 <--> ws   

#### caddy with caddy-layer4

tcp,tls,http,https,http2,h2c,h3,ws,wss... should be supported


### nginx
  
    - wss <--> nginx <--> ws


### apache



### proxy protocol 

### shadowsocks

No encryption support

### vless

No encryption support

### socks5

Does not support authentication


### qsocks 

qsocks is a simplified version of socks5, removing the handshake process, ver 0x07

Header structure
 
    +------+------+------+-----------+-----------+
    | VER | CMD | ATYP | DST.ADDR | DST.PORT |
    +------+------+------+-----------+-----------+
    | 1 | 1 | 1 | Variable | 2 |
    +------+------+------+-----------+-----------+
 
local After sending the header, continue to send the data that needs to be forwarded

remote After receiving the header, open the dst network connection, close it directly if it fails, and start relaying after it succeeds