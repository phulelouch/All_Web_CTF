# Steps of web exploitation:

### *Chủ yếu checklist này sẽ xài cho các bài black_box, tất nhiên vẫn nên sử dụng cho các bài white_box để xác định hướng exploit. Và sáng tạo lên, đừng bám theo cái này :v *

## 1. F12 View Page Source
- Theo luôn các link nó ghi
- Vào network xem cả file javascript
- is_debug=1, source=1


## 2.Directory listing
### Luôn thực hiện fuzz thư mục trước, có thể dirb hoặc chỉ xài burp intruder
#### Các file chú ý: robots.txt, gitignore, .svn, .listin, .dstore, etc. Tool: FOCA.
#### Còn có: /upload/ 

wordlists: /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
#### Download website: 
- wget -rck
- wget -r -l1 -H -t1 -nd -N -nd -N -A.swf -erobots=off <WEBSITE> -i output_swf_files.txt 


## 3. Xác Định Các Parameter cho server-side
#### - Parameter thường trong GET ?x=... POST 
#### - COOKIES và SESSIONS
#### - Cả URI cũng có thể inject 
#### - User-Agent 

## 4. Fuzz các parameters
### Với Parameter thường trong GET ?x=... POST 
- Fuzz các kí tự đặc biệt
  /SecLists/Fuzzing/special-chars.txt
- Fuzzing full trong Burp Intruder
- A-Z a-z 0-9
- Thử 2 parameter cùng lúc sẽ ntn 
- Các format string: **%s**  %c %d %e %f %I %o %p  %x %n 
- Một integer rất lớn: integer overflow
- Fuzz với dấu cách (whitespace)
- Các PHP function: phpinfo, show_source, serilization, unserilization ... 
- Fuzz với các lỗi SQL, XSS, ... *(chắc phải tạo file khác list các lỗi)*
- Fuzz với encode các kiểu như: md5, base64, oct, hex, URL, HTML 
  - VD: bài NumberMakeup: '||$['\147\154\157\142\141\154\105\166\141\154']('\141\154\145\162\164\50\61\51')||'

### Với COOKIES và SESSIONS:
- Decode các kiểu md5, base64, oct, hex, URL, HTML 
- Thử cookie, session flask exploit các kiểu https://gchq.github.io/CyberChef/
- Cookie Forcing/Injection
- Jwt exploit:
  + brute for secret key
  + change alg to None or HS256
  + fake rsa key for RS256 alg
  + if we can control some parameter in jwt, we alse use json injection for bypass some thing
 


## 5. Payload all the things
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/

https://github.com/JohnHammond/ctf-katana

https://github.com/w181496/Web-CTF-Cheatsheet#php-%E5%85%B6%E4%BB%96%E7%89%B9%E6%80%A7





