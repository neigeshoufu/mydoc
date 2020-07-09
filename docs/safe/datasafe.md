# **数据安全复习**

[TOC]

## **1-OSI七层模型和TCP/IP协议栈的层次、定义、功能（重点）**

### **1.1-分层**

#### **1.1.1-OSI七层参考模型**

- **应用层**
网络服务与最终用户的一个接口。
协议有：HTTP FTP TFTP SMTP SNMP DNS TELNET HTTPS POP3 DHCP
- **表示层**
数据的表示、安全、压缩。（在五层模型里面已经合并到了应用层）
格式有，JPEG、ASCll、EBCDIC、加密格式等 [2] 
- **会话层**
建立、管理、终止会话。（在五层模型里面已经合并到了应用层）
对应主机进程，指本地主机与远程主机正在进行的会话
- **传输层**
定义传输数据的协议端口号，以及流控和差错校验。
协议有：TCP UDP，数据包一旦离开网卡即进入网络传输层
- **网络层**
进行逻辑地址寻址，实现不同网络之间的路径选择。
协议有：ICMP IGMP IP（IPV4 IPV6）
- **数据链路层**
建立逻辑连接、进行硬件地址寻址、差错校验 [3]  等功能。（由底层网络定义协议）
将比特组合成字节进而组合成帧，用MAC地址访问介质，错误发现但不能纠正。
- **物理层**
建立、维护、断开物理连接。（由底层网络定义协议）

#### **1.1.2-TCP/IP五层模型**

- **链路层**
所以链路层的主要工作就是对电信号进行分组并形成具有特定意义的数据帧，然后以广播的形式通过物理介质发送给接收方。
- **网络层**
网络层的主要工作是定义网络地址、区分网段、子网内MAC寻址、对于不同子网的数据包进行路由。
- **传输层**
传输层的主要工作是定义端口，标识应用程序身份，实现端口到端口的通信，TCP协议可以保证数据传输的可靠性。
- **应用层**
应用层的主要工作就是定义数据格式并按照对应的格式解读数据。

## **2-网络安全的基本要素与基本要素的含义。（重点）**

### **2.1-网络安全的定义**
 > &ensp;&ensp;从本质上讲，网络安全就是网络上的信息安全，是指网络系统的硬件、软件和系统中的数据受到保护，不受偶然的或者恶意的攻击而遭到破坏、更改、泄露，系统连续可靠正常地运行，网络服务不中断。
 &ensp;&ensp;广义上讲，凡是涉及到网络上信息的保密性、完整性、可用性、真实性和可控性的相关技术和理论都是网络安全所要研究的领域。 
 
### **2.2-网络安全的基本要素**

> 基本要素是机密性bai、完整性、可用性、可控性、可审查性。

- ```保密性```：信息不泄露给非授权用户、实体或过程，或供其利用的特性。

- ```完整性```：数据未经授权不能进行改变的特性。即信息在存储或传输过程中保持不被修改、不被破坏和丢失的特性。

- ```可用性```：可被授权实体访问并按需求使用的特性。即当需要时能否存取所需的信息。例如网络环境下拒绝服务、破坏网络和有关系统的正常运行等都属于对可用性的攻击。

- ```可控性```：对信息的传播及内容具有控制能力。

- ```可审查性（不可否认性）```：出现安全问题时提供依据与手段。

> 保密性（confidentiality）与Integrity（完整性）和 Availability（可用性）并称为信息安全的CIA三要素。

## **3-黑客常用的攻击手段（非重点）**

### **3.1-常用的攻击手段**

- 后门程序
- 信息炸弹
- 拒绝服务
- 网络监听

### **3.2-黑客攻击的一般过程**
![黑客攻击.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=6a6bULgoQbUbifzLknYgwxZ7FmzNwQvVCs8jQBff4hsw2i5_V9Tz5Arf-WCxPJz0rRVtsBHLJOJB02XJqs-XuRCjTFl_AxB_D8okpr_e0qeCKVulmUOi_3X1XRYjkDNa3BKZJlstVBpHex7ZrN15Aw&file_name=/%E9%BB%91%E5%AE%A2%E6%94%BB%E5%87%BB.png)

### **3.3-DOS和DDOS**

