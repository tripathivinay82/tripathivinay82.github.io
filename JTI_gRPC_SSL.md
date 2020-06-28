## JTI (Juniper Telemetry Interface): 

**Project description:** Instructions to setup Telemtry using Secure gRPC (SSL) and OpenConfig (data format) between Juniper MX and Ubuntu 

### 1. Create GIT Repository for JTI Client [JTIMON](https://github.com/nileshsimaria/jtimon/)

```sh
* Setup Instructions
  *  go get github.com/nileshsimaria/jtimon
  *  cd go/bin/
  *  ./jtimon --help
```

### 2. Setup PKI (Public Key Infrastructure) using OpenSSL

```sh
* create private key and certiciate  for client (ubuntu)
* create private key and certiciate for server (router)
* move server .pem and .cert file to /var/tmp/ of Router 
* move client .cert file to /var/tmp/ of Router
* configure router
* start JTI subscription

root@<server>:~/Cert$ ls
	 client_RSA2048.csr
	 client_RSA2048.key.orig
	 client_RSA2048.crt
	 client_RSA2048.pem
	 server_RSA2048.csr
	 server_RSA2048.key.orig
	 server_RSA2048.key
	 server_RSA2048.crt
	 server_RSA2048.pem
	 client_RSA2048.key
```

### 3.  gRPC/SSL configuration at Server(MX)

```sh
set system services extension-service request-response grpc ssl address 10.49.167.137
set system services extension-service request-response grpc ssl port 50051
set system services extension-service request-response grpc ssl local-certificate msee
set system services extension-service request-response grpc ssl mutual-authentication certificate-authority root-ca
set system services extension-service request-response grpc ssl mutual-authentication client-certificate-request require-certificate-and-verify
set system services extension-service notification allow-clients address 0.0.0.0/0

set security certificates local msee "-----BEGIN PRIVATE KEY-----\nMIIEvQIBADANB.....\n-----END CERTIFICATE-----\n"
set security pki ca-profile root-ca ca-identity "JNPR Internal"

regress@IER# run file list /var/tmp/ detail 
/var/tmp/:
-rw-r--r--  1 regress wheel       client_RSA2048.crt
-rw-r--r--  1 regress wheel      server_RSA2048.crt
-rw-r--r--  1 regress wheel       server_RSA2048.pem

```

### 4.  JTI Sensor Config and Execution at Client(Ubuntu)

```sh
Execution: 
	jtimon --config test.json --print

root@server:~/Cert$ cat ~/telemetry/test.json 
{
    "host": "10.49.167.137",
    "port": 50051,
    "user": "regress",
    "password": "MaRtInI",
    "cid": "my-client-id",
    "grpc" : {
	"ws" : 524288
    },
    "tls" : {
 "clientcrt" : "/home/vinayt/Cert/client_RSA2048.crt",
 "clientkey" : "/home/vinayt/Cert/client_RSA2048.key",
 "ca" : "/home/vinayt/Cert/server_RSA2048.crt",
 "servername" : "regress"
     }, 
    "paths": [{
	"path": "/interfaces",
	"freq": 2000
    }, {
	"path": "/junos/system/linecard/cpu/memory/",
	"freq": 1000
    }]
}

```

### 5.   Key and Cert using OpenSSL at Client(Ubuntu)

```sh
[Reference](https://websiteforstudents.com/create-ssl-tls-self-signed-certificates-on-ubuntu-16-04-18-04-18-10/)

Client Phrase:
key: clab123
Cert challenge: cpwd123

Server Phrase:
key: slab123
Cert challenge: spwd123

openssl genrsa -des3 -out client_RSA2048.key 2048
openssl req -new -key client_RSA2048.key -out client_RSA2048.csr
cp client_RSA2048.key client_RSA2048.key.orig 
openssl rsa -in client_RSA2048.key.orig -out client_RSA2048.key
openssl x509 -req -days 365 -in client_RSA2048.csr -signkey client_RSA2048.key -out client_RSA2048.crt
openssl x509 -in client_RSA2048.crt -text
cat client_RSA2048.key client_RSA2048.crt >> client_RSA2048.pem


openssl genrsa -des3 -out server_RSA2048.key 2048
openssl req -new -key server_RSA2048.key -out server_RSA2048.csr
cp server_RSA2048.key server_RSA2048.key.orig 
openssl rsa -in server_RSA2048.key.orig -out server_RSA2048.key
openssl x509 -req -days 365 -in server_RSA2048.csr -signkey server_RSA2048.key -out server_RSA2048.crt
openssl x509 -in server_RSA2048.crt -text
cat server_RSA2048.key server_RSA2048.crt >> server_RSA2048.pem

```

