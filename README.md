# MCHAWE AI

مساعد محادثة عربي RTL بواجهة سوداء وزرقاء، يعتمد على نموذج مفتوح الأوزان **openai/gpt-oss-20b** عبر Hugging Face Inference Providers، مع اختيار أرخص مزود متاح تلقائياً (`:cheapest`).

## الملفات
- `index.html`, `style.css`, `app.js`: واجهة GitHub Pages.
- `worker/index.js`: وسيط Cloudflare Worker لحماية رمز Hugging Face.

## النشر
الموقع ينشر تلقائياً عبر GitHub Actions عند تحديث فرع `main`.

## إعداد Hugging Face
1. أنشئ رمزاً من https://huggingface.co/settings/tokens
2. امنحه صلاحية **Make calls to Inference Providers**.
3. لا تضع الرمز في ملفات الموقع أو ترسله لأي شخص.

## إعداد Cloudflare Worker
من مجلد `worker`:
```bash
npm install -g wrangler
wrangler login
wrangler secret put HF_TOKEN
wrangler deploy
```
بعد النشر أدخل رابط Worker في إعدادات الموقع (⚙).

## الحماية
عيّن متغير Worker باسم `ALLOWED_ORIGIN` إلى أصل موقع GitHub Pages فقط، مثال:
`https://kkoh2009h-gif.github.io`.
لا تضع `HF_TOKEN` في GitHub أو JavaScript بالمتصفح.

## ملاحظة التكلفة
Hugging Face يوفر رصيداً شهرياً محدوداً للحساب المجاني (تذكر صفحة الأسعار حالياً 0.10 دولار شهرياً للحساب المجاني، وقد يتغير). لذلك هذا الإعداد مناسب للتجربة والاستخدام الخفيف، وليس ضماناً لاستخدام غير محدود أو مجانياً دائماً. عند نفاد الرصيد قد يتوقف الاستدلال حتى يتجدد الرصيد أو تتم إضافة رصيد مدفوع.
