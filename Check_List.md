# Steps of web exploitation:
## 1.Directory listing
### Luôn thực hiện fuzz thư mục trước, có thể dirb hoặc chỉ xài burp intruder
#### Các file chú ý: robots.txt, gitignore, .svn, .listin, .dstore, etc. Tool: FOCA.
#### Còn có: /upload/ 

wordlists: /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
#### Download website: 
- wget -rck
- wget -r -l1 -H -t1 -nd -N -nd -N -A.swf -erobots=off <WEBSITE> -i output_swf_files.txt 


## 2. Xác Định Các Parameter
### - Parameter trong GET ?x=... POST 
### - COOKIES và SESSIONS
### - Cả URI cũng có thể inject 
### - User-Agent *(ít trong CTF)*

## 3. 


