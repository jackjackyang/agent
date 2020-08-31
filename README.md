我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# agent(网关）

[![Build Status](https://travis-ci.org/gonet2/agent.svg?branch=master)](https://travis-ci.org/gonet2/agent)

## 特性

1. 处理各种协议的接入，同时支持TCP和UDP(KCP协议)，进行双栈通信。
1. 连接管理，会话建立，数据包加解密(DH+RC4)。
1. **透传**解密后的原始数据流到后端（通过gRPC streaming)。
1. **复用**多路用户连接，到一条通往game的物理连接。
1. 不断开连接切换后端业务。
1. 唯一入口，安全隔离核心服务。

## 协议号划分

数据包会根据协议编号（0-65535) **透传** 到对应的服务， 例如(示范）:      

      1-1000: 登陆相关协议，网关协同auth服务处理。
      1001-10000: 游戏逻辑段
      ....
      
具体的划分根据业务需求进行扩展或调整。

## 消息封包格式
 
        +----------------------------------------------------------------+     
        | SIZE(2) | TIMESTAMP(4) | PROTO(2) | PAYLOAD(SIZE-6)            |     
        +----------------------------------------------------------------+     
        
> SIZE: 后续数据包总长度         
> TIMESTAMP: 数据包序号           
> PROTO: 协议号           
> PAYLOAD: 负载           
