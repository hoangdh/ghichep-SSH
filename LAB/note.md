======= Một vài ghi chép về sử dụng SSH =======

<blockquote>
Ghi chép lại một vài câu lệnh SSH hay sử dụng.
</blockquote>

===== 1. Tạo key pair cho server =====

<code> ssh-keygen -t rsa -b 4096 </code>

-   **Chú thích**
    -   ''-t'': Chọn kiểu mã hóa
    -   ''-b'': Kích thước của key (bit)
    -   ''Passphare'': được sử dụng để mã hóa key (Nếu private key bị lộ
        nhưng không có passphare thì cũng không thể sử dụng được.) (Tùy
        chọn)

Thông thường, cặp key sẽ được lưu trữ tại thư mục ''.ssh'' trong thư mục
''home'' của user. Tên mặc định của key phụ thuộc vào thuật toán mã hóa
mà chúng ta sử dụng, trong trường hợp trên là ''id\_rsa'' và
''id\_rsa.pub''

Tùy chọn ''-f'': Đường dẫn của key sau khi tạo

<code> ssh-keygen -f \~/runsystem-key -t rsa -b 4096 </code>

===== 2. Sao chép public key sang một server khác =====

Một lệnh khá tiện lợi dùng để sao chép public key sang một máy chủ khác
và cài đặt nó thành ''authorized\_keys''

Copy key mặc định (id\_rsa.pub)

<code> ssh-copy-id -i \~/runsystem-key root\@server1 </code>

Copy key chỉ định

<code> ssh-copy-id -i \~/runsystem-key.pub root\@server1 </code>

Chú ý: \* ''\~/runsystem-key'': Đường dẫn Public key
\*''root\@server1'': User trên máy chủ mà bạn muốn sử dụng key

===== 3. Không cho phép xác thực bằng mật khẩu qua SSH =====

Mở file cấu hình của SSH

> > vi /etc/ssh/sshd\_config

<code> ... PasswordAuthentication no ... </code>

Sửa dòng ''PasswordAuthentication yes'' thành ''PasswordAuthentication
no'' và lưu lại, khởi động lại SSH.

===== 4. Không cho phép ''root'' đăng nhập qua SSH =====

Mở file cấu hình của SSH

> > vi /etc/ssh/sshd\_config

<code> ... PermitRootLogin no ... </code>

Sửa dòng ''PermitRootLogin yes'' thành ''PermitRootLogin no'' và lưu
lại, khởi động lại SSH.

===== 5. Đổi port mặc định SSH =====

Mở file cấu hình của SSH

> > vi /etc/ssh/sshd\_config

<code> ... Listen 1022 ... </code>

Sửa dòng ''Listen 22'' thành ''Listen 1022'' và lưu lại, khởi động lại
SSH.

===== 6. Truy cập bằng lệnh ssh với custom port =====

Chúng ta thêm tùy chọn ''-p <port>'' vào câu lệnh:

<code> ssh -p 1022 root\@server1 </code>

===== 7. Chuyển file qua SSH =====

-   Với port mặc định (22)

<code> scp file1 file2 root\@server1:/path/to/folder </code>

-   Với custom port

<code> scp -P 1022 file1 file2 root\@server1:/path/to/folder </code>

===== 8. Thực thi một câu lệnh qua SSH =====

<code> ssh root\@server1 'cat /etc/\*-release' </code>

===== 9. Bỏ qua bước thêm FootPrinting trong lần đầu truy cập host =====

Sử dụng flag ''StrictHostKeyChecking=no'' trong câu lệnh

<code> ssh -o StrictHostKeyChecking=no root\@server1 </code>

Hoặc chỉnh sửa trong file cấu hình (Thêm hoặc sửa)

> > vi /etc/ssh/sshd\_config

<code> ... StrictHostKeyChecking no ... </code>

Lưu lại, khởi động lại SSH.

====== 10. Tham khảo thêm ====== \
* Cấu hình file config: \*
https://www.ssh.com/ssh/config/ \*
https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client
\* More: h
