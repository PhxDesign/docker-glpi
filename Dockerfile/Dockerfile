FROM nanoserver/mysql
MAINTAINER nanoserver.es@gmail.com

ADD https://github.com/glpi-project/glpi/releases/download/9.5.5/glpi-9.5.5.tgz glpi.tgz

RUN MySQL --user=root --password="2v3%ZRe#vHhG" --connect-expired-password -Bse "ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE DATABASE glpi_p CHARACTER SET utf8 COLLATE utf8_bin;" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'glpi'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'glpi'@'%' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `glpi_p` . * TO 'glpi'@'localhost' IDENTIFIED BY 'Password123' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `glpi_p` . * TO 'glpi'@'%' IDENTIFIED BY 'Password123' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "SHOW DATABASES;"

RUN powershell -Command \
  Expand-Archive -Path c:\glpi.tgz -DestinationPath C:\inetpub\wwwroot ; \
  ICACLS C:\inetpub\wwwroot\glpi /INHERITANCE:R ; \
  ICACLS C:\inetpub\wwwroot\glpi /T /C /L /Q /GRANT BUILTIN\IIS_IUSRS:F ; \
  ICACLS C:\inetpub\wwwroot\glpi /T /GRANT Administrators:F ; \
  ICACLS C:\inetpub\wwwroot\glpi /setowner BUILTIN\IIS_IUSRS /T /C /L /Q
RUN powershell -command rm -Recurse c:\*.tgz -Force
