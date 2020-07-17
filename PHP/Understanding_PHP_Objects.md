#### Đây là 1 vấn đề khá thú vị. Nói đơn giản về PHP Object thì: 1 Object có thể là bất cứ thứ gì mà developer chọn. Trước hết có 2 ví dụ dưới đây:

#### VD1:
```
<?php
class aw {
	public function __construct() {echo "calling __construct\n";}
	public function __destruct() {echo "calling __destruct\n";}
}

$ser = serialize(new aw());//triggers the __construct
print"(+) serialized: ".$ser."\n";
unserialize($ser);//trigger the __detruct
?>

```
#### Kết quả sẽ như thế này :
```
calling __construct
calling __destruct
(+) serialized: O:2:"aw":0:{}
calling __destruct

```

Ở đây chúng ta thấy rằng có 2 lần \_\_destruct được gọi.

#### VD2:
```
<?php
class aws {
	public function __construct() {echo "calling __construct\n";}
	public function __destruct() {echo "calling __destruct\n";}
}
$try  = new aws();
$sera = serialize($try);//triggers the __construct
print"(+) serialized: ".$sera."\n";

unserialize($sera);//trigger the __detruct
?>
```
#### Kết quả:
```
calling __construct
(+) serialized: O:3:"aws":0:{}
calling __destruct
calling __destruct
```

\_\_destruct lại được gọi 2 lần nhưng lần này có sự khác biệt
- Thực ra \_\_construct luôn được gọi đầu tiên khi ta tạo new object tức khi bắt đầu tham chiếu
- Và 1 hàm \_\_destruct luôn sẽ được gọi khi object tự hủy. Với VD1: `new aw()` tức là nó sẽ tự tham chiếu và hủy tham chiếu vào 1 biến $temp. Còn với VD2 object được đặt trong 1 biến $try, tức là còn tham chiếu nên nó chỉ tự hủy sau khi unserialize ra $try và hủy tham chiếu (việc hủy tham chiếu có thể là do việc hủy trương trình)
- Một \_\_destruct còn lại chính là do unserialize  

#### Khó hiểu vãi lìn phải không nào, nhưng thôi ráng đê :v

#### Ngoài construct và destruct còn có những "magic methods" khác, hãy xem list dưới đây nhé:

<img src="https://github.com/phulelouch/All_Web_CTF/blob/master/PHP/Pics/php_magic_method.png">

#### À thiều \_unset($key) nha:
This is triggered when code calls unset() on the object where the variable is inaccessible.
