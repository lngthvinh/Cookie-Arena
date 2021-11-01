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
 | [SUM](#SUM) | Programming | 1 | `Flag{1plust1_1s_2_qu1ck_mafth}` |
 | [Where is my house](#Where-is-my-house) | Network | 1 | `Flag{DNS_A_AAAA_TXT_CNAME}` |
 | [Scan me if you can](#Scan-me-if-you-can) | Network | 1 | `Flag{Every-Header-Have-It-Own-Meaning}` |
 | [XOR](#XOR) | Cryptography | 1 | `Flag{a^b=c=>b^c=a}` |
 | [Morse](#Morse) | Cryptography | 1 | `Flag{M.O.R.S.E.C.O.D.E}` |
 | [Julius Caesar](#Julius-Caesar) | Cryptography | 1 | `Flag{El_Clasico_Cipher}` |
 | [Sixty Four](#Sixty-Four) | Cryptography | 1 | `Flag{___Base64xHex___}` |
 | [Basic Image](#Basic-Image) | Forensic | 1 | `Flag{metadataratatatataaaaaa}` |
 | [ExSeller](#ExSeller) | Forensic | 1 | `Flag{Micro$oft_Heck3r_Man}` |
 | [Streamer](#Streamer) | Forensic | 1 | `Flag{TCP_streamin_go_skrrrrrrrt}` |
 | [Interceptor](#Interceptor) | Forensic | 1 | `Flag{1s_th1s_m1sc3llan30us?}` |
 
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
* Xem thử 1 vài thông tin về tcpwrapped. Thì khi xem đến trang này https://news.cloud365.vn/tcp-wrappers-chung-la-gi-va-chung-duoc-su-dung-nhu-the-nao-trong-linux/
* Họ có đề cập `Wrappers không hoạt động với các dịch vụ gọi thủ tục từ xa (RPC) qua TCP)`
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
