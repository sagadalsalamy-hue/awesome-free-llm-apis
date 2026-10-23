# تثبيت FreeLLMAPI على جهازك

المصدر: https://github.com/tashfeenahmed/freellmapi

يجمع الطبقات المجانية من عشرات المزودين خلف نقطة واحدة متوافقة مع OpenAI.

## الخيار 1: Docker (الأسهل، ماك/لينكس/WSL)

```bash
curl -fsSL https://freellmapi.co/install.sh | bash
```

ينشئ `~/freellmapi` ومفتاح التشفير ويشغّل الحاوية. افتح http://localhost:3001

## الخيار 2: تطبيق سطح المكتب (ويندوز / ماك)

حمّل المثبّت من: https://github.com/tashfeenahmed/freellmapi/releases/latest

## الخيار 3: من المصدر (Node 20.18+ و npm 10+)

```bash
git clone https://github.com/tashfeenahmed/freellmapi.git
cd freellmapi
npm install
printf "ENCRYPTION_KEY=%s\nPORT=3001\n" "$(node -e 'console.log(require("crypto").randomBytes(32).toString("hex"))')" > .env
npm run dev
```

## الخيار 4: أندرويد (تجريبي)

دليل Termux داخل المستودع: `docs/en/install/02-android-termux.md`

## بعد التشغيل

1. افتح http://localhost:3001 وأنشئ الحساب الأول.
2. أضف مفاتيح المزودين من صفحة **Keys**.
3. رتّب **Fallback Chain** كما تريد.
4. انسخ المفتاح الموحّد من أعلى صفحة Keys.

## الاستخدام

```bash
curl http://localhost:3001/v1/chat/completions \
  -H "Authorization: Bearer <المفتاح الموحّد>" \
  -H "Content-Type: application/json" \
  -d '{"model":"auto","messages":[{"role":"user","content":"مرحبا"}]}'
```

أو وجّه أي مكتبة OpenAI إلى `base_url=http://localhost:3001/v1`. اسم النموذج `auto` افتراضي مني، راجع وثائق المشروع (`docs/en/api/01-rest-api.md`) للقيمة الصحيحة.
