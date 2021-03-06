# HƯỚNG DẪN TẠO SERVER LOCAL

- Để chạy localhost, ta cần cài đặt:

[Xampp v7.3.18 x64](https://www.apachefriends.org/xampp-files/7.3.18/xampp-windows-x64-7.3.18-0-VC15-installer.exe)
[Xampp v7.3.2 x32](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/7.3.2/xampp-portable-win32-7.3.2-0-VC15-installer.exe/download)

- **Bước 0:** Đưa php vào system path:

  - Nhấn phím windows, nhập “path” để tìm Edit the system environment variable:

  ![local01](pictures/local01.png)

  - Chọn Environment Variables:

  ![local02](pictures/local02.png)

  - Chọn path > Edit:

  ![local03](pictures/local03.png)

  - Chọn New, điền vào C:\xampp\php

  ![local04](pictures/local04.png)

  - Chọn OK để save lại.

- **Bước 1:** Giải nén file card_scanner.zip(\web_server\local\) và chép thư mục card_scanner vào thư mục C:\xampp\htdocs.
- **Bước 2:** Khởi động phần mềm Xampp để tạo môi trường cho Localhost. Nhấn Start cho Apache và MySQL.

![local05](pictures/local05.png)

- **Bước 3:** truy cập <http://localhost/phpmyadmin> để vào trang quản lý Database.
  - Tạo new database với tên countstd:

  ![local06](pictures/local06.png)

  - Import database có sẵn vào database vừa được tạo, chọn import:

  ![local07](pictures/local07.png)

  - Chọn Choose file và chọn vào file countstd.sql (\web_server\local\) > Bấm Go ở cuối trang

  ![local08](pictures/local08.png)

- **Bước 4:** Mặc định, hệ thống đã có tài khoản admin. Nếu muốn thay đổi tài khoản admin, xóa admin cũ trong bảng admin từ database countstd trong phpMyAdmin, sau đó truy cập vào tệp tin _DatabaseSeeder.php_ theo đường dẫn C:\xampp\htdocs\card_scanner\database\seeds. Thay đổi thông tin tài khoản đăng nhập mong muốn:

```python
class seedAdmin extends Seeder
{
    public function run()
    {
        DB::table('admin')->insert([
            ['taikhoan' => 'tên đăng nhập ở đây', 'password' => bcrypt('Mật khẩu ở đây')],
            ['taikhoan' => 'admin', 'password' => bcrypt('123456')],
        ]);
    }
}
```

- **Bước 5:** Mở cmd, gõ vào:

```bash
cd C:\xampp\htdocs\card_scanner
```

- **Bước 6:** Thực thi thay đổi cơ sở dữ liệu (LƯU Ý: nếu gặp lỗi, thì kiểm tra lại bảng admin từ database và đảm bảo không có tài khoản admin bị trùng):

```bash
php artisan db:seed
```

- **Bước 7:** Tiến hành chạy server:

```bash
php artisan serve --port=2020
```

![local09](pictures/local09.png)

- **Bước 8:** Truy cập _<http://localhost:2020>_ hoặc nhấp đúp vào shortcut _Card Scanner Web Server_ (C:\xampp\htdocs\card_scanner) để truy cập hệ thống.