#### **3.3.1-DOS（拒绝服务攻击）**
> 拒绝服务，造成DoS的攻击行为被称为DoS攻击，其目的是使计算机或网络无法提供正常的服务。最常见的DoS攻击有计算机网络宽带攻击和连通性攻击。

#### **3.3.2-DDOS（分布式拒绝服务攻击）**
> 指处于不同位置的多个攻击者同时向一个或数个目标发动攻击，或者一个攻击者控制了位于不同位置的多台机器并利用这些机器对受害者同时实施攻击。由于攻击的发出点是分布在不同地方的，这类攻击称为分布式拒绝服务攻击，其中的攻击者可以有多个。

## **4-数据加密技术（重点、难点）**

### **4.1-对称加密算法**

- 包含的算法
主要有DES算法，3DES算法，TDEA算法，Blowfish算法，RC5算法，IDEA算法。

### **4.2-非对称加密算法**

- **简述**
非对称加密算法需要两个密钥：公开密钥（publickey:简称公钥）和私有密钥（privatekey:简称私钥）。公钥与私钥是一对，如果用公钥对数据进行加密，只有用对应的私钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。

- **过程**
基本过程是：甲方生成一对密钥并将公钥公开，需要向甲方发送信息的其他角色(乙方)使用该密钥(甲方的公钥)对机密信息进行加密后再发送给甲方；甲方再用自己私钥对加密后的信息进行解密。甲方想要回复乙方时正好相反，使用乙方的公钥对数据进行加密，同理，乙方使用自己的私钥来进行解密。
- **主要算法**
RSA、Elgamal、背包算法、Rabin、D-H、ECC（椭圆曲线加密算法）

### **4.3-混合加密体系**
![hunhe.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=010dbUVy_d392ouuZxyRrnkyNkGxA19LsJwLQfy6na4j8QFNtiy0c4nkW3_2-B02ILUgFXVJ-Pq-BDy0W4Y3umw3Z-vEl08sXt897ci-JWk-xXo_KlqQDoH0-4CKaCQYL8rEUdGa62Tv&file_name=/hunhe.png)

### **4.4-数字签名**
> 数字签名是非对称密钥加密技术与数字摘要技术的应用。数字签名必须保证以下几点：
接收者能够核实发送者对报文的签名；
发送者事后不能抵赖对报文的签名；
接收者不能伪造对报文的签名。


![shuziqianm.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=a94aHeWKwiviIFcHb9hDYvvK_OU0YLHTKfPkbkk5atjhc1CtXm4ZXxgUqOW2jujfxKiU6OkyFz-Fd8GnWyvkf8GZPdvD0yLnJlAUIUUfkFCUrDLSKUy-I42GR1rorVeLsHli_65_tCYVgPamI0o&file_name=/shuziqianm.png)

![jiamishuzi.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=6575YOZj3tZG2i1MLiI7CZv9sSPi-zZ2SDntmghH_gN26-Ppj_FfDhFVSOsYW1WHm8MWndPFis3r2QIOKhBlTiW_SXVzs2Vk_YsFKpv8ZsqDSYeeH4N4ogHeXXMWYUOaWEyFy9bb_iaZf6vh78Q&file_name=/jiamishuzi.png)

#### **4.4.1-主要算法**
> 基于公钥密码体制和私钥密码体制都可以获得数字签名，主要是基于公钥密码体制的数字签名。包括普通数字签名和特殊数字签名。普通数字签名算法有RSA、ElGamal、Fiat-Shamir、Guillou- Quisquarter、Schnorr、Ong-Schnorr-Shamir数字签名算法、Des/DSA，椭圆曲线数字签名算法和有限自动机数字签名算法等。

#### **4.4.2-报文鉴别技术**

![hash.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=7f94-JR8c2wWbphAtsxLD4zgDEYNxTEkah3R3TbjwS6HXFL8n9eNBH7wK4anY7QZItfMymAEPoRhZfR5nAbMmN2WYanno3f1S4u9Ye9TGixP8SN1ZUWorjIIAn8BF6XF86IzUZVkbsc&file_name=/hash.png)

