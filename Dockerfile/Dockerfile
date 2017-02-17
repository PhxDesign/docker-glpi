# Dockerfile: Nano Server with IIS - PHP - MySQL - WordPress.

FROM nanoserver/mysql

MAINTAINER nanoserver.es@gmail.com

ADD https://wordpress.org/latest.zip wordpress.zip

RUN MySQL --user=root --password=",<.=eiduH5Av" --connect-expired-password -Bse "ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE DATABASE wordpress CHARACTER SET utf8 COLLATE utf8_bin;" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'dbuser'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'dbuser'@'%' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `wordpress` . * TO 'dbuser'@'localhost' IDENTIFIED BY 'Password123' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `wordpress` . * TO 'dbuser'@'%' IDENTIFIED BY 'Password123' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "SHOW DATABASES;"

RUN powershell -Command \

  Expand-Archive -Path c:\wordpress.zip -DestinationPath C:\inetpub\wwwroot ; \
  ICACLS C:\inetpub\wwwroot\wordpress /INHERITANCE:R ; \
  ICACLS C:\inetpub\wwwroot\wordpress /T /C /L /Q /GRANT BUILTIN\IIS_IUSRS:F ; \
  ICACLS C:\inetpub\wwwroot\wordpress /T /GRANT Administrators:F ; \
  ICACLS C:\inetpub\wwwroot\wordpress /setowner BUILTIN\IIS_IUSRS /T /C /L /Q

RUN powershell -command rm -Recurse c:\*.zip -Force