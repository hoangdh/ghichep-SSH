## Bài thực hành

### Nội dung

```
1. Viết 1 script thực hiện ssh vào 1 server khác và tạo ra 1 file với tên là test.txt.
2. Viết 1 script thực hiện copy 1 file từ server hiện tại sang server khác.
3. Viết 1 script thực hiện 1 trong  2 việc trên tới 1 Danh sách server có sẵn.

Lưu ý:
Chỉ thực hiện các chức năng nêu trên, 3 yêu cầu 3 script khác nhau.
sau khi hoàn thành, node lại gạch đầu dòng, để thực thi được cần những yêu cầu gì. Chụp lại kết quả, báo cáo qua mail.
```

### Bài thực hành:

#### Bài 1:

```sh
#!/bin/bash

ssh root@192.168.100.196 "touch ~/test.txt"
```

<img src="http://image.prntscr.com/image/1e12a26d981e415ca3bd10e9c354aa09.png" />

#### Bài 2:

```sh
#!/bin/bash

scp test.txt root@192.168.100.196:/tmp/ 
```

<img src="http://image.prntscr.com/image/4c74d63a6a28408d9e957750f5c41385.png" />

#### Bài 3:

```sh
#!/bin/bash

server=`cat server.txt`

for s in $server
do
ssh root@$s "echo a > ~/test.txt"
scp server.txt root@$s:/tmp/
ssh root@$s "ls /tmp"
done
```

Nội dung file server:

```
192.168.100.196
192.168.100.197
192.168.100.198
```

<img src="http://image.prntscr.com/image/7d909ac9b97240ebb32b6471d78e9889.png" />