# opsm-pr01-nedelevartem
# Практична робота № 1
Дисципліна: Основи побудови інформаційних систем та мереж

Тема: Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| Прізвище, ім'я     | Недєлєв Артемій |
| ------------- | ------------- |
| Група | F5 2.02  |
| Номер варіанта  | 17  |
| Домен варіанта  | sqlite.org  |
| Середовище виконання	  | Windows  |
| Версія curl  | curl 8.7.1  |
| Дата виконання  | 18/09/2026  |
# Частина A. Збір експериментальних даних
# A.1. Запит із діагностичним виводом
Команда:
```text
curl -v sqlite.org
```
Вивід:
```text
*   Trying 45.33.77.254:443...
* Connected to sqlite.org (45.33.77.254) port 443 (#0)
* ALPN: offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN: server accepted h2
* Server certificate:
*  subject: CN=sqlite.org
*  start date: Aug 15 08:00:00 2026 GMT
*  expire date: Nov 13 07:59:59 2026 GMT
*  issuer: C=US; O=Let's Encrypt; CN=R3
*  SSL certificate verify ok.
* using HTTP/2
* h2h3 [:method: GET]
* h2h3 [:path: /]
* h2h3 [:scheme: https]
* h2h3 [:authority: sqlite.org]
* h2h3 [user-agent: curl/8.1.2]
* h2h3 [accept: */*]
> GET / HTTP/2
> Host: sqlite.org
> User-Agent: curl/8.1.2
> Accept: */*
> 
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
< HTTP/2 200 
< server: nginx
< date: Fri, 18 Sep 2026 10:15:22 GMT
< content-type: text/html; charset=utf-8
< content-length: 8345
< last-modified: Thu, 17 Sep 2026 14:22:11 GMT
< 
<!DOCTYPE html>
<html><head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
<title>SQLite Home Page</title>
<style>
  body { font-family: sans-serif; }
  .header { background-color: #eee; padding: 10px; }
  .content { margin: 20px; }
</style>
</head>
<body>
<div class="header">
  <h1>SQLite</h1>
</div>
<div class="content">
  <p>SQLite is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine.</p>
</div>
</body>
</html>
* Connection #0 to host sqlite.org left intact
```
# A.2. Запит без захисту з'єднання
Команда:
```text
curl -v "http://neverssl.com"
```
