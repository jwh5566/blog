## socket，IP和简单C/S编程
### 作者               
jwh5566                
                
### 日期              
2017-09-13                  
                
### 标签              
python，python2，socket， ipv4
                
----  
### 打印主机名和IP地址
```python
import socket


def print_machine_info():
    host_name = socket.gethostname()
    ip_address = socket.gethostbyname(host_name)
    print "Host name: %s" % host_name
    print "IP address: %s" % ip_address

if __name__ == '__main__':
    print_machine_info()

```
执行结果:
>Host name: ZXW-20160304LTC
IP address: 172.168.1.8

### 获取远程服务器的ip地址信息(类似通过域名找ip)
```python
import socket

def get_remote_machine_info():
    remote_host = 'www.python.org'
    try:
        print "IP address of %s: %s" %(remote_host,socket.gethostbyname(remote_host))
    except socket.error, err_msg:
        print "%s: %s" %(remote_host, err_msg)

if __name__ == '__main__':
    get_remote_machine_info()

```
执行结果:
>IP address of www.python.org: 151.101.72.223
### 根据端口号和协议找出相关的服务名

```python
import socket

def find_service_name():
    protocolname = 'tcp'
    for port in [80, 25, 23]:
        print "Port: %s => service name: %s" %(port, socket.getservbyport(port, protocolname))
    print "Port: %s => service name: %s" % (53, socket.getservbyport(53, 'udp'))

if __name__ == '__main__':
    find_service_name()
```
执行结果:
>Port: 80 => service name: http
Port: 25 => service name: smtp
Port: 23 => service name: telnet
Port: 53 => service name: domain

### 转换网络字节和主机字节顺序
```python
import socket

def convert_integer():
    data = 1234
    # 32 bits
    print "Original: %s => Long host byte order: %s, Network byte order: %s" %(data, socket.ntohl(data), socket.htonl(data))
    # 16 bits
    print "Original: %s => Short host byte order: %s, Network byte order: %s" %(data, socket.ntohs(data), socket.htons(data))
if __name__ == '__main__':
    convert_integer()
```
执行结果:
>Original: 1234 => Long host byte order: 3523477504, Network byte order: 3523477504
Original: 1234 => Short host byte order: 53764, Network byte order: 53764
