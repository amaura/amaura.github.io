---
layout: post
title: SCAN connection troubleshooting
---

During my working days I see a lot of customers facing problems when using SCAN to connect to their Oracle Database.

First of all I think that all Oracle DBA nowadays should know how SCAN work. The entry point is this very complete white paper : [Oracle SCAN Explained](http://www.oracle.com/technetwork/products/clustering/overview/scan-129069.pdf)

Basically when an Oracle client connects to a SCAN (provided that you use a >11gr2 client), eg. myscan.db.com: 

- The client makes a DNS request to resovle the 3 SCAN addresses
- The client uses this list of 3 address to access in a round robin way the listeners
- When connected to a SCAN listener it will asks for the service contained in the SERVICE_NAME clause of your tnsnames.ora
- It will then be redirected to a local listener
- It will connect to a local listener usually an a cluster VIP

Thus, the requirements are :
- The client should resolve the 3 IPs, so on the client machine type :
```
nslookup myscan.db.com
```
