# 🛠️ دليل بناء Vencord / Equicord من السورس وتثبيت البلوقنات الخارجية
# Building Vencord / Equicord from Source & Installing External Plugins

> هذا الدليل ثنائي اللغة (عربي / إنجليزي) موجّه للمستخدمين والمطورين الذين يريدون بناء نسخة مخصصة من **Vencord** أو **Equicord** من الكود المصدري، وتثبيت بلوقنات (إضافات) خارجية غير موجودة رسميًا في المشروع.
>
> This bilingual (Arabic / English) guide is for users and developers who want to build a custom version of **Vencord** or **Equicord** from source, and install external/community plugins not included officially in the project.

---

## ⚠️ تنبيه مهم | Important Disclaimer

**عربي:** تعديل عميل ديسكورد عبر "Client Mods" مثل Vencord و Equicord يُعتبر مخالفًا لشروط استخدام Discord (ToS)، وقد يعرّض الحساب لخطر الإيقاف بنسبة منخفضة لكنها موجودة. استخدم هذه البلوقنات على مسؤوليتك الخاصة، وتجنّب البلوقنات التي تتدخل في طريقة عمل خوادم Discord الرسمية (مثل سبام، أو تجاوز حماية).

**English:** Using Discord client mods such as Vencord and Equicord goes against Discord's Terms of Service, and there is a small but real risk of account action. Use these tools at your own risk, and avoid plugins that interfere with Discord's servers (e.g. spam tools or anti-detection bypasses).

---

## 📦 الجزء الأول: المتطلبات الأساسية | Part 1: Prerequisites

قبل البدء، تأكد من تثبيت الأدوات التالية على نظامك (Windows / macOS / Linux):

Before starting, make sure the following tools are installed on your system (Windows / macOS / Linux):

| الأداة / Tool | الوصف / Description | الرابط الرسمي / Official Link |
|---|---|---|
| **Git** | لإستنساخ (clone) السورس كود / Used to clone the source code | https://git-scm.com/downloads |
| **Node.js (LTS)** | بيئة تشغيل JavaScript المطلوبة للبناء / Required JS runtime for building | https://nodejs.org |
| **pnpm** | مدير الحزم المستخدم في المشروع (لا تستخدم npm أو yarn) / Package manager used by the project (do NOT use npm or yarn) | يُثبَّت بالأمر / Install with: `npm i -g pnpm` |

**عربي:** بعد تثبيت Node.js، افتح الـ Terminal (أو CMD/PowerShell في ويندوز) ونفّذ الأمر التالي لتثبيت pnpm:

**English:** After installing Node.js, open your terminal (or CMD/PowerShell on Windows) and run the following command to install pnpm:

```bash
npm i -g pnpm
```

> ⚠️ **مستخدمو ويندوز:** لا تشغّل أي من الأوامر التالية في Terminal مفتوح بصلاحيات Administrator، لأن ذلك قد يكسر تثبيت Discord.
>
> ⚠️ **Windows users:** Do NOT run any of the following commands in an Administrator terminal — this can break your Discord installation.

---

## 🚀 الجزء الثاني: بناء Vencord من السورس | Part 2: Building Vencord from Source

### 1️⃣ استنساخ المستودع | Cloning the repository

**عربي:** اختر مجلدًا تتذكره (مثل Documents)، ثم نفّذ:

**English:** Choose a memorable folder (e.g. Documents), then run:

```bash
cd "%USERPROFILE%/Documents"     # Windows
cd "$HOME/Documents"             # Linux / macOS

git clone https://github.com/Vencord/Vencord
cd Vencord
```

### 2️⃣ تثبيت الاعتماديات | Installing dependencies

```bash
pnpm install --no-frozen-lockfile
```

### 3️⃣ بناء المشروع | Building the project

```bash
pnpm build
```

**عربي:** إذا كنت تريد بناء نسخة تطويرية (Dev Build) تتيح لك أدوات إضافية مثل PatchHelper، استخدم:

**English:** If you want a Development Build with extra tools like PatchHelper, use:

```bash
pnpm build --dev
```

### 4️⃣ حقن (Inject) النسخة المبنية في Discord | Injecting your build into Discord

```bash
pnpm inject
```

اتبع التعليمات التي تظهر على الشاشة لاختيار نسخة Discord المراد تعديلها (Stable / Canary / PTB).

Follow the on-screen prompts to choose which Discord installation (Stable / Canary / PTB) to patch.

### 5️⃣ التحديث التلقائي عند التطوير | Auto-rebuild while developing

```bash
pnpm build --watch
```