### 6.   Verification at Server(MX)

```sh
regress@IER> show system connections | match 50051                                  
tcp4       0      0  10.49.167.137.50051                           10.13.139.90.48094                            ESTABLISHED
tcp4       0      0  10.49.167.137.50051                           *.*                                           LISTEN

regress@IER> show extension-service request-response clients 
Client ID              Socket Address                     Client Type   Channel Count
my-client-id           ipv6:::ffff:10.13.139.90:48094     gRPC               1

regress@IER> show extension-service request-response clients detail 
Channel information:
Client ID: my-client-id
Socket Address: ipv6:::ffff:10.13.139.90:48094
Client Type: gRPC
Channel Count: 1

Channel target: unix:/var/run/japi_na-grpcd
Channel status: GRPC_CHANNEL_READY

regress@IER> show extension-service request-response servers           
gRPC server information:
Max connections: 5, Skip-authentication: Disabled

Address: 10.49.167.137, Port: 50051
Status: Up, Type: SSL

Address: unix:/var/run/japi_jsd
Status: Up, Type: Clear-text

regress@IER> show security pki ca-certificate detail 
Certificate identifier: root-ca
Certificate version: 1
Serial number: 2c798585ededb521ebf91168c7500b8a4f0460a5
Issuer:
Organization: JNPR, Country: US, State: MA, Locality: WESTFORD, Common name: IER
Subject:
Organization: JNPR, Country: US, State: MA, Locality: WESTFORD, Common name: IER
Subject string: 
C=US, ST=MA, L=WESTFORD, O=JNPR, CN=IER, emailAddress=abc@abc.com
Validity:
Not before: 06-19-2020 00:01 UTC
Not after: 06-19-2021 00:01 UTC
Public key algorithm: rsaEncryption(2048 bits)
30:82:01:0a:02:82:01:01:00:c0:5a:08:d2:0d:05:2e:b0:f2:06:8d
b6:da:e3:92:72:0d:00:e9:f2:3d:63:43:e0:71:b7:ed:36:8e:b1:96
b9:29:13:4c:16:2d:81:f1:66:3e:8e:af:1b:54:d3:81:c1:53:41:25
0b:83:ab:ae:3e:99:83:cc:1d:e3:09:77:0d:87:de:c8:a6:d1:9c:a4
55:df:ac:69:39:45:df:70:38:5c:bf:1d:ea:88:8b:ec:9d:9c:eb:a3
50:3f:e7:7a:98:c5:24:6a:ff:95:69:44:00:e7:af:33:96:13:9e:e4
af:ec:59:7f:2e:b0:b3:e4:75:4b:f7:30:f3:cb:67:fd:c3:33:cd:a8
b6:c8:cb:fa:b7:bf:69:3e:a8:f1:45:db:4e:46:73:90:81:ad:ce:6f
0a:c2:5b:ca:55:81:23:68:63:dd:ab:c6:25:e9:06:ad:dd:ee:59:04
da:bb:a9:03:a4:16:b1:c4:9a:5e:e5:bc:a7:55:f6:bd:9c:a2:7e:21
f3:f4:6e:b0:e6:2e:6b:c4:a9:c4:55:26:1c:11:d7:40:34:6a:63:03
db:4e:64:db:dd:78:8b:57:0b:67:f2:82:57:ef:55:c1:70:36:54:dc
dd:9a:19:aa:09:2c:5e:7f:28:f0:0a:ff:65:1a:76:a0:31:81:d2:80
c1:51:3d:b2:e5:02:03:01:00:01
Signature algorithm: sha256WithRSAEncryption
Fingerprint:
98:9d:61:d1:b6:1b:dc:ec:9b:04:18:8a:b6:4a:72:71:f3:90:15:38 (sha1)
8b:18:4b:71:f2:5e:2f:43:90:a7:f0:0b:fe:03:45:73 (md5)

regress@IER> show ephemeral-configuration instance junos-analytics 
## Last changed: 2020-06-18 18:05:17 PDT
services {
analytics {
export-profile export_1000 {
    transport grpc;
}
export-profile export_1001 {
    transport grpc;
}
sensor sensor_1000 {
    export-name export_1000;
    resource /interfaces/;
    subscription-id 1000;
    reporting-rate 2;
    life-time long-lived;
}
sensor sensor_1001 {
    export-name export_1001;
    resource /junos/system/linecard/cpu/memory/;
    subscription-id 1001;
    reporting-rate 1;
    life-time long-lived;
}
}
}

regress@IER> show system processes extensive | match "xmlproxyd|na-grpcd|na-mqttd|agentd|jsd|mgd-api" 
7634 root      20    0   716M  7680K select  1   0:22   0.68% xmlproxyd
59694 root      20    0   737M 20812K select  0   0:00   0.10% jsd{jsd}
7633 nobody    20    0 51148K  6772K select  0   0:41   0.00% na-mqttd
7637 root      20    0 25852K  7416K select  1   0:20   0.00% na-grpcd{na-grpcd}
7650 root      20    0   741M 19960K select  1   0:08   0.00% agentd{agentd}
7637 root      20    0 25852K  7416K nanslp  0   0:03   0.00% na-grpcd{na-grpcd}
7637 root      20    0 25852K  7416K nanslp  0   0:02   0.00% na-grpcd{na-grpcd}
7650 root      20    0   741M 19960K select  1   0:01   0.00% agentd{agentd}
59694 root      20    0   737M 20812K select  1   0:01   0.00% jsd{jsd}
59694 root      20    0   737M 20812K select  0   0:01   0.00% jsd{jsd}
7573 root      20    0   716M  7692K select  0   0:00   0.00% mgd-api
7637 root      20    0 25852K  7416K select  0   0:00   0.00% na-grpcd{na-grpcd}
59694 root      20    0   737M 20812K select  0   0:00   0.00% jsd{jsd}
59694 root      20    0   737M 20812K select  1   0:00   0.00% jsd{jsd}
7649 root      22    0   720M  8520K select  1   0:00   0.00% stats-agentd
7637 root      20    0 25852K  7416K nanslp  0   0:00   0.00% na-grpcd{na-grpcd}
7637 root      20    0 25852K  7416K nanslp  0   0:00   0.00% na-grpcd{na-grpcd}
7637 root      20    0 25852K  7416K select  1   0:00   0.00% na-grpcd{na-grpcd}

regress@IER> show agent sensors | no-more    

Sensor Information : 

Name                                    : __default_fabric_sensor__ 
Resource                                : /junos/system/linecard/fabric/ 
Version                                 : 1.0                  
Sensor-id                               : 2277069355            
Subscription-ID                         : 562952230490667      
Parent-Sensor-Name                      : Not applicable       
Component(s)                            : PFE                   

Server Information : 

Name                                : __default__snmp_server__ 
Scope-id                            : 0                     
Remote-Address                      : 0.0.0.0               
Remote-port                         : 0                     
Transport-protocol                  : UDP                   

Profile Information : 

Name                                : __default_snmp_export_profile__ 
Reporting-interval                  : 30                    
Payload-size                        : 5000                  
Address                             : 0.0.0.0               
Port                                : 0                     
Timestamp                           : 0                     
Format                              : GPB                   
DSCP                                : 0                     
Forwarding-class                    : 0                     
Loss-priority                       : low                  

Sensor Information : 

Name                                    : sensor_1000           
Resource                                : /interfaces/          
Version                                 : 1.0                  
Sensor-id                               : 539528115             
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : Not applicable       
Component(s)                            : PFE,PFE,PFE,dcd,mib2d,xmlproxyd 

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_1_1       
Resource                                : /junos/system/linecard/interface/logical/usage/ 
Version                                 : 1.1                  
Sensor-id                               : 3139259737            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : PFE                   

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_1_2       
Resource                                : /junos/system/linecard/interface/queue/ 
Version                                 : 1.0                  
Sensor-id                               : 3139259738            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : PFE                   

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_1_3       
Resource                                : /junos/system/linecard/interface/traffic/ 
Version                                 : 1.0                  
Sensor-id                               : 3139259739            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : PFE                   

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_2_1       
Resource                                : /interfaces/          
Version                                 : 1.0                  
Sensor-id                               : 3139256665            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : dcd                   

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_4_1       
Resource                                : /interfaces/          
Version                                 : 1.0                  
Sensor-id                               : 3139262809            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : mib2d                 

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1000_6_1       
Resource                                : /interfaces/          
Version                                 : 1.0                  
Sensor-id                               : 3139260761            
Subscription-ID                         : 1000                 
Parent-Sensor-Name                      : sensor_1000          
Component(s)                            : xmlproxyd             

Profile Information : 

Name                                : export_1000           
Reporting-interval                  : 2                     
Payload-size                        : 5000                  
Format                              : GPB                   

Sensor Information : 

Name                                    : sensor_1001           
Resource                                : /junos/system/linecard/cpu/memory/ 
Version                                 : 1.0                  
Sensor-id                               : 539528114             
Subscription-ID                         : 1001                 
Parent-Sensor-Name                      : Not applicable       
Component(s)                            : PFE                   

Profile Information : 

Name                                : export_1001           
Reporting-interval                  : 1                     
Payload-size                        : 5000                  
Format                              : GPB                   

==> at PFE (login from MX Shell: vty fpcX)

VMX-0(10.49.167.137 vty)# show agent sensors    

Jvision ID  Name
----------  --------------------------------
539528114  sensor_1001           5000(1109)
2277069355  __default_fabric_sensor__  5000(93)
3139259737  sensor_1000_1_1       5000(351)
3139259738  sensor_1000_1_2       5000(1035)
3139259739  sensor_1000_1_3       5000(608)

Total number of jvision SENSORs = 5

Non-JV  ID  Name
----------  --------------------------------

Total number of non-jvision SENSORs = 0


VMX-0(10.49.167.137 vty)# show agent sensors id 3139259739
ID: 3139259739 Type: 1 Name: (sensor_1000_1_3)
Sensor Data: 637(609) bytes
Jvision Header: system: 10.49.167.137, slot: 0, time: Jun 19 01:13:06.173, sequence_number: 223, sensor_name: sensor_1000_1_3:/junos/system/linecard/interface/traffic/:/interfaces/:PFE, version: 1.0
Interface = ge-0/0/0 (527) Parent = ae2
Init time = Jun 17 13:52:34


In Packets = 114497535 (1001 pkts/sec) Bytes = 11557091307 (102221 bytes/sec)
UPackets = 114494274  MPackets = 0 BPackets = 0
RX Error Packets = 0
In Pause Packets = 0
Out Packets = 51875003 (500 pkts/sec) Bytes = 5809902074 (56026 bytes/sec)
UPackets = 51998447  MPackets = 0 BPackets = 0
TX Error Packets = 0
Out Pause Packets = 0
if_oprtn_status = UP 
Carrier Transitions Packets = 1
Last Change = 0 ms from time_get_ms
High Speed = 1000 Mbps
In errors = 0
Qdrop errors = 0
Framing errors = 0
In Discard = 0
Runts = 0
L3 incomplete errors = 0
L2 channel errors = 0
L2 mismatch errors = 0
FIFO errors = 0
Resource errors = 0
Out errors = 0
Out Discard = 0
Interface = ge-0/0/1 (528) Parent = ae1
Init time = Jun 17 13:52:34


In Packets = 2532994 (1 pkts/sec) Bytes = 252504475 (157 bytes/sec)
UPackets = 2532989  MPackets = 0 BPackets = 0
RX Error Packets = 0
In Pause Packets = 0
Out Packets = 51857673 (500 pkts/sec) Bytes = 4771162071 (46071 bytes/sec)
UPackets = 51981113  MPackets = 0 BPackets = 0
TX Error Packets = 0
Out Pause Packets = 0
if_oprtn_status = UP 
Carrier Transitions Packets = 1
Last Change = 0 ms from time_get_ms
High Speed = 1000 Mbps
In errors = 0
Qdrop errors = 0
Framing errors = 0
In Discard = 0
Runts = 0
L3 incomplete errors = 0
L2 channel errors = 0
L2 mismatch errors = 0
FIFO errors = 0
Resource errors = 0
Out errors = 0
Out Discard = 0
Interface = ge-0/0/2 (529) 
Init time = Jun 17 13:52:34


In Packets = 103701664 (1000 pkts/sec) Bytes = 10577338715 (102048 bytes/sec)
UPackets = 103698408  MPackets = 0 BPackets = 0
RX Error Packets = 0
In Pause Packets = 0
Out Packets = 116751438 (1000 pkts/sec) Bytes = 11776948640 (102102 bytes/sec)
UPackets = 116748180  MPackets = 0 BPackets = 0
TX Error Packets = 0
Out Pause Packets = 0
if_oprtn_status = UP 
Carrier Transitions Packets = 1
Last Change = 0 ms from time_get_ms
High Speed = 1000 Mbps
In errors = 0
Qdrop errors = 0
Framing errors = 0
In Discard = 0
Runts = 0
L3 incomplete errors = 0
L2 channel errors = 0
L2 mismatch errors = 0
FIFO errors = 0
Resource errors = 0
Out errors = 0
Out Discard = 0
Interface = ge-0/0/3 (530) 
Init time = Jun 17 13:52:34


In Packets = 0 (0 pkts/sec) Bytes = 0 (0 bytes/sec)
UPackets = 99  MPackets = 0 BPackets = 0
RX Error Packets = 0
In Pause Packets = 0
Out Packets = 0 (0 pkts/sec) Bytes = 0 (0 bytes/sec)
UPackets = 0  MPackets = 0 BPackets = 0
TX Error Packets = 0
Out Pause Packets = 0
if_oprtn_status = UP 
Carrier Transitions Packets = 1
Last Change = 0 ms from time_get_ms
High Speed = 1000 Mbps
In errors = 0
Qdrop errors = 0
Framing errors = 0
In Discard = 0
Runts = 0
L3 incomplete errors = 0
L2 channel errors = 0
L2 mismatch errors = 0
FIFO errors = 0
Resource errors = 0
Out errors = 0
Out Discard = 0
Export: Interval = 2000 msecs, Payload-size = 5000 bytes, Server = Src: 0.0.0.0:1000, Dst: none, Qos = TOS:0x0, Hint:0x40000010, FC:0 PLP:0
Filter: none
Accounting:
       224 total successful reaps, 0 failed/aborted reap(s).
	 1 reaps in latest reporting interval.
	 1 packets in latest reporting interval.
	 4 instances in latest reporting interval.
       224 total packets sent.
       224 wraps, 1 reap(s) on average to wrap.
Last 10 wraps (UTC):
	2020 Jun 19 01:13:06:173
	2020 Jun 19 01:13:04:163
	2020 Jun 19 01:13:01:309
	2020 Jun 19 01:12:59:304
	2020 Jun 19 01:12:57:300
	2020 Jun 19 01:12:55:393
	2020 Jun 19 01:12:53:389
	2020 Jun 19 01:12:51:385
	2020 Jun 19 01:12:48:313
	2020 Jun 19 01:12:46:304
---------------------------

```

