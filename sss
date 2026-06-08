#!/bin/bash

# 1. Обновление пакетов и установка зависимостей
echo "=== Установка пакетов (HTTPD, SAMBA, PHP, OPENSSL) ==="
yum install -y httpd samba samba-client php openssl

# 2. Создание структуры каталогов
echo "=== Настройка директорий ==="
mkdir -p /var/www/html/files
chmod -R 755 /var/www/html
chown -y apache:apache /var/www/html

# 3. Настройка Samba (доступ к каталогу /var/www/html/)
echo "=== Настройка Samba ==="
cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

cat <<EOF >> /etc/etc/samba/smb.conf

[www_html]
    path = /var/www/html
    writable = yes
    browseable = yes
    guest ok = yes
    create mask = 0775
    directory mask = 0775
    force user = apache
EOF

# 4. Настройка SELinux (критично для CentOS, чтобы Samba и Apache не ругались)
echo "=== Настройка SELinux ==="
setsebool -P httpd_enable_homedirs on 2>/dev/null
setsebool -P samba_export_all_rw on 2>/dev/null
chcon -R -t httpd_sys_rw_content_t /var/www/html/

# 5. Создание веб-сайта (index.php) для вывода списка файлов
echo "=== Создание веб-страницы ==="
cat <<'EOF' > /var/www/html/index.php
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Скачивание зашифрованных файлов</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        ul { list-style-type: none; padding: 0; }
        li { margin: 10px 0; padding: 10px; background: #f4f4f4; border-radius: 4px; }
        a { text-decoration: none; color: #0066cc; font-weight: bold; }
    </style>
</head>
<body>
    <h2>Список зашифрованных файлов для скачивания:</h2>
    <ul>
    <?php
    $dir = "/var/www/html/files/";
    if (is_dir($dir)) {
        if ($dh = opendir($dir)) {
            while (($file = readdir($dh)) !== false) {
                if ($file != "." && $file != "..") {
                    echo "<li>📎 <a href='files/" . htmlspecialchars($file) . "' download>" . htmlspecialchars($file) . "</a></li>";
                }
            }
            closedir($dh);
        }
    }
    ?>
    </ul>
</body>
</html>
EOF

# 6. Открытие портов в FirewallD
echo "=== Настройка FirewallD ==="
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=samba
firewall-cmd --reload

# 7. Запуск и добавление служб в автозагрузку
echo "=== Запуск сервисов ==="
systemctl enable --now httpd
systemctl enable --now smb
systemctl enable --now nmb

echo "======================================================="
echo " Настройка успешно завершена!"
echo " Веб-сайт доступен по адресу: http://<IP_вашей_виртуалки>/"
echo " Samba-шара доступна по адресу: \\\\<IP_вашей_виртуалки>\\www_html"
echo "======================================================="
