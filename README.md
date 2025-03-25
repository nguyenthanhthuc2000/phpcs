# Hướng dẫn sử dụng PHP_CodeSniffer (phpcs)

## Cài đặt
1. Cài đặt PHP_CodeSniffer và PSR-12 Coding Standard thông qua Composer:
```bash
composer require --dev squizlabs/php_codesniffer
composer require --dev slevomat/coding-standard
```

2. Cài đặt sẳn, vào thư mục cùng cấp với thư mục root chứa source code:
```bash
git clone https://github.com/nguyenthanhthuc2000/phpcs.git
cd your folder -> composer install
```

## Cách sử dụng

### 1. Kiểm tra code (phpcs)
```bash
# Kiểm tra toàn bộ code trong thư mục src
./vendor/bin/phpcs ../src

# Kiểm tra một file cụ thể
./vendor/bin/phpcs ../src/routes/web.php

# Kiểm tra với giới hạn bộ nhớ cao hơn
./vendor/bin/phpcs -d memory_limit=512M ../src

# Kiểm tra và hiển thị source code
./vendor/bin/phpcs -s ../src

# Kiểm tra và hiển thị mã lỗi
./vendor/bin/phpcs -n ../src

# Kiểm tra với màu sắc
./vendor/bin/phpcs --colors ../src
```

### 2. Tự động sửa code (phpcbf)
```bash
# Sửa toàn bộ code trong thư mục src
./vendor/bin/phpcbf ../src

# Sửa một file cụ thể
./vendor/bin/phpcbf ../src/routes/web.php

# Sửa với giới hạn bộ nhớ cao hơn
./vendor/bin/phpcbf -d memory_limit=512M ../src
```

### 3. Các tùy chọn phổ biến
```bash
# Hiển thị tiến trình kiểm tra
-p

# Hiển thị source code
-s

# Hiển thị mã lỗi
-n

# Sử dụng màu sắc
--colors

# Chỉ định chuẩn coding
--standard=PSR12

# Bỏ qua các file theo pattern
--ignore=*/vendor/*,*/node_modules/*

# Tạo file report
--report-file=report.txt
```

### 4. Ví dụ lệnh đầy đủ
```bash
# Kiểm tra với đầy đủ tùy chọn
./vendor/bin/phpcs -psn --colors --standard=PSR12 --ignore=*/vendor/*,*/node_modules/* ../src

# Sửa code với đầy đủ tùy chọn
./vendor/bin/phpcbf --standard=PSR12 --ignore=*/vendor/*,*/node_modules/* ../src
```

## Cấu hình trong phpcs.xml
```xml
<?xml version="1.0"?>
<ruleset name="PSR-12">
    <description>PSR-12 Coding Standard</description>

    <!-- Include PSR-12 -->
    <rule ref="PSR12"/>

    <!-- Paths to check -->
    <file>src</file>

    <!-- Exclude paths -->
    <exclude-pattern>*/vendor/*</exclude-pattern>
    <exclude-pattern>*/node_modules/*</exclude-pattern>

    <!-- Show progress -->
    <arg value="p"/>

    <!-- Show source codes -->
    <arg value="s"/>

    <!-- Show sniff codes in all reports -->
    <arg value="n"/>

    <!-- Use colors in output -->
    <arg name="colors"/>

    <!-- Allow . in hook file names -->
    <rule ref="Generic.Files.LineLength">
        <properties>
            <property name="lineLimit" value="120"/>
            <property name="absoluteLineLimit" value="0"/>
        </properties>
    </rule>
</ruleset>
```

## Các lỗi phổ biến và cách sửa

### 1. Lỗi khoảng trắng
```php
// Sai
$string = "Hello"."World";

// Đúng
$string = "Hello" . "World";
```

### 2. Lỗi tên method
```php
// Sai
public function get_user_data() {}

// Đúng
public function getUserData() {}
```

### 3. Lỗi khoảng trắng cuối dòng
```php
// Sai
$variable = "value";    

// Đúng
$variable = "value";
```

### 4. Lỗi use statements
```php
// Sai
use App\Models\User, App\Models\Post;

// Đúng
use App\Models\User;
use App\Models\Post;
```
