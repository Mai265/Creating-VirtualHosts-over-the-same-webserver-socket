# Creating Virtual Hosts over the same webserver socket
Steps to implement two virtual hosts in  the same webserver socket
## 1.Install HTTP service
```
[x@server ~]# sudo yum install http -y
```
## 2.Enable and start HTTP service
```
[x@server ~]# sudo systemctl enable --now httpd
```
## 3.Check HTTP service status
```
[x@server ~]# systemctl status httpd
```
## 4. Check service socket 
```
[x@server ~]# ss -ltn
```
## 5. Add service to firewall 
```
[x@server ~]# sudo firewall-cmd --add-service=http --permanent
```
## 6. Make sure that HTTP service is added
```
[x@server ~]# sudo firewall-cmd --list-services 
```
## 7. Copy the attached configuration and data files to its' path as shown:
- To configure the 1st virtual host copy `ahmed.com.conf` under `/etc/httpd/conf.d` 
- To configure the 2nd virtual host copy `mai.com.conf` under `/etc/httpd/conf.d`
- Edit `/var/www/ahmed.com` , `/var/www/ahmed.com` directories to contain the website bages. file `index.html` contain the main bage html code.

 ## 8. Restart HTTP service to read the configuration 
 ```
[x@server ~]# sudo systemctl restart httpd

```
 ## 9. Add the servers names to host files at clients 
 - In linux  clients open `/etc/hosts` and add lines:
 
    > 192.168.x.x       &emsp;&emsp;&emsp;      ahmed.com
    > 
    > 192.168.x.x       &emsp;&emsp;&emsp;      mai.com
    
 - In windows clients open `C:\Windows\System32\drivers\etc\hosts` and add the same 2 lines.
 # 10. Test the connection via
 ```
[x@server ~]# sudo systemctl restart httpd

```
[x@server ~]# curl mai.com
```
Output > Welcom to mai.com

```
[x@server ~]# curl ahmed.com
```
Output > Welcom to Ahmed.com
