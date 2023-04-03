## 에러 메시지 

> DBMS: MySQL (no ver.) Case sensitivity: plain=mixed, delimited=exact [08S01] 
Communications link failure The last packet sent successfully to the server was 0 milliseconds ago. 
The driver has not received any packets from the server. 
No appropriate protocol (protocol is disabled or cipher suites are inappropriate).

<br/>

## 원인

- 적절하지 않은 드라이버 사용

<br/>

## 해결

- 적절한 드라이버로 변경 (ex: MySQL Driver -> Aurora Driver)

<img width="553" alt="image" src="https://user-images.githubusercontent.com/53105735/229513465-4535c2a7-efa0-41b5-8fe5-7a71afc28c61.png">

<br/>

## 참고

- https://youtrack.jetbrains.com/issue/DBE-13313/Cant-connect-to-remote-MySQL-since-last-version-of-IntelliJ#focus=Comments-27-4921748.0-0
