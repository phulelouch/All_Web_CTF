#### This paper is writting with the intention of understanding PHP Object under Offensive Security aspect (or Hacker, Red Team aspect), in order to gain insight into a security problem that have been exist since the first day of Java, PHP and other programming languages that support OOP.

#### Although this paper only covering PHP language, the problems happend in others. First we will discuss what we know. Second study a real vulnerability in Magento case.


### 1. Object and Magic method
#### This is an interesting topic. In a simple way PHP do support Object-Oriented Programming in a strange way, with serialize and unserialize, developer can chooses anything to be objects in PHP'VM memory. Let's look at a simple example. 

#### EX1:
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
#### The result :
```
calling __construct
calling __destruct
(+) serialized: O:2:"aw":0:{}
calling __destruct

```

Here we can see that there was 2 times \_\_destruct was call

#### EX2:
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
#### And the result:
```
calling __construct
(+) serialized: O:3:"aws":0:{}
calling __destruct
calling __destruct
```
Class get constructed and destructed at run time for memory management
purposes within the PHP virtual machine. Note that the \_destruct gets called twice, once on unserialize() and then again on script completion. So they are different.

- serialize($mixed)
Generates a storable representation of a value (of any type). This is useful for storing or passing PHP values around without losing their type and structure.
- unserialize($string)
Takes a single serialized string variable and converts it back into a PHP value.

#### We can use stdClass unserialize no class name

#### In PHP (and other languages as well) there are a number of "magic methods" when implemented within an object, are triggered on certain conditions. Two very important ones in PHP are \_construct and \_destruct. However, there are many others. Let's break down a list:

<img src="https://github.com/phulelouch/All_Web_CTF/blob/master/PHP/Pics/php_magic_method.png">


### 2. PHP Overloading

Overloading, specifically in PHP, refers to the dynamic creation of properties and methods processed via magic methods.

There are several methods used by magic methods to perform this "dynamic" creation. Two importants ones are:
- call_user_func_array ($callback, $array) : call a callback with an array of parameters
- call_user func($callback,[, $param [, $param]]) : call a callback with any number of arguments

Why did these 2 matter, these are often included in the '\_call' magic method and if abused correctly, can allow the redirection of code flow.

### 3. Private Properties and Methods
```
<?php
class a{
	private $student = "mr_me";
	public $teacher = "muts";
}
$a_instance = new a;
print $a_instance-> teacher;
print $a_instance-> student;
?>

```

The result would be some thing:
```
PHP Warning:  Uncaught Error: Cannot access private property awae::$student in php shell code:1
Stack trace:
#0 {main}
  thrown in php shell code on line 1
```

The way around this is to put that private method into public constructor or change the private into public. 
Or we can modify the serialize string in order to suite our need. Let choose the hard way.
```
<?php
class aw {
	private $student = "mr me\n";
	public $teacher  = "muts\n";
	public function __construct($student) {
		$this->student = $student;
		echo $this->student."\n";
	}
}
$aw = new aw("OSID24561");
print$aw->teacher;
?>

```

```
OSID24561
muts
```


### 4 The Devil of Details

We know that unserialize function take a string parameter, which is the output of serialize, right? So what does this string look like:

With an object like this:
```
<?php
class Hi {
	public $public       = 1;
	protected $protected = 2;
	private $private     = 3;
}
$hi = new Hi();
print(base64_decode(base64_encode(serialize($hi))));
?>
```
Create:
O:2:"Hi":3:{s:6:"public";i:1;s:12:"\*protected";i:2;s:11:"Hiprivate";i:3;}

However, this is actually wrong, and will NOT serialize back into PHP's memory. When unserialize we got an error:
```
Notice:  unserialize(): Error at offset 47 of 73 bytes in /home/phulelouch/Desktop/All_Web_CTF/untitled.php on line 
```


