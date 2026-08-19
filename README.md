# فصل ۵ — Webhookها

## Webhook چیه؟

Webhook یه URL هست که n8n بهت می‌ده و وقتی یه سرویس بیرونی (فرم سایت، سیستم پرداخت، اپلیکیشن دیگه) به اون URL درخواست بفرسته، workflow تو خودکار اجرا می‌شه.

## ساخت یه Webhook ساده

1. یه Node به اسم **Webhook** اضافه کن
2. `HTTP Method` رو روی `POST` بذار
3. یه `Path` دلخواه انتخاب کن، مثلاً `new-order`
4. n8n دو تا URL بهت می‌ده:
   - **Test URL**: برای توسعه و تست
   - **Production URL**: برای استفاده‌ی واقعی (بعد از فعال‌سازی/publish کردن workflow)

## مثال کاربردی: اتصال فرم سایت به n8n

فرض کن فرم تماس سایتت داده رو به این شکل POST می‌کنه:

```json
{
  "name": "سارا احمدی",
  "email": "sara@example.com",
  "message": "سلام، سوال دارم"
}
```

با Webhook Node این داده رو می‌گیری و می‌تونی:
- توی گوگل‌شیت ذخیره‌ش کنی
- پیام تلگرام بفرستی
- ایمیل خودکار جواب بدی

## امنیت Webhook

- از **Header Auth** برای محدود کردن دسترسی به Webhook استفاده کن
- IP سرویس مبدا رو (در صورت امکان) با Node شرطی (IF) بررسی کن
- هیچ‌وقت داده‌ی حساس رو بدون اعتبارسنجی مستقیم به دیتابیس نفرست

## پاسخ دادن به Webhook

با Node **Respond to Webhook** می‌تونی یه پاسخ سفارشی (مثلاً `{"status": "ok"}`) به فرستنده‌ی درخواست برگردونی.

## تمرین این فصل

فایل `workflow.json` این پوشه رو import کن، Webhook رو فعال کن و با ابزاری مثل Postman یا curl یه درخواست تست بفرست:

```bash
curl -X POST http://localhost:5678/webhook-test/new-order \
  -H "Content-Type: application/json" \
  -d '{"name": "تست", "email": "test@example.com"}'
```

➡️ فصل بعد: [پروژه‌های واقعی](../06-real-world-projects)
