#### Đây là 1 vấn đề khá thú vị. Nói đơn giản về PHP Object thì: 1 Object có thể là bất cứ thứ gì mà developer chọn. Trước hết có 2 ví dụ dưới đây:
```
<?php
class awae {
	public function __construct() {echo "calling __construct\n";}
	public function __destruct() {echo "calling __destruct\n";}
}

$ser = serialize(new awae());//triggers the __construct
print"(+) serialized: ".$ser."\n";
unserialize($ser);//trigger the __detruct

?>
```
#### Kết quả sẽ như thế này :
```
calling __construct
calling __destruct
(+) serialized: O:4:"awae":0:{}
calling __destruct
```
\_\_construct được 
Ở đây chúng ta thấy rằng có 2 lần \_\_destruct được gọi.