**عربي:** هذا الأمر يعيد البناء تلقائيًا كل ما عدّلت في الكود — مفيد جدًا أثناء تطوير البلوقنات.

**English:** This command rebuilds automatically every time you edit the code — very useful while developing plugins.

---

## 🧩 الجزء الثالث: تثبيت بلوقنات خارجية (User Plugins) في Vencord | Part 3: Installing External Plugins (User Plugins)

**عربي:** البلوقنات الرسمية موجودة في `src/plugins`، لكنها مرتبطة بـ Git الأساسي، ولا يُفضّل وضع بلوقناتك الخارجية فيها لتجنب التعارضات. بدلًا من ذلك نستخدم مجلد `src/userplugins`.

**English:** Official plugins live in `src/plugins`, but it's tracked by the main Git repo, so external plugins shouldn't go there to avoid conflicts. Instead, we use the `src/userplugins` folder.

### الخطوات | Steps

1. **عربي:** افتح مجلد Vencord الذي استنسخته، ثم انتقل إلى مجلد `src`.
   **English:** Open your cloned Vencord folder, then go into the `src` directory.

2. **عربي:** أنشئ مجلدًا جديدًا اسمه `userplugins` (إن لم يكن موجودًا).
   **English:** Create a new folder named `userplugins` (if it doesn't exist).

```bash
cd src
mkdir userplugins
cd userplugins
```

3. **عربي:** لتثبيت بلوقن خارجي عبر Git، استنسخه داخل هذا المجلد. مثال:
   **English:** To install an external plugin via Git, clone it inside this folder. Example:

```bash
git clone https://github.com/D3SOX/vc-betterActivities
```

   **عربي:** أو إذا حمّلت البلوقن كملف ZIP من GitHub، فضع المجلد الناتج مباشرة داخل `src/userplugins/`، بحيث يحتوي على ملف `index.ts` أو `index.tsx` كنقطة الدخول.

   **English:** Or, if you downloaded the plugin as a ZIP from GitHub, place the extracted folder directly inside `src/userplugins/`, making sure it contains an `index.ts` or `index.tsx` entry file.

4. **عربي:** أعد بناء Vencord:
   **English:** Rebuild Vencord:

```bash
pnpm build
```

5. **عربي:** أعد تشغيل Discord بالكامل (إغلاق كامل من Task Manager / Activity Monitor ثم إعادة فتح) لتظهر البلوقنات الجديدة في تبويب Vencord بإعدادات Discord.

   **English:** Fully restart Discord (close it completely from Task Manager / Activity Monitor, then reopen) so the new plugins appear in the Vencord tab of Discord settings.

### ملاحظات مهمة | Important Notes

- **عربي:** أوامر `git fetch` و `git pull` تُحدّث Vencord نفسه فقط، وليس البلوقنات الخارجية. لتحديث بلوقن خارجي، عليك تحميل النسخة الجديدة وإعادة استبدال الملفات يدويًا، أو دخول مجلد البلوقن وتشغيل `git pull` إذا كان مستنسخًا بـ Git.

- **English:** `git fetch` and `git pull` only update Vencord itself, not your external plugins. To update an external plugin, download the new version and replace the files manually, or `cd` into the plugin folder and run `git pull` if it was cloned with Git.

- **عربي:** إذا ظهرت أخطاء حول حزم مفقودة بعد إضافة بلوقن جديد، شغّل `pnpm install --no-frozen-lockfile` مرة أخرى ثم أعد البناء.

- **English:** If you get "missing package" errors after adding a new plugin, run `pnpm install --no-frozen-lockfile` again, then rebuild.

---

## 🌀 الجزء الرابع: بناء Equicord من السورس | Part 4: Building Equicord from Source

**عربي:** Equicord هو نسخة مطوّرة (Fork) من Vencord تحتوي على أكثر من 300 بلوقن إضافي، وخطوات بنائه تكاد تكون مطابقة لـ Vencord.

**English:** Equicord is a fork of Vencord with 300+ additional plugins, and the build process is nearly identical to Vencord's.

### 1️⃣ الاستنساخ | Cloning

```bash
cd "$HOME/Documents"   # or "%USERPROFILE%/Documents" on Windows

git clone https://github.com/Equicord/Equicord
cd Equicord
```

### 2️⃣ التثبيت والبناء | Install & Build

```bash
pnpm install --no-frozen-lockfile
pnpm build
```

**عربي:** لتفعيل وضع التطوير (Developer-only plugins + أدوات تصحيح مثل PatchHelper):

**English:** To enable Developer-only plugins and debug tools like PatchHelper:

```bash
pnpm build --dev
```

### 3️⃣ الحقن | Injection

```bash
pnpm inject
```

> 💡 **عربي:** ملاحظة من الوثائق الرسمية: إذا كنت لا تنوي التطوير أو استخدام بلوقنات مخصصة (User Plugins)، فلا حاجة فعلية لبناء Equicord من السورس — يمكنك استخدام Equilotl (المثبّت الجاهز) أو Equibop (عميل مستقل يحتوي Equicord مسبقًا).
>
> 💡 **English:** Note from the official docs: unless you plan to develop or use custom user plugins, there's no real need to build Equicord from source — you can use Equilotl (the pre-built installer) or Equibop (a standalone client with Equicord pre-installed).

---

## 🧩 الجزء الخامس: تثبيت بلوقنات خارجية في Equicord | Part 5: Installing External Plugins in Equicord

**عربي:** الطريقة مطابقة تمامًا لـ Vencord:

**English:** The process is identical to Vencord:

1. انتقل إلى / Go to `src/userplugins` (أنشئه إن لم يكن موجودًا / create it if it doesn't exist).
2. ضع كل بلوقن في مجلد خاص به، بحيث يحتوي على `index.ts` أو `index.tsx` كنقطة دخول.
   Place each plugin in its own folder with an `index.ts` or `index.tsx` entry point.
3. أعد البناء / Rebuild:

```bash
pnpm build
```

4. أعد تشغيل Discord أو Equibop بالكامل / Fully restart Discord or Equibop.

**عربي:** يمكنك أيضًا استخدام `pnpm watch` بدلًا من `pnpm build` أثناء التطوير، حيث يعيد البناء تلقائيًا مع كل تعديل، مع الضغط على `Ctrl+R` داخل Discord لتحميل التغييرات إذا كنت تستخدم Code Patches.

**English:** During development you can also use `pnpm watch` instead of `pnpm build` — it rebuilds automatically on every change, and you can press `Ctrl+R` inside Discord to reload changes when using code patches.

---

## 🔗 روابط تعليمية رسمية | Official Documentation Links

### Vencord

- 📘 الموقع الرسمي للوثائق / Official Docs: https://docs.vencord.dev
- 🛠️ دليل البناء من السورس / Installing from Source: https://docs.vencord.dev/installing/
- 🧩 دليل تثبيت البلوقنات الخارجية / Installing Custom Plugins: https://docs.vencord.dev/installing/custom-plugins/
- 👨‍💻 دليل إنشاء البلوقنات / Creating Plugins: https://docs.vencord.dev/plugins/
- 📂 المستودع الرسمي / Official Repository: https://github.com/Vencord/Vencord
- 🌐 قائمة البلوقنات الرسمية / Official Plugin List: https://vencord.dev/plugins

### Equicord

- 📘 الموقع الرسمي للوثائق / Official Docs: https://docs.equicord.org
- 🚀 نقطة الانطلاق / Getting Started: https://docs.equicord.org/getting-started
- 🛠️ دليل البناء من السورس / Building from Source: https://docs.equicord.org/building-from-source
- 🧩 دليل تثبيت بلوقنات المستخدم / Installing User Plugins: https://docs.equicord.org/plugins
- 💻 دليل التثبيت العام / Installation Guide: https://docs.equicord.org/installation
- 📂 المستودع الرسمي / Official Repository: https://github.com/Equicord/Equicord
- 🌙 Equibop (عميل مستقل / standalone client): https://equibop.org

---

## ✅ خلاصة سريعة | Quick Summary

**عربي:**
1. ثبّت Git و Node.js و pnpm.
2. استنسخ مستودع Vencord أو Equicord من GitHub.
3. شغّل `pnpm install --no-frozen-lockfile` ثم `pnpm build`.
4. شغّل `pnpm inject` لربطه بـ Discord.
5. ضع أي بلوقن خارجي داخل `src/userplugins`، أعد البناء، وأعد تشغيل Discord.

**English:**
1. Install Git, Node.js, and pnpm.
2. Clone the Vencord or Equicord repository from GitHub.
3. Run `pnpm install --no-frozen-lockfile` then `pnpm build`.
4. Run `pnpm inject` to patch your Discord client.
5. Place any external plugin inside `src/userplugins`, rebuild, and restart Discord.

---

*هذا الدليل لأغراض تعليمية فقط، ويعتمد على الوثائق الرسمية لكل من Vencord و Equicord بتاريخ يونيو 2026.*

*This guide is for educational purposes only, based on the official Vencord and Equicord documentation as of June 2026.*
