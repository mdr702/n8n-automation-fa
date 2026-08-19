# فصل ۲ — مفاهیم پایه و Nodeها

## Node چیه؟

هر **Node** یه بلوک عملیاتی توی n8n هست: می‌تونه داده بگیره، پردازش کنه، یا با یه سرویس بیرونی (مثل تلگرام یا گوگل‌شیت) صحبت کنه.

### انواع اصلی Node

| نوع | کاربرد | مثال |
|-----|--------|------|
| **Trigger** | شروع‌کننده‌ی workflow | Webhook, Schedule, Manual |
| **Regular** | پردازش/اتصال به سرویس | HTTP Request, Telegram, Google Sheets |
| **Logic** | تصمیم‌گیری و کنترل جریان | IF, Switch, Merge, Loop |
| **Data** | تغییر و شکل‌دهی داده | Set, Code, Filter |

## ساختار داده در n8n

n8n داده رو به‌صورت آرایه‌ای از آبجکت‌ها بین nodeها رد و بدل می‌کنه:

```json
[
  {
    "json": {
      "name": "علی",
      "email": "ali@example.com"
    }
  }
]
```

هر Node این آرایه رو می‌گیره، پردازش می‌کنه و آرایه‌ی جدیدی برای Node بعدی می‌فرسته.

## اتصال Nodeها (Connections)

Nodeها با خط به هم وصل می‌شن و مسیر جریان داده رو مشخص می‌کنن. می‌تونی از یه Node، چند شاخه‌ی موازی بسازی (مثلاً هم به تلگرام پیام بفرسته، هم توی گوگل‌شیت ذخیره کنه).

## Node پرکاربرد: Edit Fields (Set)

برای ساختن یا تغییر مقادیر داده استفاده می‌شه:

```
Field name: status
Field value: completed
```

## Node پرکاربرد: Code

اگه منطق پیچیده‌تری لازم داری، می‌تونی مستقیم JavaScript بنویسی:

```javascript
for (const item of $input.all()) {
  item.json.fullName = item.json.firstName + ' ' + item.json.lastName;
}
return $input.all();
```

## تمرین این فصل

فایل `workflow.json` این پوشه رو import کن — یه workflow ساده که:
1. با Manual Trigger شروع می‌شه
2. با Set دو تا فیلد می‌سازه
3. با Code اون‌ها رو ترکیب می‌کنه

➡️ فصل بعد: [Triggerها](../03-triggers)
