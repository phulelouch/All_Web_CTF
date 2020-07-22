# 1. some strange of php
- php use {} like [] for array
- bypass some function like md5 or sha1 just with array in input
- php replace . with _
## php type Juggling
- "a"==0 => true
- "7a...."==int(7),.. etc
- md5 magic for bypass some md5 func
## func vuln
- file_get_contents also use like curl
- fake data with data:text/plain
- extract() rewrite value of var in program
- use php://filter/convert.base64-encode/resource=index.php for lfi chall 
