# Cookie Arena Season 1 - Capture The Flag (CTF)

### Overview
 | Title | Category | Points | Flag
 | ------ | ------ | ------ | ------ |
 | [Discord](#Discord) | Misc | 1 | `Flag{Cookie_Han_Hoan}` |
 | [Hân Hoan](#Hân-Hoan) | Web Basic | 1 | `Flag{Cookies_Yummy_Cookies_Yammy!}` |
 | [JS Bp Bp](#JS-Bp-Bp) | Web Basic | 1 | `Flag{JAV-ascript_F*ck}` |
 | [Impossible](#Impossible) | Web Basic | 1 | `Flag{Javascript_is_not_safe???}` |
 | [Infinite Loop](#Infinite-Loop) | Web Basic | 1 | `Flag{Y0u_c4ptur3_m3_xD!!!}` |
 | [I am not a robot](#I-am-not-a-robot) | Web Basic | 1 | `Flag{N0_B0T_@ll0w}` |
 | [Sause](#Sause) | Web Basic | 1 | `Flag{Web_Sause_Delicious}` |
 | [Header 401](#Header-401) | Web Basic | 1 | `Flag{m4g1c@l_h34d3r_xD}` |
 | [Ét Quy Eo](#Ét-Quy-Eo) | Web Exploitation | 1 | `Flag{Fr33_Styl3}` |
 | [SQL Filter](#SQL-Filter) | Web Exploitation | 1 | `Flag{Gr33t1nG}` |
 | [The maze runner](#The-maze-runner) | Web Exploitation | 1 | `FLAG{6059e2117ea3eeecdad7faf1e15d16a2}` |
 | [Misconfiguration](#Misconfiguration) | Web Exploitation | 1 | `Flag{1b283f0725d536a0f217d89caca7b183}` |
 | [Gatling gun](#Gatling-gun) | Web Exploitation | 1 | `FLAG{e6c068faf9241fe9d1f2000516718377}` |
 | [SUM](#SUM) | Programming | 1 | `Flag{1plust1_1s_2_qu1ck_mafth}` |
 | [Pro102](#Pro102) | Programming | 1 | `Flag{2fast2fur10us}` |
 | [Roberval](#Roberval) | Programming | 1 | `Flag{n0_pr0b_w1th_cub3_r00t_RIGHT?}` |
 | [Where is my house](#Where-is-my-house) | Network | 1 | `Flag{DNS_A_AAAA_TXT_CNAME}` |
 | [Scan me if you can](#Scan-me-if-you-can) | Network | 1 | `Flag{Every-Header-Have-It-Own-Meaning}` |
 | [Very Good Shipper](#Very-Good-Shipper) | Network | 1 | `Flag{t00-ez-4-y0u}` |
 | [Post Office Man](#Post-Office-Man) | Network | 1 | `Flag{1-Ha\/3-1o0o-UnS33n-3Ma1L}` |
 | [Secure HTTP](#Secure-HTTP) | Network | 1 | `Flag{This-Is-A-Trusted-One}` |
 | [XOR](#XOR) | Cryptography | 1 | `Flag{a^b=c=>b^c=a}` |
 | [Morse](#Morse) | Cryptography | 1 | `Flag{M.O.R.S.E.C.O.D.E}` |
 | [Julius Caesar](#Julius-Caesar) | Cryptography | 1 | `Flag{El_Clasico_Cipher}` |
 | [Sixty Four](#Sixty-Four) | Cryptography | 1 | `Flag{___Base64xHex___}` |
 | [Basic Image](#Basic-Image) | Forensic | 1 | `Flag{metadataratatatataaaaaa}` |
 | [ExSeller](#ExSeller) | Forensic | 1 | `Flag{Micro$oft_Heck3r_Man}` |
 | [Streamer](#Streamer) | Forensic | 1 | `Flag{TCP_streamin_go_skrrrrrrrt}` |
 | [Interceptor](#Interceptor) | Forensic | 1 | `Flag{1s_th1s_m1sc3llan30us?}` |
 | [AudiCaty](#AudiCaty) | Forensic | 1 | `Flag{No_Bullets_for_Player_001}` 
 | [Volatility](#Volatility) | Forensic | 1 | `Flag{7ef31e58bd4086e294b4d700c721f35f}` |
 
# Hân Hoan
 
### Challenge
 
<img src=temp/1.png>
 
### Solution

* Truy cập trang ta có 1 form submit.

<img src=temp/2.png>

* Submit thử và quan sát cookie (do bài có đề cập 'bánh quy').

<img src=temp/3.png>

* Submit lại với username là `CookieHanHoan` và sửa cookie Role thành `CookieHanHoan`. Ta có được cờ.

<img src=temp/4.png>

# JS Bp Bp
 
### Challenge
 
<img src=temp/5.png>
 
### Solution

* Truy cập trang ta có 1 form submit.

<img src=temp/6.png>

* Đề bài đề cập đến js vậy mở js lên xem thì có 4 file js. Các file đều đã được mã hóa.

<img src=temp/7.png>

<img src=temp/8.png>

* Nhìn vào thì nhận ra ngay đây là JSFuck. Decode từng file rồi đọc.

```
function verifyUsername(username) {     if (username != "cookiehanhoan") {       return false     }     return true   }
```

* 1.js cho ta username là `cookiehanhoan`

```
function reverseString(str) {   if (str === "")    { return "" }   else {   return reverseString(str.substr(1)) + str.charAt(0)}   }
```

* 2.js là 1 hàm đảo ngược chuỗi

```
function verifyPassword(password) {     if (reverseString(password) != "dr0Wss@p3rucreSr3pus") {       return false     }     return true   }
```

* 3.js cho ta password là `dr0Wss@p3rucreSr3pus` tuy nhiên cần đảo ngược lại thành `sup3rSercur3p@ssW0rd`

```
function verifyRole(role) {       if (role.charCodeAt(0) != 64) {         return false;       }       if ((role.charCodeAt(1) + role.charCodeAt(2) != 209) && (role.charCodeAt(2) - role.charCodeAt(1) != 9)) {         return false       }       if ((role.charCodeAt(3).toString() + role.charCodeAt(4).toString() != "10578") && (role.charCodeAt(3) - role.charCodeAt(4) != 27)) {         return false       }     return true   }
```

* charCodeAt gồm 0 đến 4 vậy role có 5 ký tự. Lần lượt tra bảng ascii để giải quyết.
* `role.charCodeAt(0) != 64` > ký tự đầu là `@`.
* `role.charCodeAt(1) + role.charCodeAt(2) != 209` và `role.charCodeAt(2) - role.charCodeAt(1) != 9` > giải hệ pt 2 ẩn hoặc tùy bạn, ta được 2 ký tự tiếp theo là `d` và `m`.
* `role.charCodeAt(3).toString() + role.charCodeAt(4).toString() != "10578"` > đến đây thì đoán đc rồi, role là `admin`. 105 là `i` và 78 là `N`.
* Vậy role cuối cùng là `@dmiN`

<img src=temp/9.png>

# Impossible
 
### Challenge
 
<img src=temp/a.png>
 
### Solution

* Viewsource ta được đoạn code sau.

```js
function checkPass()
{
	var password = document.getElementById('password').value;
	if (btoa(password.replace("cookiehanhoan", "")) == "Y29va2llaGFuaG9hbg==") {
		window.setTimeout(function() {
			window.location.assign('check.php?password=' + password);
		}, 500);
	}
}
```

* Decode base64 `Y29va2llaGFuaG9hbg==` ta được `cookiehanhoan`. Vậy password nhập `cookiehanhoan` là được, tuy nhiên bị hàm replace bỏ đi.
* Vậy đơn giản là ta nhập password như sau: `cookiecookiehanhoanhanhoan` (vì hàm replace chỉ thực hiện 1 lần)

<img src=temp/b.png>

# Infinite Loop
 
### Challenge
 
<img src=temp/c.png>
 
### Solution

* Truy cập trang ta được 1 form submit.

<img src=temp/d.png>

* Lúc submit thì thấy nó load khá lâu.
* Đề bài đề cập đến vòng lặp và công cụ mạnh mẽ vậy chắc nói đến Burp Suite rồi.
* Dùng Burp Suite và submit thì thấy trang liên tục chuyển hướng. Làm 1 hồi ta có được cờ.

<img src=temp/e.png>

# I am not a robot
 
### Challenge
 
<img src=temp/f.png>
 
### Solution

* Bài này cơ bản. Mở file robots.txt và đọc thôi.

<img src=temp/10.png>

<img src=temp/11.png>

# Sause
 
### Challenge
 
<img src=temp/12.png>
 
### Solution

* Bài này cơ bản. Mở source và đọc thôi.

<img src=temp/13.png>

# Header 401
 
### Challenge
 
<img src=temp/14.png>
 
### Solution

* Đề bài đề cập đến HTTP Protocol. Vậy đổi GET thành POST ta được gì (sử dụng Burp Suite).

<img src=temp/15.png>

* `Missing Basic Authorization Header`. OK, nếu view source ta cũng nhận được thông tin là `Basic Authentication Credential: gaconlonton/cookiehanhoan`.

<img src=temp/16.png>

* Vậy ta còn thiếu header cho phần xác thực.
* Các bạn có thể đọc thêm ở đây https://en.wikipedia.org/wiki/Basic_access_authentication

<img src=temp/17.png>

* Vậy ta cần bổ sung thêm vào header như sau: `Authorization: Basic Z2Fjb25sb250b246Y29va2llaGFuaG9hbg==` với `Authorization: Basic Z2Fjb25sb250b246Y29va2llaGFuaG9hbg==` là base64 của `gaconlonton:cookiehanhoan`

<img src=temp/18.png>

# SUM
 
### Challenge
 
<img src=temp/19.png>

```
# nc programming.letspentest.org 8111
Number list: 
14254 77252 90039 72763 21060 72080 63176 27633 80700 12487
Calculate the equation of this numbers:
```
 
### Solution

* Bài này yêu cầu viết một chương trình socket để giao tiếp với server. Đồng thời yêu cầu thực hiện tính tổng các số mà server đưa ra.
* Server sẽ đưa ra 1 dãy các số như sau: `14254 77252 90039 72763 21060 72080 63176 27633 80700 12487`
* ý tưởng của mình là replace khoảng trắng (' ') thành dấu cộng ('+') sử dụng: `banner.replace(' ', '+')`
* Sau đó chỉ cần dùng hàm `eval` là tính được tổng: `eval(banner[:-1])` (ở đây mình bỏ dấu + cuối)
* Chương trình mình giải quyết bài này như sau (bạn đọc có thể tham khảo)

```python
#!/usr/bin/python3
import socket

IP, PORT = ('programming.letspentest.org', 8111)

def receive_all_line(s):
    data = s.recv(999999)
    return data.decode()

def receive_one_line(s):
    r = b''
    while (True):
        t = s.recv(1)
        if t == b'\n': break
        r = r + t
    return r.decode()

def send_one_line(s, data):
    s.sendall(f"{data}\n".encode())

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((IP, PORT))
    
    while True:
        banner = receive_one_line(s)
        print(banner)
        while 'Number list:' not in banner:
            if 'Flag{' in banner: exit()
            banner = receive_one_line(s)
            print(banner)
        banner = receive_one_line(s)
        print(banner)
        banner = banner.replace(' ', '+')
        answer = eval(banner[:-1])
        print(answer)
        send_one_line(s, answer)

    s.close()

if __name__ == '__main__':
    main()

```

<img src=temp/1a.png>

# Pro102
 
### Challenge
 
<img src=temp/27.png>

```
# nc programming.letspentest.org 8222
Equation: 
1*X^2 - 594*X - 54675 = 0
Calculate the roots of this equation:
```
 
### Solution

* Bài này yêu cầu viết một chương trình socket để giao tiếp với server. Đồng thời yêu cầu giải phương trình bậc 2 mà server đưa ra.
* Server sẽ đưa ra pt bậc 2 như sau (mẫu): `1*X^2 - 594*X - 54675 = 0`
* Pt có 2 ngiệm, khi gửi phải ghi từ nhỏ đến lớn: `-81, 675`
* Mình giải quyết bằng cách đọc vào chuỗi `banner[:-5]` chỉ lấy `1*X^2 - 594*X - 54675`
* Sau đó dùng package sympy hỗ trợ giải pt bậc 2 vô cùng tiện lợi: `solve(banner[:-5], x)`
* Kết quả trả về 1 list: `[-81, 675]`
* Ta chỉ cần chuyển từ list về string và gửi đi.
* Chương trình tham khảo như sau.

```python
#!/usr/bin/python3
import socket
from sympy.solvers import solve
from sympy import Symbol

IP, PORT = ('programming.letspentest.org', 8222)

def receive_all_line(s):
    data = s.recv(999999)
    return data.decode()

def receive_one_line(s):
    r = b''
    while (True):
        t = s.recv(1)
        if t == b'\n': break
        r = r + t
    return r.decode()

def send_one_line(s, data):
    s.sendall(f"{data}\n".encode())

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((IP, PORT))
    
    while True:
        banner = receive_one_line(s)
        print(banner)
        while 'Equation:' not in banner:
            if 'Flag{' in banner: exit()
            banner = receive_one_line(s)
            print(banner)
        banner = receive_one_line(s)
        print(banner)
        x = Symbol('X')
        arr = solve(banner[:-5], x)
        ans = ', '.join([str(i) for i in arr])
        print(ans)
        send_one_line(s, ans)

    s.close()

if __name__ == '__main__':
    main()

```

<img src=temp/28.png>

# Roberval
 
### Challenge
 
<img src=temp/29.png>

```
# nc programming.letspentest.org 8333
Harry có một túi bi gồm N viên, trong đó, có 1 viên bi nhẹ hơn so với các viên bi còn lại. Harry cho thí sinh một chiếc cân Roberval và yêu cầu sử dụng chiếc cân này để tìm ra viên bi nhẹ hơn với ít số lần cân nhất. 
Với N = 243 
Số lần cân ít nhất là:
```
 
### Solution

* Bạn đã nghe qua bài toán cân bi chưa? Chưa biết thì đọc đi nhé.
* Hướng giải quyết là ta sẽ sử dụng thuật toán "chia ba".
* Lấy N chia 3 rồi cập nhật N là kết quả của phép tính. Đến khi N còn 1 hoặc 2 (tức < 3) thì số lần đem chia 3 chính là số lần cân ít nhất.
* *Lưu ý: Do mình nhận thấy server chỉ gửi số lẻ nên mình sẽ giải quyết theo cách trên. Bài toàn vừa nêu chưa thật sự tối ưu và chính xác (nhưng mình cũng tìm được cờ nên dừng lại, bạn đọc tham khảo và phát triển thêm nhé)*

```python
#!/usr/bin/python3
import socket

IP, PORT = ('programming.letspentest.org', 8333)

def receive_all_line(s):
    data = s.recv(999999)
    return data.decode()

def receive_one_line(s):
    r = b''
    while (True):
        t = s.recv(1)
        if t == b'\n': break
        r = r + t
    return r.decode()

def send_one_line(s, data):
    s.sendall(f"{data}\n".encode())

def solver(n):
    count = 0
    while (n >= 3):
        n = n // 3
        count += 1
    return count

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((IP, PORT))
    
    while True:
        banner = receive_one_line(s)
        print(banner)
        while 'N =' not in banner:
            if 'Flag{' in banner: exit()
            banner = receive_one_line(s)
            print(banner)
        banner = banner[8:]
        answer = solver(int(banner))

        banner = receive_one_line(s)
        print(banner)
        send_one_line(s, answer)
        print(answer)

    s.close()

if __name__ == '__main__':
    main()

```

<img src=temp/2a.png>

# Where is my house
 
### Challenge
 
<img src=temp/1b.png>
 
### Solution

* Bài này mình dùng https://www.nslookup.io/ để scan.

<img src=temp/1c.png>

# Scan me if you can
 
### Challenge
 
<img src=temp/1d.png>
 
### Solution

* Scan port của nó.

```
# nmap -Pn network-insecure.letspentest.org
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-11-01 18:37 +07
Nmap scan report for network-insecure.letspentest.org (18.140.65.99)
Host is up (0.057s latency).
rDNS record for 18.140.65.99: ec2-18-140-65-99.ap-southeast-1.compute.amazonaws.com
Not shown: 999 filtered ports
PORT     STATE SERVICE
9003/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 169.98 seconds
```

* Có 1 port nhưng không xác định được dịch vụ.
* Scan kiểu khác xem.

```
# nmap -sV network-insecure.letspentest.org
Starting Nmap 7.91 ( https://nmap.org ) at 2021-11-01 18:36 +07
Nmap scan report for network-insecure.letspentest.org (18.140.65.99)
Host is up (0.0073s latency).
rDNS record for 18.140.65.99: ec2-18-140-65-99.ap-southeast-1.compute.amazonaws.com
Not shown: 999 filtered ports
PORT     STATE SERVICE    VERSION
9003/tcp open  tcpwrapped

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.25 seconds
```

* Lần này thì thấy port `9003` sử dụng dịch vụ `tcpwrapped`.
* Xem thử 1 vài thông tin về tcpwrapped. Thì khi xem đến trang này https://news.cloud365.vn/tcp-wrappers-chung-la-gi-va-chung-duoc-su-dung-nhu-the-nao-trong-linux/. Họ có đề cập `Wrappers không hoạt động với các dịch vụ gọi thủ tục từ xa (RPC) qua TCP)`
* OK, vậy netcat thử.

```
# nc network-insecure.letspentest.org 9003
aaa
HTTP/1.1 400 Bad Request
Server: Flag{Every-Header-Have-It-Own-Meaning}Date: Mon, 01 Nov 2021 11:53:07 GMT
Content-Type: text/html
Content-Length: 157
Connection: close

<html>
<head><title>400 Bad Request</title></head>
<body>
<center><h1>400 Bad Request</h1></center>
<hr><center>nginx/1.20.0</center>
</body>
</html>
```

* Vậy là có được cờ.

# Very Good Shipper
 
### Challenge
 
<img src=temp/2b.png>
 
### Solution

* Bài này chỉ cần netcat vào và trả lời câu hỏi.

```
# nc network.letspentest.org 9003

Chào mừng bạn đến với cánh cửa thử thách của Cookie Arena Season 1.
 Để vượt qua thử thách này, hãy trả lời đúng các câu hỏi dưới đây.
Ở mỗi câu hỏi bạn sẽ có 10s để nhập câu trả lời A, B, C, D.

Ngoài 3 giải chính (nhất, nhì, ba), thì Cookie Hân Hoan có bao nhiêu giải thưởng phụ?
A.5
B.2
C.8
D.10
D

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░

Cookie Hân Hoan là fanpage chia sẻ về?
A.Bài học cuộc sống 
B.Chuyện cười 
C.Bánh bánh quy
D.Bảo mật và an toàn thông tin
D

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░

Có bao nhiêu chủ đề trong Cookie Arena Season 1?
A.6
B.2
C.4
D.3
A

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░

Cookie Hân Hoan có bao nhiêu nhân vật chính?
A.1
B.4
C.2
D.3
B

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░

Bạn đang kết nối tới cánh cửa này thông qua giao thức mạng nào?
A.TCP
B.UDP
C.ICMP
D.FTP
A

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░

Những người được ban tổ chức lựa chọn để trao giải, có phải gửi cách giải các thử thách (write-up) cho BTC không?
A.Có
B.Không
A

░ ∗ ◕ ں ◕ ∗ ░ Chuẩn Rồi ░ ∗ ◕ ں ◕ ∗ ░


Flag{t00-ez-4-y0u}
```

# Post Office Man
 
### Challenge
 
<img src=temp/2c.png>
 
### Solution

* Bài này thì cứ netcat vào ta thấy server đề cập đến USER, PASS.
* OK bạn có biết giao thức POP3 và các câu lệnh ko. Tìm đọc nhé.
* *POP viết tắt của từ Post Office Protocol là một giao thức tầng ứng dụng, dùng để lấy thư điện tử từ server mail, thông qua kết nối TCP/IP.*

```
# nc network.letspentest.org 9002                                      
+OK popper file-based pop3 server ready

Please using USER to login first
Các Bạn hãy sử dụng câu lênh USER để login vào hệ thống
(Cứ nhập linh tinh zô 乁| ･ 〰 ･ |ㄏ)
USER aaaa

+OK user accepted

Please using PASS to login first
Các Bạn hãy sử dụng câu lênh PASS để login vào hệ thống
(Cú nhập linh tinh zô 乁| ･ 〰 ･ |ㄏ)
PASS aaaa

+OK pass accepted


POP3 do not understand the command  ▐  ⊙ ▃ ⊙ ▐
POP3 không hiểu cấu lệnh mà bạn vừa nhập vào  ▐  ⊙ ▃ ⊙ ▐
STAT

+OK 10 9400
RETR 10

+OK 940 octets
Received: from [208.10.167.165] by sweetwater.netease.net
(SMTPD32-5.05) id AC28801E8; Thu, 19 Aug 1999 20:15:20 -0500
Message-Id: <199908192015750.SM00960@>
X-RCPT-TO: dusty@demo.netease.net
Date: Thu, 19 Aug 1999 20:15:55 -0500
X-UIDL: 230371285
Status: U
From: <dusty@netease.net>


Subject: test
Dear Anonymous,

Thank you for using ThrowAway Mail to fight spam, your temporary disposable email is :

prugochihu@wemel.site

Get the #1 Rated VPN Exclusive offer: Save 49% & try ExpressVPM 100% risk-free!


Use it to communicate with any website you want to. You have 48 hours to use this mailbox, if you do not visit your mail inbox within 48 hours, it wil be deleted , once visited your mail box extends to another 48 hours.

For using this service you MUST enable cookie and javascript, cookie is just to record your session id and language preference, your Privacy is covered under our Privacy and Cookie policy .

ThrowAwayMail Team

RETR 9

+OK 940 octets
Received: from [208.10.167.165] by sweetwater.netease.net
(SMTPD32-5.05) id AC28801E8; Thu, 19 Aug 1999 20:15:20 -0500
Message-Id: <199908192015750.SM00960@>
X-RCPT-TO: dusty@demo.netease.net
Date: Thu, 19 Aug 1999 20:15:55 -0500
X-UIDL: 230371285
Status: U
From: <dusty@netease.net>


Subject: test
Dear Anonymous,

Thank you for using ThrowAway Mail to fight spam, your temporary disposable email is :

prugochihu@wemel.site

Get the #1 Rated VPN Exclusive offer: Save 49% & try ExpressVPM 100% risk-free!


Use it to communicate with any website you want to. You have 48 hours to use this mailbox, if you do not visit your mail inbox within 48 hours, it wil be deleted , once visited your mail box extends to another 48 hours.

For using this service you MUST enable cookie and javascript, cookie is just to record your session id and language preference, your Privacy is covered under our Privacy and Cookie policy .

ThrowAwayMail Team

RETR 8

+OK 940 octets
Received: from [208.10.167.165] by sweetwater.netease.net
(SMTPD32-5.05) id AC28801E8; Thu, 19 Aug 1999 20:15:20 -0500
Message-Id: <199908192015750.SM00960@>
X-RCPT-TO: dusty@demo.netease.net
Date: Thu, 19 Aug 1999 20:15:55 -0500
X-UIDL: 230371285
Status: U
From: <dusty@netease.net>


Subject: test
Dear Anonymous,

Thank you for using ThrowAway Mail to fight spam, your temporary disposable email is :

prugochihu@wemel.site

************************| Flag{1-Ha\/3-1o0o-UnS33n-3Ma1L} |********************


Use it to communicate with any website you want to. You have 48 hours to use this mailbox, if you do not visit your mail inbox within 48 hours, it wil be deleted , once visited your mail box extends to another 48 hours.

For using this service you MUST enable cookie and javascript, cookie is just to record your session id and language preference, your Privacy is covered under our Privacy and Cookie policy .

ThrowAwayMail Team
```

# Secure HTTP
 
### Challenge
 
<img src=temp/2d.png>
 
### Solution

* Truy cập trang với HTTP thì ko được. Thử với HTTPS thì được.
* Bài đề cập đến `"mã hóa dữ liệu trong quá trình trao đổi giữa trình duyệt và máy chủ"`.
* OK, dùng wireshark để capture thử nhé. Mình Follow TCP đến Stream thứ 5 là thấy cờ.

<img src=temp/2e.png>

# XOR
 
### Challenge
 
[encrypt.py](temp/encrypt.py)

[cipher.txt](temp/cipher.txt)
 
### Solution

* Mở file encrypt.py xem thử thì thấy key len chỉ có 1.
* OK, vậy chỉ cần bruteforce thôi. Mình dùng trang này https://www.dcode.fr/xor-cipher, sử dụng tùy chọn `KNOWING THE KEY SIZE (IN BYTES)` là `1`

<img src=temp/1e.png>

<img src=temp/1f.png>

# Morse
 
### Challenge
 
[cipher.wav](temp/cipher.wav)
 
### Solution

* Mở file lên nghe tút tút.. OK Morse đấy, mình dùng trang này rồi bỏ vào cho nó làm việc thôi https://morsecode.world/international/decoder/audio-decoder-expert.html

# Julius Caesar
 
### Challenge
 
`Synt{Ry_Pynfvpb_Pvcure}`
 
### Solution

* OK dùng trang này bruteforce cho nhanh https://www.dcode.fr/caesar-cipher

<img src=temp/20.png>

# Sixty Four
 
### Challenge
 
`NDY2QzYxNjc3QjVGNUY1RjQyNjE3MzY1MzYzNDc4NDg2NTc4NUY1RjVGN0Q=`
 
### Solution

* Bài này đơn giản thôi. base64 > hex.

# Basic Image
 
### Challenge
 
[KB.jpg](temp/KB.jpg)
 
### Solution

* Dùng exiftool.

```
# exiftool KB.jpg 
ExifTool Version Number         : 12.32
File Name                       : KB.jpg
Directory                       : .
File Size                       : 241 KiB
File Modification Date/Time     : 2021:11:01 20:10:43+07:00
File Access Date/Time           : 2021:11:01 20:11:16+07:00
File Inode Change Date/Time     : 2021:11:01 20:11:06+07:00
File Permissions                : -rw-------
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Exif Byte Order                 : Big-endian (Motorola, MM)
Make                            : Flag{metadataratatatataaaaaa}
Artist                          : cookiehanhoan
XP Author                       : cookiehanhoan
Padding                         : (Binary data 2030 bytes, use -b option to extract)
Current IPTC Digest             : 946603002c9e60851a0e31aed59ec2bd
Coded Character Set             : UTF8
Special Instructions            : FBMD01000a8c01000084810000e5040100d82e0100c84d010014c40100f4520200688302007da90200e2c802004aa80300
By-line                         : cookiehanhoan
IPTC Digest                     : 946603002c9e60851a0e31aed59ec2bd
About                           : uuid:faf5bdd5-ba3d-11da-ad31-d33d75182f1b
Creator                         : cookiehanhoan
Image Width                     : 2048
Image Height                    : 2048
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2048x2048
Megapixels                      : 4.2
```

# ExSeller
 
### Challenge
 
[bruteme.xlsx](temp/bruteme.xlsx)
 
### Solution

* Bài này mình dùng binwalk kết hợp grep.

```
# binwalk -e bruteme.xlsx

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 361, uncompressed size: 1440, name: [Content_Types].xml
930           0x3A2           Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 588, name: _rels/.rels
1735          0x6C7           Zip archive data, at least v2.0 to extract, compressed size: 258, uncompressed size: 980, name: xl/_rels/workbook.xml.rels
2313          0x909           Zip archive data, at least v2.0 to extract, compressed size: 732, uncompressed size: 1632, name: xl/workbook.xml
3090          0xC12           Zip archive data, at least v2.0 to extract, compressed size: 1870, uncompressed size: 8390, name: xl/theme/theme1.xml
5009          0x1391          Zip archive data, at least v2.0 to extract, compressed size: 498, uncompressed size: 916, name: xl/worksheets/sheet2.xml
5561          0x15B9          Zip archive data, at least v2.0 to extract, compressed size: 458, uncompressed size: 832, name: xl/worksheets/sheet3.xml
6073          0x17B9          Zip archive data, at least v2.0 to extract, compressed size: 503, uncompressed size: 938, name: xl/worksheets/sheet1.xml
6630          0x19E6          Zip archive data, at least v2.0 to extract, compressed size: 188, uncompressed size: 223, name: xl/sharedStrings.xml
6868          0x1AD4          Zip archive data, at least v2.0 to extract, compressed size: 662, uncompressed size: 1540, name: xl/styles.xml
7573          0x1D95          Zip archive data, at least v2.0 to extract, compressed size: 405, uncompressed size: 831, name: docProps/app.xml
8288          0x2060          Zip archive data, at least v2.0 to extract, compressed size: 318, uncompressed size: 597, name: docProps/core.xml
9697          0x25E1          End of Zip archive, footer length: 22

# grep -r "Flag{" _bruteme.xlsx.extracted 
_bruteme.xlsx.extracted/xl/sharedStrings.xml:<sst xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" count="2" uniqueCount="2"><si><t>check</t></si><si><t>Flag{Micro$oft_Heck3r_Man}</t></si></sst>
```

# Streamer
 
### Challenge
 
[travis.pcapng](temp/travis.pcapng)
 
### Solution

* Bài cho ta 1 file pcapng. Dùng wireshark để đọc.
* Thử xem trên giao thức HTTP có file nào lấy được không (File > Export Objects > HTTP...) thì phát hiện có file `evilcontent.zip`. 

<img src=temp/21.png>

* OK save xuống và mở lên thì thấy file `flag.txt`

<img src=temp/22.png>

* Ta cần tìm pass để mở, thử xem tiếp qua giao thức TCP (Analyze > Follow > TCP Stream). Xem 1 lượt đến stream thứ 5 thì thấy như sau.

<img src=temp/23.png>

* Thử dùng password đó mở file zip. (Kết quả thành công, ta có được cờ.)

# Interceptor
 
### Challenge
 
[cooooooooooookie.gif](temp/cooooooooooookie.gif)
 
### Solution

* Mình dùng công cụ split gif online để cắt https://ezgif.com/split
* Sau đó quan sát thì thấy ở mỗi hình có 1 phần mã QR.
* Tổng có 9 phần, ghép lại đủ ta được mã QR code. Scan mã ta được cờ.

<img src=temp/24.png>

# AudiCaty
 
### Challenge
 
[squitgaem.wav](temp/squitgaem.wav)
 
### Solution

* AudiCaty tức là đề cập đến Audacity. Vậy dùng Audacity để mở file. 
* Mình đặt Spectrogram và Rate 22050Hz là đọc được cờ.

<img src=temp/34.png>

# Volatility
 
### Solution

* Bài này mình chỉ cần dùng `strings` và `grep` là tìm được cờ.

<img src=temp/35.png>

# Ét Quy Eo
 
### Challenge
 
<img src=temp/25.png>
 
### Solution

* Bài này cho ta 1 form login, thử `' or 1=1--` thì được ngay.
* Ta được mã base64 `RmxhZ3tGcjMzX1N0eWwzfQ==` decode ta có được cờ.

# SQL Filter
 
### Solution

* Bài này vẫn là SQLi tuy nhiên có filter.
* Thử với chữ `or` => blacklist
* Thử với `is` => được
* Thử với `not` => được
* Thử với `is not` => blacklist
* OK, do this `is/**/not` => pass
* Vậy payload của ta đơn giản như sau: `'/**/is/**/not/**/'a` => login thành công được mã base64, decode ra cờ

# The maze runner
 
### Challenge
 
<img src=temp/26.png>
 
### Solution

* Bài này trang web cho ta một mê cung rất nhiều site.
* Mình giải quyết bằng cách liệt kê ra tất cả các site sử dụng https://www.mysitemapgenerator.com/
* Sau đó phát hiện có site chưa cờ là `/MS70RIE/2D5TA9DK/UGR85I0H/60ADG`

# Misconfiguration
 
### Challenge
 
<img src=temp/2f.png>
 
### Solution

* Bài này mình dùng dirsearch để tìm các site truy cập được. Kết quả có 2 site.

<img src=temp/30.png>

<img src=temp/31.png>

* Đến đây thì ta có 2 phần của cờ.
* Tải xuống file `backup-ddmmyy.bak` mà site 2 đề cập. Dump nó với HxD thì thấy có file part3.txt nhúng được nhúng bên trong.

<img src=temp/33.png>

* Dùng `binwalk` để giải nén. Ta được phần còn lại của cờ.

```bash
# binwalk -e backup-ddmmyy.bak
```

<img src=temp/32.png>

# Gatling gun
 
### Challenge
 
<img src=temp/36.png>
 
### Solution

* Truy cập trang web có 3 chỗ input và bài đề cập đến gatling gun. Là muốn ta bruteforce tuy nhiên có tới 3 input thì hơi nhiều.

<img src=temp/37.png>

* Gợi ý bài là `"nhặt đạn ở trong Github của Cookie Hân Hoan"`.
* Tìm đến github với user có tên `"Cookie Hân Hoan"`.

<img src=temp/38.png>

* Vào repo `HoangTuEch` ta thấy có 3 file ứng với 3 input.

<img src=temp/39.png>

* OK, có đạn rồi, brute force thôi. Sử dụng burp suite chế độ intruder cluster bomb (bạn đọc tự tìm hiểu nhé https://youtu.be/4mpszXedKeQ?t=431).
* Đợi 1 tí là có cờ.

<img src=temp/3a.png>
