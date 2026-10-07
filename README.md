# DevOps Hackathon – Đề 001: Quản lý phòng Lab

## 1. Thông tin sinh viên

| Họ và tên | Mã sinh viên | Lớp | Tài khoản Linux | GitHub | Cổng Nginx |
|---|---|---|---|---|---|
| Đinh Đình Thành | B24DTCN447 | K24CNTT1 | dinhdinhthanh-k24cntt1 | dinhthanh143 | 8088 |

## 2. Môi trường triển khai

- Hệ điều hành:  Debian GNU/Linux, 13 (trixie)
- Phiên bản Nginx: nginx/1.24.0
- Nơi chạy: VPS GCP
- Tài khoản: ![alt text](/screenshots/01-user.png)

## 3. Cấu trúc dự án
```text
devops-hackathon-de001-dinhthanh/
├── src/
│   └── index.html
├── nginx/
│   └── dinhdinhthanh-k24cntt1.conf
├── screenshots/
├── .gitignore
└── README.md
```

## 4. Cấu hình Nginx

- Port: 8088
- Server name: 136.86.164.31
- Web root: /var/www/devops-hackathon-de001-dinhdinhthanh/src
- Index file: index.html
- Tên tài khoản: dinhdinhthanh-k24cntt1
- Allow directive: allow all;
![alt text](/screenshots/02-nginx.png)


## 5. Tường lửa UFW

Các lệnh cấu hình:
sudo ufw allow 22/tcp
sudo ufw allow 8088/tcp
sudo ufw enable
sudo ufw status verbose
![alt text](/screenshots/03-ufw.png)


Kết quả:
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
8088/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
8088/tcp (v6)              ALLOW IN    Anywhere (v6)

## 6. Các bước triển khai

sudo useradd -m -s /bin/bash dinhdinhthanh-k24cntt1

sudo passwd dinhdinhthanh-k24cntt1

sudo usermod -aG sudo dinhdinhthanh-k24cntt1

su - dinhdinhthanh-k24cntt1

sudo apt update

sudo apt install -y nginx git ufw curl

sudo systemctl enable nginx

sudo systemctl start nginx

sudo git clone https://github.com/dinhthanh143/devops-hackathon-de001-dinhdinhthanh /var/www/devops-hackathon-de001-dinhdinhthanh

sudo chown -R dinhdinhthanh-k24cntt1:dinhdinhthanh-k24cntt1 /var/www/devops-hackathon-de001-dinhdinhthanh

find /var/www/devops-hackathon-de001-dinhdinhthanh -type d -exec chmod 755 {} \;

find /var/www/devops-hackathon-de001-dinhdinhthanh -type f -exec chmod 644 {} \;

sudo cp /var/www/devops-hackathon-de001-dinhdinhthanh/nginx/dinhdinhthanh-k24cntt1.conf /etc/nginx/sites-available/

sudo ln -s /etc/nginx/sites-available/dinhdinhthanh-k24cntt1.conf /etc/nginx/sites-enabled/

sudo rm -f /etc/nginx/sites-enabled/default

sudo nginx -t

sudo systemctl reload nginx

sudo ufw allow 22/tcp

sudo ufw allow 8088/tcp

sudo ufw enable


## 7. Kiểm tra & minh chứng



## 8. Quy trình cập nhật website

1. Sửa file `src/index.html` trên máy tính cá nhân.

2. Commit và push code lên GitHub:

git add src/index.html

git commit -m "Cập nhật lần 2 - 07/10/2026 15:45"

git push origin main

3. Trên server, cập nhật mã nguồn:

cd /var/www/devops-hackathon-de001-dinhdinhthanh

git pull origin main

4. Kiểm tra lại trên trình duyệt không cần reload Nginx.

## 9. Sự cố gặp phải & cách khắc phục (nếu có)

Không có

## 10. Git log
![alt text](/screenshots/05-git-log.png)
