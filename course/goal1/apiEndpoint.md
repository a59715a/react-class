# Supabase API 端點文檔

## 1. 查詢所有資料 (Select All)
```bash
curl --location 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU'
```

---

## 2. 新增資料 (Insert)
```bash
curl --location 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU' \
--header 'Content-Type: application/json' \
--header 'Prefer: return=minimal' \
--data-raw '{
    "name": "測試名字",
    "email": "test@test.com",
    "password": "QQ",
    "gender": "male"
}'
```

---

## 3. 條件查詢 (Select Where)
```bash
curl --location --request GET 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*&email=eq.test%40test.com' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'select=*' \
--data-urlencode 'email=eq.test@test.com'
```