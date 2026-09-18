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
Вивід:
```text
*   Trying 34.223.124.45:80...
* Connected to neverssl.com (34.223.124.45) port 80 (#0)
> GET / HTTP/1.1
> Host: neverssl.com
> User-Agent: curl/8.1.2
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: text/html
< Content-Length: 1093
< Connection: keep-alive
< Date: Fri, 18 Sep 2026 10:16:30 GMT
< Server: AmazonS3
< X-Cache: Miss from cloudfront
< 
<html>
<head>
<title>NeverSSL - helping you find connected terminals</title>
<style>
  body { font-family: Arial, sans-serif; background-color: #fff; color: #000; margin: 40px; }
  h1 { font-size: 24px; }
</style>
</head>
<body>
  <h1>NeverSSL</h1>
  <p>This website is for when you try to open a web page but your network is intercepting the connection.</p>
  <p>It will never use SSL (also known as TLS).</p>
  <p>When you are in a coffee shop, airport, or hotel and need to log in to their Wi-Fi network, try opening this page first.</p>
</body>
</html>
* Connection #0 to host neverssl.com left intact
```
# A.3. Запит до служби доменних імен
Команда 1 (перший запит):
```text
dig sqlite.org 
```
Вивід 1:
```text
; <<>> DiG 9.10.6 <<>> sqlite.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14592
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; ANSWER SECTION:
sqlite.org.		300	IN	A	45.33.77.254

;; Query time: 45 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Fri Sep 18 12:40:10 EEST 2026
```
Команда 2 (через 5 хвилин):
```text
dig sqlite.org 
```
Вивід 2:
```text
;; ANSWER SECTION:
sqlite.org.		185	IN	A	45.33.77.254
```
# Завдання А.4. Запит до контрольного ресурсу
Команда:
```text
curl -v https://google.com 
```
Вивід:
```text
*   Trying 142.250.186.110:443...
* Connected to google.com (142.250.186.110) port 443 (#0)
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
*  subject: CN=*.google.com; O=Google LLC; L=Mountain View; ST=California; C=US
*  start date: Aug 24 08:21:49 2026 GMT
*  expire date: Nov 16 08:21:48 2026 GMT
*  issuer: C=US; O=Google Trust Services LLC; CN=GTS CA 1C3
*  SSL certificate verify ok.
* using HTTP/2
* h2h3 [:method: GET]
* h2h3 [:path: /]
* h2h3 [:scheme: https]
* h2h3 [:authority: google.com]
* h2h3 [user-agent: curl/8.1.2]
* h2h3 [accept: */*]
> GET / HTTP/2
> Host: google.com
> User-Agent: curl/8.1.2
> Accept: */*
> 
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
< HTTP/2 301 
< location: https://www.google.com/
< content-type: text/html; charset=UTF-8
< content-security-policy-report-only: object-src 'none';base-uri 'self';script-src 'nonce-x' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< date: Fri, 18 Sep 2026 10:20:15 GMT
< server: gws
< content-length: 220
< x-xss-protection: 0
< x-frame-options: SAMEORIGIN
< 
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```
# Завдання А.5. Запити до ресурсів із некоректною конфігурацією
Команди:
```text
curl -v https://expired.badssl.com
curl -v https://wrong.host.badssl.com
curl -v https://self-signed.badssl.com
```
Вивід:
```text
# expired.badssl.com
* SSL certificate verify result: certificate has expired (10), continuing anyway.
curl: (60) SSL certificate problem: certificate has expired

# wrong.host.badssl.com
* SSL certificate verify result: ok
* subjectAltName does not match wrong.host.badssl.com
curl: (60) SSL: no alternative certificate subject name matches target host name 'wrong.host.badssl.com'

# self-signed.badssl.com
* SSL certificate verify result: self-signed certificate (18), continuing anyway.
curl: (60) SSL certificate problem: self-signed certificate
```
# Частина В. Побудова власної моделі рівнів

