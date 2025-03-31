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
![image](https://github.com/user-attachments/assets/f8750545-aed0-48f7-b6fc-af9b5df00a92)
- Khi phar://evil.phar được thực thi, magic method của Evil sẽ được gọi
## Bypass với natas33:
  ![image](https://github.com/user-attachments/assets/65b08bc7-eb66-4a41-9de9-f1faff272207)
- Giải thích đơn giản thì ở câu này ta upload file (ví dụ là hehe.php) và server sẽ mã hoá md5(hehe.php) == siganture thì thực thi file
- Ta có thể thấy việc so sánh "==" được diễn ra ở *__destruct* --một magic method (nghe quen chứ) :grinning:
- So sánh "==" thì khá dễ để bypass (một ông anh đẹp trai nào đó gửi tôi bảng này) :goat:
  ![image](https://github.com/user-attachments/assets/adc75c58-b28f-48ea-87d7-dad3dc9bba46)
- Vì tôi sẽ upload file *shell.php* để khai thác pass nên chuyện gì xảy ra nếu tôi đổi *Siganture = true* (theo cái bảng thì **md5(shell.php) == true** return *true* ... chắc chắn rồi)
- Chuyện cần làm bây giờ chỉ là xào lại cái code mẫu ở trên
1. Chuyển tham số theo ý tôi muốn
2. Tải lên file shell.php
3. Chạy phar://hehe.phar . Break xong nhảy thẳng vô chạy thằng __Destruct().
   ![image](https://github.com/user-attachments/assets/f35f6202-d241-4e42-8d2f-bb4bf1be1667)
5. Lụm cờ
![image](https://github.com/user-attachments/assets/2f74ebb1-5d7c-41a3-8e86-206fba13b9fd)
## Note
- Ở bước so sánh  **md5(shell.php) == Signature** tôi đã thử đổi **Sig** cho giống với md5(shell.php) và tất nhiên nó cũng hoạt động
### Magic method là gì
- Là **method** nhưng có **__** đằng trước
- Tự động thực thi khi có một sự kiện gì đó xảy ra -- cảm ơn chatGPT
  ![image](https://github.com/user-attachments/assets/16b8fc1a-d893-4dc4-8f84-f1c02a8db760)
- Chi tiết [magicmethod](https://www.php.net/manual/en/language.oop5.magic.php)
### Stub?
- Tới đây lười quá r nên là ***HAFL gì gì đó** được sử dụng trong code là để nhận biết những phần còn lại là Binary nên không cần đụng tới.
- Phần còn lại là cái gì thì k biết đâu đừng có hỏi  :grinning:

  


 




