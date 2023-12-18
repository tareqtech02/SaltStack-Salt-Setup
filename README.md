# SaltStack or Salt Setup  
  
<br />  
## Salt Master  
___
Update System
```
yum update -y
```

Install Salt Master
```
yum install salt-master -y
```

Enable and Start the Salt Master Service
```
systemctl enable salt-master
systemctl start salt-master
```

Verify Salt Master Status
```
systemctl status salt-master
```

Disable and Stop the Service Firewall Configuration
```
systemctl disable firewalld
```
  
## Salt Minions  
<br />  
Update System
```
yum update -y
```

Add the repolist for Salt Minions
```
sudo rpm --import https://repo.saltproject.io/salt/py3/redhat/9/x86_64/3005/SALTSTACK-GPG-KEY2.pub
curl -fsSL https://repo.saltproject.io/salt/py3/redhat/9/x86_64/3005.repo | sudo tee /etc/yum.repos.d/salt.repo
```

Verify the repolist
```
yum repolist
```

Install Salt Minion
```
yum install salt-minion -y
```

Enable and Start the Salt Minion Service
```
systemctl enable salt-minion
systemctl start salt-minion
```

Configure Salt Minion and Connecting to the Salt master
```
vim /etc/salt/minion.d/master.conf
master: 192.168.1.142
```

Declaring the minion ID
```
vim /etc/salt/minion.d/id.conf
id: minion-dev-web-01
```

Restart and Verify Salt Minion Status
```
systemctl restart salt-minion
```

Verify Salt Minion Status
```
systemctl status salt-minion
```

Disable and Stop the Service Firewall Configuration
```
systemctl disable firewalld
```
  
Accepting keys  
```
salt-key -L  # Lists all minion IDs
salt-key -A  # Accepts All Keys 
salt-key -a web01  # Accept specific key
```
  
Deleting keys  
```
salt-key -D  # Deleting all keys
salt-key -d dba01  # remove an specific key
```

Display the versions of SaltStack components
```
salt-run manage.versions
```
  
## Testing  
<br />  
salt '*' test.ping
```
