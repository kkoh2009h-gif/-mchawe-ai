# MCHAWE AI

واجهة دردشة عربية RTL بتصميم أسود وأزرق، تستخدم نموذج Hugging Face:
`OBLITERATUS/gemma-4-E4B-it-OBLITERATED` عبر Inference Providers (Featherless AI).

## الملفات
- `index.html`, `style.css`, `app.js`: واجهة GitHub Pages.
- `worker/index.js`: وسيط Cloudflare Worker لحماية رمز Hugging Face.

## نشر الواجهة
1. ارفع الملفات إلى جذر المستودع.
2. افتح Settings → Pages.
3. اختر Deploy from a branch ثم `main` و`/(root)`.

## إعداد Hugging Face
1. أنشئ رمزاً من https://huggingface.co/settings/tokens
2. امنحه صلاحية Make calls to Inference Providers.
3. لا تضع الرمز في ملفات الموقع أو ترسله لأي شخص.

## نشر Cloudflare Worker
من مجلد worker نفّذ:
```bash
npm install -g wrangler
wrangler login
wrangler secret put HF_TOKEN
wrangler deploy
```
بعد النشر أدخل رابط Worker في إعدادات الموقع (⚙).

## الحماية
بعد معرفة عنوان GitHub Pages، عيّن متغير Worker باسم `ALLOWED_ORIGIN` إلى أصل موقعك فقط، مثال:
`https://YOUR-USERNAME.github.io`.
لا تضع HF_TOKEN في GitHub أو JavaScript بالمتصفح.

ملاحظة: استخدام Inference Providers قد يتطلب رصيداً أو فوترة، وتوفر Featherless للنموذج ليس مضموناً دائماً.
