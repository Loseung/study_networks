### **🧪 문제 1: 특정 IP 차단 상태 확인 후 차단 설정**

#### **✅ 실행 예시**

$ sudo ./[problem1.sh](http://problem1.sh) )

\[INFO\] 현재 rich rule 목록에 192.168.0.100 차단 룰이 존재하지 않습니다.

\[INFO\] 차단 룰을 추가합니다...

success

또는

$ sudo ./[problem1.sh](http://problem1.sh) 192.168.0.100

\[INFO\] 192.168.0.100은 이미 차단되어 있습니다.

\[SKIP\] 추가 작업을 수행하지 않습니다.
```shell
#vim
#!/bin/bash

usr_ip="192.168.0.36"

if [ -z "$(sudo firewall-cmd --list-rich-rules | grep "$usr_ip")" ]; then
        echo "[INFO] 현재 rich rule 목록에 "$usr_ip" 차단 룰이 존재하지 않습니다."
        echo "[INFO] 차단 룰을 추가합니다..."
        sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address='$usr_ip' reject'
        sudo firewall-cmd --reload
else
        echo "[INFO] 현재 rich rule 목록에 "$usr_ip" 차단 룰이 존재합니다."
fi
```

```shell
#실행
[hoseung@192.168.0.37 ~/quests]$ sudo bash problem1.sh 
[INFO] 현재 rich rule 목록에 192.168.0.36 차단 룰이 존재하지 않습니다.
[INFO] 차단 룰을 추가합니다...
success
success

#룰이 있을 경우
[hoseung@192.168.0.37 ~/quests]$ sudo bash problem1.sh 
[INFO] 현재 rich rule 목록에 192.168.0.36 차단 룰이 존재합니다.
```
---

### **🔒 문제 2: 포트 8080이 열려 있다면 닫기**

#### **✅ 실행 예시**

$ sudo ./[problem2.sh](http://problem2.sh) 8080/tcp

\[INFO\] 포트 8080/tcp 이 열려 있습니다. 제거합니다...

success

또는

$ sudo ./[problem2.sh](http://problem2.sh) 8080/tcp

\[INFO\] 포트 8080/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다.

```shell
[hoseung@192.168.0.37 ~/quests]$ sudo bash problem2.sh
[INFO] 포트 8080/tcp 이 열려 있습니다. 제거합니다...
success
success
[hoseung@192.168.0.37 ~/quests]$ sudo bash problem2.sh
[INFO] 포트 8080/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다.

```

```shell
#!/bin/bash

port="8080"
#[hoseung@192.168.0.37 ~]$ sudo firewall-cmd --permanent --remove-port=8000/tcp

if [ -z "$(sudo firewall-cmd --list-ports | grep "$port")" ]; then
        echo "[INFO] 포트 8080/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다."
else
        echo "[INFO] 포트 8080/tcp 이 열려 있습니다. 제거합니다..."
        sudo firewall-cmd --permanent --remove-port="$port"/tcp
        sudo firewall-cmd --reload
fi

```

---

### **🧩 문제 3: SSH 서비스 제거 후 특정 IP만 허용**####하지않기

#### **✅ 실행 예시**

$ sudo ./[problem3.sh](http://problem3.sh) 22/?-\> 찾기

\[INFO\] SSH 서비스가 열려 있습니다. 제거합니다...

success

\[INFO\] 192.168.0.10 IP에만 포트 22 허용 규칙을 추가합니다...

success

또는

$ sudo ./[problem3.sh](http://problem3.sh) 22/?-\> 찾기

\[INFO\] SSH 서비스가 이미 제거되어 있습니다.

\[INFO\] 포트 22 허용 규칙만 추가합니다...

success

---

