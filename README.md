# فصل ۴ — کار با HTTP Request و APIها

## HTTP Request Node

قوی‌ترین Node برای اتصال به هر API که n8n اینتگریشن اختصاصی براش نداره.

### مثال: گرفتن اطلاعات آب‌وهوا

```
Method: GET
URL: https://api.open-meteo.com/v1/forecast?latitude=35.7&longitude=51.4&current_weather=true
```

خروجی به‌صورت JSON برمی‌گرده و می‌تونی توی Nodeهای بعدی ازش استفاده کنی.

## احراز هویت (Authentication)

اکثر APIها نیاز به Authentication دارن. n8n از این روش‌ها پشتیبانی می‌کنه:

| نوع | کاربرد |
|-----|--------|
| **None** | APIهای عمومی و رایگان |
| **Header Auth** | ارسال API Key در Header |
| **Basic Auth** | یوزرنیم/پسورد |
| **OAuth2** | سرویس‌هایی مثل گوگل، مایکروسافت |

نکته مهم: کلیدهای API رو همیشه توی بخش **Credentials** ذخیره کن، نه مستقیم توی URL — امن‌تره و قابل استفاده مجدده.

## پارس کردن پاسخ JSON

فرض کن پاسخ API این شکلیه:

```json
{
  "results": [
    { "id": 1, "name": "محصول الف" },
    { "id": 2, "name": "محصول ب" }
  ]
}
```

برای دسترسی به این داده در Node بعدی از expression استفاده می‌کنی:

```
{{ $json.results }}
```

## ارسال درخواست POST با بدنه‌ی JSON

```
Method: POST
Body Content Type: JSON
Body: {
  "title": "{{ $json.title }}",
  "status": "done"
}
```

## تمرین این فصل

فایل `workflow.json` این پوشه رو import کن — یه workflow که با HTTP Request به یه API عمومی وصل می‌شه و نتیجه رو فیلتر می‌کنه.

➡️ فصل بعد: [Webhookها](../05-webhooks)