![md5.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=a74b5w0x3B8Ke_TjGKswC0a4Cm3uDJoybpAogBNdwMq5GiGqss7fERXGU6tBCeaQlKJA5NoVWVb0mVIHAuIIEv9Ec_89P9qs3wuHyH-QVmn9r-oCAKyu4MV20l3MXbTNNTysK0cr8Q&file_name=/md5.png)
![sha.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=0ee9BVJ46OGlhU1IjewkvP-BfaWjpZjchaSz56nlkd-doqQ499inJ_ktKTpcuEJng2F-CmO0I9bERLyonirsvT40_dE5Nr_TbJZ-TwbHFswtARZSBDw834l3kZqDTZjkhw3iMGNU8g&file_name=/sha.png)

## **5-GRE隧道技术与IPSec vpn的区别（重点）**

### **5.1-GRE隧道技术**

- ```GRE（Generic Routing Encapsulation）```即通用路由封装协议，是对某些网络层协议（如IP和IPX）的数据报进行封装，使这些被封装的数据报能够在另一个网络层协议（如IP）中传输。
- GRE: （Generic Routing Encapsulation） 是一项由 Cisco 公司开发的轻量级隧道协议，它能够将各种网络协议（IP非IP）封装到IP隧道内。并通过IP互联网络在Cisco路由器间```创建一个虚拟的点对点隧道链接```。将GRE称为轻量级隧道协议的主要原因是，GRE头部较小，因此用它封装数据效率高。```但GRE没有任何安全防护机制```。
- GRE是VPN（Virtual Private Network）的第三层隧道协议，即在协议层之间采用了一种被称之为Tunnel（隧道）的技术。

### **5.2-IPsec**

- IPsec VPN（Internet Protocol Security Virtual Private Network）是采用IPSec协议来实现远程接入的一种VPN技术。
- IPSec是由Internet Engineering Task Force （IETF）定义的安全标准框架，在公网上为两个私有网络提供安全通信通道，通过加密通道保证连接的安全，提供私密数据封包服务。
VPN作为一项成熟的技术，广泛应用于组织总部和分支机构之间的组网互联，其利用组织已有的互联网出口，虚拟出一条“专线”，将组织的分支机构和总部连接起来，组成一个大的局域网。
- VPN用户访问内网资源还需为拔入到UTM25的用户分配一个虚拟的私有IP，使SSL VPN客户端的用户可以像局域网用户一样能正常访问局域网内的资源。
![ipc.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=fe4dEOmQD9aRKfZ259mhlKJEoQIFeUWu6u2KkAL7iyc-gG4zVfqDAcgKoaRf6yQXH0Dblm6CoLYObZEySF-hULtV6Yw-ZeCpT2dOfnBZCAoWIUskAZ_ytEmpZb_tTyl8pkOBNiaQig&file_name=/ipc.png)

### **5.3-区别**
> GRE隧道不提供安全性保障。使用ipsec加密gre隧道是现网中比较常用的VPN部署，它的加密方式分为两种，可以使用IPsec来加密隧道进行传输，叫做IPsec over GRE，也可以加密数据流后从隧道传输，称为GRE over IPsec。

## **6-基于数据的入侵检测的工作模式（非重点）**
> 侵检测的基本原理：主要分为四个阶段：
1、数据收集：数据收集是入侵检测的基础，采用不同的方法进行分析。
2、数据处理：从原始数据中除去冗余、杂声，并且进行格式化以及标准化处理。
3、数据分析：检查数据是否正常，或者显示是否存在入侵。
4、响应处理：发现入侵，采取措施进行保护，保留入侵证据并且通知管理员

## **7-防火墙技术（重点、难点）**

