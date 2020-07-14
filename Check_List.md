# Steps of web exploitation:

## 1. F12 View Page Source
- Theo luôn các link nó ghi
- Vào network xem cả file javascript


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
#### - User-Agent *(ít trong CTF)*

## 4. Fuzz các parameters
### Với Parameter thường trong GET ?x=... POST 
- Fuzz các kí tự đặc biệt
  /SecLists/Fuzzing/special-chars.txt
- Fuzzing full trong Burp Intruder
- A-Z a-z 0-9
- Thử 2 parameter cùng lúc sẽ ntn 
- Các format string: **%s**  %c %d %e %f %I %o %p  %x %n 
- Một integer rất lớn: integer overflow
- Các PHP function: phpinfo, show_source, ... 
- Fuzz với các lỗi SQL, XSS, ... *(chắc phải tạo file khác list các lỗi)*
- Fuzz với encode các kiểu như: md5, base64, oct, hex, URL, HTML 
  - VD: bài NumberMakeup: '||$['\147\154\157\142\141\154\105\166\141\154']('\141\154\145\162\164\50\61\51')||'

### Với COOKIES và SESSIONS:
- Decode các kiểu md5, base64, oct, hex, URL, HTML 
- Thử cookie, session flask exploit các kiểu




