# XSS

![Screenshot 2025-05-09 012554](https://github.com/user-attachments/assets/a9bf5e3b-80e3-4c0c-9469-858fe8a31364)

![Screenshot 2025-05-09 013154](https://github.com/user-attachments/assets/d315fd9f-8b40-4742-bebb-1673aa5f4f35)

> <script>alert('heloooo')</script>

![Screenshot 2025-05-09 013237](https://github.com/user-attachments/assets/b7cf1b2b-1be1-42be-a64b-8dd5a693aee3)

![image](https://github.com/user-attachments/assets/3cf85edc-c839-4f7d-a543-c4cfa3fcd176)

# DOM XSS

![image](https://github.com/user-attachments/assets/10427616-f046-4fa7-931e-06e663b051d6)

Lần này payload không hoạt động, vì payload được gán thẳng vào innerHTML

![image](https://github.com/user-attachments/assets/82bc8f55-fa28-444a-aaa3-77026b2a06fb)

Có lẻ innerHTML không chạy các thẻ <script> nhưng <img thì được

Ta sẽ gửi một payload như sau 

> <img src="" onerror="alert('aaaa')>

khi ảnh không được tải lên thì sự kiện onerror sẽ thực thi và khi đó

![image](https://github.com/user-attachments/assets/3a98aa17-0013-4485-b1ce-11f96f4475be)