### **7.1-防火墙的分类**
![firewall.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=28ae3Kt8dd14eftevqshymT6peH__m_Os0UkCdt2wMEeY2g4RYwJ638wSzM5mpmD33RhoB6GyzF8YR1Gobw8pNOg0zR2musUsL4iAaE60Im3wxRbF75zsMUE7hE0unEbPmGo1j0z2pvBSNqK&file_name=/firewall.png)
![firewall2.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=c579cP4k7BcAK53CuaILkrj3rA8NvNbBzFJFlD-e4Vl9EJeDKFTWuFMky_iYnkpjVEZAOIx1WPc6iYGY7a4ufUkPHh58l5YTvBJDocS7iktcNEN4-_GFbSd1EHOMtS7wVvq2IzwE4wH8Cm82Qg&file_name=/firewall2.png)
### **7.2-防火墙的体系结构**
![tixjiegou.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=b3ac_WjgD2PrpsVEc6HlDGpXt6fAxyqIggnZ8n7WR-8ywuRZJxFisXq7gpaBHoDDxH2ZjWytWj12-4DGFohsnLPmnn8lCSyQF6Lg-rAImIT92nZli2TOLrYUtK2HNrz-deHST49N9GTtiQ1Bqg&file_name=/tixjiegou.png)
![beipp.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=7348WzuHb55sGpF4dG9lnCFDEwHwExcF7zw7nOUVX-95ott-HCUI10iTIN6ZU__eewXpAmwhxEVSYzkoN3mSvtMO9o9xx0Zf-WDRfVTuxU2CCEglfHG_Bxle3jzGxgVg7dqlV2gHmhMl&file_name=/beipp.png)
![dmz.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=aa7erROYaaxYMkmCFFv9f0xP2KAzMJ5ZnusVWgoEPrq534Wa5MweJE_DACnVir_uezFB4mFy8LiytKtpHOUmZhkEL07MSLaw-6Vx4EdgkZ-uN1BxpVCnGtdLgs0Cw-m-HDBWUUXUYw&file_name=/dmz.png)

### **7.3-包过滤防火墙（工作原理、优缺点、ACL的配置）**
![包过滤.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=399bDLvJ-IdB5AwutuByMaD--E-OcCooGYaaxRJay3rylhUUw9uiOqk0wwBLyfnsg_baakoIYmNNZnufLV96RJfx_zhZk5tIolG0kh47jc1GcogBxUiSwCJ7WyKrhLQL1xOyeEBN-DyN0mHLfg&file_name=/%E5%8C%85%E8%BF%87%E6%BB%A4.png)

#### **包过滤流程**
![包过滤流程.png](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=376bocx-X6n98wHhjzr4ktyCpB4ON5TLZYWiB2VdUi0DqkFi1VSsxA_m5ga3cn46GjLxRvjTH7M-y3qfksrOH0BBNnNfu0GdZB6zHBIyT0SfIj8xBoEI63QhD7VlHZz3FPQ2U51QcfAM9V16froMcFbexg&file_name=/%E5%8C%85%E8%BF%87%E6%BB%A4%E6%B5%81%E7%A8%8B.png)

**动态包过滤防火墙的工作流程**
![动态包过滤.jpg](http://cloud.wydxsdac.top:8088/cloud/index.php?user/publicLink&fid=5840R3fE2yeTkd1Y6FIsH0V1951iaDFGm-bdexdckhFvG5j3lCIqW1H2MrgItFb_hqnpgAewxXGDUhVIGStqu8ougmldPmgYIjcR0w13kC12-4qfjeBIF-MC5oaJJEjJLsv_bdtsmoyiXGd9BTJiqhafag&file_name=/%E5%8A%A8%E6%80%81%E5%8C%85%E8%BF%87%E6%BB%A4.jpg)

#### **优缺点**

##### **优点**
- 对于一个小型的、不太复杂的站点，包过滤比较容易实现。
- 因为过滤路由器工作在IP层和TCP层，所以处理包的速度比代理服务器快。
- 过滤路由器为用户提供了一种透明的服务，用户不需要改变客户端的任何应用程序，也不需要用户学习任何新的东西。因为过滤路由器工作在IP层和TCP层，而IP层和TCP层与应用层的问题毫不相关。所以，过滤路由器有时也被称为“包过滤网关”或“透明网关”，之所被称为网关，是因为包过滤路由器和传统路由器不同，它涉及到了传输层。
- 过滤路由器在价格上一般比代理服务器便宜。

##### **缺点**
- 由于无法对数据报的内容进行核查，一次无法过滤或审核数据报的内容
- 由于此种类型的防火墙工作在较低层次，防火墙本身所能接触的信息较少，所以它无法提供描述细致事件的日志系统。
- 所有可能用到的端口（尤其是大于1024的端口）都必须开放，对外界暴露，从而极大地增加了被攻击的可能性
- 如果网络结构比较复杂，那么对管理员而言配置访问控制规则将非常困难

#### **ACL的配置**

- 略。具体查看思科网络学院。

### **许可**
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">知识共享署名-非商业性使用 4.0 国际许可协议</a>进行许可。

- 内阁首辅2020-7-8&16：34&于汉堡王