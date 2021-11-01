# Cookie Arena Season 1 - Capture The Flag (CTF)

### Overview
 | Title | Category | Points | Flag
 | ------ | ------ | ------ | ------ |
 | [Hân Hoan](#Hân-Hoan) | Web Basic | 1 | `Flag{Cookies_Yummy_Cookies_Yammy!}` |
 | [JS Bp Bp](#JS-Bp-Bp) | Web Basic | 1 | `Flag{JAV-ascript_F*ck}` |
 | [Impossible](#Impossible) | Web Basic | 1 | `Flag{Javascript_is_not_safe???}` |
 | [Infinite Loop](#Infinite-Loop) | Web Basic | 1 | `Flag{Y0u_c4ptur3_m3_xD!!!}` |
 | [I am not a robot](#I-am-not-a-robot) | Web Basic | 1 | `Flag{N0_B0T_@ll0w}` |
 | [Sause](#Sause) | Web Basic | 1 | `Flag{Web_Sause_Delicious}` |
 
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