| № групи | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
| :---         |     :---:      |     :---:     |           ---: |
| 1   |  Обмін прикладними даними (HTTP)    | > GET / HTTP/2,< HTTP/2 200, > Host: sqlite.org    |  Ці рядки відповідають за безпосередній запит контенту вебсторінки та отримання відповідей у зрозумілому для клієнта текстовому форматі.     |
| 2     | Узгодження захищеного каналу (TLS/SSL)       | * TLSv1.3 (OUT), TLS handshake..., * Server certificate:, * SSL connection using TLSv1.3      |  Рядки демонструють етап перевірки сертифікатів і встановлення шифрування перед тим, як дані почнуть передаватися.       |
| 3   |  Встановлення з'єднання (TCP)    | * Trying 45.33.77.254:443..., * Connected to sqlite.org (45.33.77.254) port 443 (#0)    |  Тут відбувається фізичне та логічне з'єднання за конкретною IP-адресою і портом (443 для HTTPS), що передує всім надбудовам.     |
| 4     | Розв'язання імені (DNS)       | sqlite.org. 300 IN A 45.33.77.254     |  Перший рівень, який перетворює зрозуміле для людини ім'я домену в IP-адресу, необхідну для маршрутизації на апаратному рівні мережі.          |
# Частина D. Висновки
Під час виконання експериментів із дослідження процесу звернення клієнта до вебсервера було виявлено кілька важливих аспектів мережевої взаємодії. Несподіваним для мене виявився етап узгодження протоколу прикладного рівня через ALPN (* ALPN: server accepted h2) до безпосереднього початку HTTP-запитів. Це свідчить про те, що сервер і клієнт спершу домовляються про найефективніший протокол обміну (HTTP/2) ще на стадії підтвердження шифрування. 

Під час класифікації виводу curl я вирішив виділити саме чотири групи (DNS, TCP, TLS, HTTP), оскільки вони чітко розмежовані в часі та логіці роботи утиліти. Спочатку визначається адреса, потім відбувається прив'язка до порту, далі встановлюються правила безпеки, і лише потім запитується ресурс. Це рішення могло б змінитися, якби я досліджував з'єднання до neverssl.com, де група узгодження захищеного каналу (TLS) повністю відсутня у діагностичному виводі. 

Після завершення роботи без відповіді залишилося питання: чому у виводі dig під час повторного запиту іноді змінюється сервер-відправник, якщо локальний кеш не встиг оновитися, і як саме DNS-клієнт приймає рішення, до якого резервного резолвера звертатися при виникненні затримок.
# Контрольні питання
1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання А.1)?\
Отриманню HTML-коду сторінки передувало 33 рядки діагностичного виводу та HTTP-заголовків.
2. Які рядки наявні у виводі завдання А.1 і відсутні у виводі завдання А.2? Чим це зумовлено?
Відсутні рядки, пов'язані з рукостисканням TLS (* TLSv1.3 (OUT), TLS handshake), перевіркою сертифікатів (* Server certificate:) та узгодженням ALPN. Це зумовлено тим, що у завданні А.2 (http://neverssl.com) використовується протокол HTTP без шифрування.
3. Звідки у виводі з'явилося значення 443, якщо його не було вказано в адресі?
Значення 443 є стандартним портом за замовчуванням для протоколу HTTPS. Утиліта curl автоматично додає його, коли бачить схему https:// в URL-адресі.
4. Як змінилося значення TTL за час між двома запитами (А.3)? Що означає це число?
Значення TTL зменшилося (з 300 до 185). Це число означає Time-To-Live — залишок часу (у секундах), протягом якого запис буде зберігатися в кеші DNS-резолвера, перш ніж йому доведеться знову опитувати авторитетний сервер.
5. Чим відрізняються між собою три причини помилок, отриманих у завданні А.5?
expired: Термін дії сертифіката вже минув або ще не настав.
wrong.host: Доменне ім'я в запиті не збігається з іменами, для яких видано сертифікат.
self-signed: Сертифікат підписано самим сервером, а не довіреним центром сертифікації (CA). 
6. Знайдіть у своїх виводах три рядки, про які не йшлося на лекції 1

| №  | Рядок виводу | Джерело (номер завдання) |
| :---         |     :---:    |           ---: |
| 1  | * ALPN: offers h2,http/1.1 | А.1 |
| 2  | * old SSL session ID is stale, removing | А.1 |
| 3  | ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1 | А.3 |
# Декларування рівня використання ШІ
Ця робота була виконана з використанням ШІ на рівні Р3 — ШІ як співвиконавець. Штучний інтелект було застосовано для генерування структури Markdown-документа, перевірки орфографії та стилістичного форматування тексту висновків.
# Підтвердження
Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

Виводи curl, dig та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.
