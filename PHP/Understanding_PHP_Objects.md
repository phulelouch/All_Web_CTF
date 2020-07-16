#### Đây là 1 vấn đề khá thú vị. Nói đơn giản về PHP Object thì: 1 Object có thể là bất cứ thứ gì mà developer chọn.
```
<?php
class awae{
  public function __construct() {echo "calling __contruct\n"; }
  public function __destruct() {echo "calling __destruct\n"; }
 }
$ser = serialize(new awae); //triggers the __construct
print "(+) serialized: ".$ser."\n";
unserialize($ser); //trigger the __detruct
?>
