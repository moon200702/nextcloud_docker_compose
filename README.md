Nextcloud Docker Compose 使用說明
================================

這份設定會啟動一套基礎的 Nextcloud 服務，包含：
- Nextcloud 網頁介面
- PostgreSQL 資料庫
- Redis 快取
- Cron 背景任務
- Collabora 線上文件協作

1. 先確認 Docker 已安裝
-------------------------
請先確認 Docker 與 Docker Compose 可以正常使用：

  docker --version
  docker compose version

2. 進入資料夾
-------------

  cd /workspaces/CsvCompareApp/nextcloud

3. 建立環境變數檔案（建議）
----------------------------
你可以建立一個 .env 檔案，填入以下內容：

  POSTGRES_DB=nextcloud
  POSTGRES_USER=nextcloud
  POSTGRES_PASSWORD=請換成強式密碼
  REDIS_PASSWORD=請換成強式密碼
  NEXTCLOUD_ADMIN_USER=admin
  NEXTCLOUD_ADMIN_PASSWORD=請換成強式密碼
  NEXTCLOUD_HOST=localhost
  COLLABORA_DOMAIN=.*
  COLLABORA_ALIASGROUP1=https://.*:443
  COLLABORA_USERNAME=admin
  COLLABORA_PASSWORD=請換成強式密碼

4. 啟動服務
-----------

  docker compose up -d

5. 查看服務狀態
---------------

  docker compose ps

6. 查看日誌
-----------

  docker compose logs -f nextcloud

7. 開啟 Nextcloud
-----------------
在瀏覽器開啟：

  http://localhost:8080

預設管理員帳號為你在 .env 裡設定的 NEXTCLOUD_ADMIN_USER 與 NEXTCLOUD_ADMIN_PASSWORD。

8. 停止服務
-----------

  docker compose down

9. 移除資料（會刪除所有資料）
--------------------------------
若你想清空所有資料與容器，請使用：

  docker compose down -v

10. 注意事項
------------
- 請務必修改預設密碼，避免安全風險。
- 如果你要正式上線，建議再加上 HTTPS、反向代理與備份機制。
- Collabora 需要正確的網域設定，若你要正式使用建議改成實際網域。
