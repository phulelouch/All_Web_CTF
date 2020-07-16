#### Đây là 1 vấn đề khá thú vị. Nói đơn giản về PHP Object thì: 1 Object có thể là bất cứ thứ gì mà developer chọn.
```
<?php
class awae {
	public function __construct() {echo "calling __contruct\n";}
	public function __destruct() {echo "calling __destruct\n";}
}

$ser = serialize(new awae());//triggers the __construct
print"(+) serialized: ".$ser."\n";
unserialize($ser);//trigger the __detruct

?>
```
#### Kết quả sẽ như thế này :
```
calling __contruct
calling __destruct
(+) serialized: O:4:"awae":0:{}
calling __destruct
```
Ở đây chúng ta thấy rằng có 2 lần \_\_contruct được gọi
