![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white) ![Celery](https://img.shields.io/badge/Celery-37814A?style=for-the-badge&logo=celery&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Pourya Mohamadi — Python Developer (Backend & Systems)

Self-taught Python developer. I design, build, deploy, and operate production systems end to end: multi-brand Django e-commerce platforms serving real customers, a risk-first cryptocurrency trading bot, and packaged Python SDKs. Currently focused on trading-system architecture, automated testing, and security engineering.

---

## What I build

### Trading systems (Python · 2026)
Author of an adaptive trading bot for the Bitpin exchange (~24k LOC, ~100 modules):

- **Layered architecture** — exchange adapters normalize REST payloads into frozen domain dataclasses; strategy, risk, persistence, and execution never touch provider JSON directly.
- **Explainable strategy engine** — deterministic multi-timeframe signals (EMA trend, MACD momentum, ATR volatility, volume filters) that carry a score, confidence, regime, and human-readable reasons for every component.
- **Risk engine** — daily/monthly drawdown kill switches persisted to PostgreSQL so restarts cannot reset them; `Decimal` money math; hard blockers that always override signals.
- **Exchange client** — HMAC-signed auth with managed token lifecycle, per-endpoint rate limiting, circuit breaker, and order execution gated off by default (simulation-first; live requires explicit config + admin approval).
- **Tooling around it** — backtesting with walk-forward splits, feature/label dataset pipeline for learning from past trades, and a read-only FastAPI + Jinja2 dashboard.
- **Tested** — 369 pytest tests across 37 files (fakes, monkeypatching, DB-backed fixtures).

### Production web platforms (Django · 2023–2026)
Built and operate real revenue-generating platforms as a solo developer:

- **E-commerce across multiple brands** — catalogs, session carts with variant/color handling, orders, coupons/discount codes, invoicing (PDF), and admin tooling.
- **Service-business platform (Lidoma HVAC)** — booking/order flow, staff area, custom email-based user model, sitemaps/SEO, and Celery pipelines for transactional email, nightly `pg_dump` backups to Google Cloud Storage, and Google Reviews fetching with Redis caching.
- **LLM content pipeline** — scheduled OpenAI-driven blog writing with structured prompts, JSON response parsing, similarity-based dedup against existing posts, and automated Pexels image sourcing.
- **Real-world integrations** — Iranian payment gateways (Zibal, bank gateway package, Torob BNPL flow with verify/settle/revert), SMS.ir notifications, Instagram posting automation, Google OAuth sign-in, PostEx shipping rates.

### Packaged Python SDKs
- **[pexels-python](https://github.com/Stink-Po/pexels-python)** — a typed Pexels API wrapper: Pydantic input validation on every call, response analyzer, hatchling packaging with src layout, and its own test suite.
- **[boxoffice_api](https://github.com/Stink-Po/boxoffice_api)** — Box Office Mojo data library: requests + BeautifulSoup scraping into pandas DataFrames with thread-pool concurrency, packaged for PyPI via a GitHub Actions release workflow.

---

## Skills (backed by shipped code)

| Area | What I actually use |
|---|---|
| **Languages** | Python (primary), JavaScript, HTML/CSS/SCSS |
| **Web frameworks** | Django 5 (custom user models/managers, CMS/blog, carts, orders, admin), FastAPI (app factory, routers, Jinja2 dashboard) |
| **Data & ORM** | PostgreSQL, SQLAlchemy 2 + Alembic migrations, Django ORM, Redis, RabbitMQ |
| **Async & jobs** | Celery workers + django_celery_beat schedules |
| **DevOps & deploy** | Docker Compose production stacks (nginx TLS via certbot, gunicorn gevent workers, resource limits), Linux VPS administration, Google Cloud Storage |
| **Testing** | pytest at scale in the trading bot; test suites in published packages |
| **Integrations** | Payment gateways (Zibal / bank gateways / Torob), SMS.ir, Instagram API, Google OAuth/Reviews/Storage, OpenAI API, shipping APIs |
| **Trading domain** | Exchange REST/HMAC auth, rate limiting, order lifecycle, drawdown risk controls, backtesting, feature/label engineering |

## How I work

- Secrets live in environment config only (`.env` + pydantic-settings / python-decouple); every repo ships a `.env.example`; dependencies pinned.
- Safety-first defaults in anything touching money: paper/simulation mode default, master kill switch, persistent drawdown halts, `Decimal` for money, positions recorded only after verified fills.
- Explainability as a feature: trading signals and risk decisions carry their reasons; dashboards are read-only by default.
- Domain isolation: provider-specific formats are normalized at the boundary and never leak inward.

## Currently improving

- **Automated testing for web apps** — strong discipline in the trading bot; extending it to Django projects.
- **Security engineering** — secrets hygiene, endpoint auth, and least-privilege containers are a deliberate, active focus area.
- **CI everywhere** — GitHub Actions release automation today; rolling out test pipelines across all active repos.

## Trajectory

- **2022** — first Python programs: CLI tools, translators, small automation.
- **2023** — algorithms and games (minimax tic-tac-toe AI, pygame), first Django applications.
- **2023–2024** — multi-brand Django e-commerce in production: payments, shipping, SMS, coupons.
- **2025–2026** — production platforms with Celery/LLM/Instagram pipelines, published Python packages, and a risk-first trading system with layered architecture, persistent risk controls, and a real test suite.

## Selected public repositories

- [pexels-python](https://github.com/Stink-Po/pexels-python) — Pydantic-validated Pexels API SDK
- [boxoffice_api](https://github.com/Stink-Po/boxoffice_api) — box office data scraper library
- [tictoctoi_with_AI](https://github.com/Stink-Po/tictoctoi_with_AI) — tic-tac-toe with minimax AI

*(Production platforms and the trading bot live in private repositories.)*

## Contact

- Email: fresh.pourya@gmail.com
- LinkedIn: [pourya-mohamadi](https://www.linkedin.com/in/pourya-mohamadi/)

---

---

# پوریا محمدی — توسعه‌دهنده پایتون (بک‌اند و سیستم‌ها)

توسعه‌دهنده پایتون خودآموخته. طراحی، پیاده‌سازی، دیپلوی و نگه‌داری سیستم‌های پروداکشن را به‌صورت کامل انجام می‌دهم: پلتفرم‌های فروشگاهی جنگو برای چند برند واقعی، ربات معامله‌گری ارز دیجیتال با رویکرد «اول ایمنی»، و کتابخانه‌های پایتون بسته‌بندی‌شده. تمرکز فعلی: معماری سیستم‌های معامله‌گری، تست خودکار، و مهندسی امنیت.

---

## چه چیزی می‌سازم

### سیستم‌های معامله‌گری (پایتون · ۲۰۲۶)
نویسنده ربات معامله‌گری تطبیقی برای صرافی بیت‌پین (~۲۴ هزار خط کد، ~۱۰۰ ماژول):

- **معماری لایه‌ای** — آداپترهای صرافی پاسخ‌های REST را به دیتاکلاس‌های تغییرناپذیر (frozen) نرمال‌سازی می‌کنند؛ لایه‌های استراتژی، ریسک، persistence و اجرا هرگز با JSON اختصاصی صرافی سروکار ندارند.
- **موتور استراتژی قابل توضیح** — سیگنال‌های قطعی چند‌تایم‌فریمی (روند EMA، مومنتوم MACD، نوسان ATR، فیلتر حجم) که برای هر مؤلفه امتیاز، اطمینان، رژیم بازار و دلیل قابل‌خواندن ارائه می‌دهند.
- **موتور ریسک** — کلیدهای توقف (kill switch) افت روزانه/ماهانه که در PostgreSQL ذخیره می‌شوند تا ری‌استارت نتواند آن‌ها را ریست کند؛ محاسبات مالی با `Decimal`؛ بلاکرهای سخت که همیشه بر سیگنال اولویت دارند.
- **کلاینت صرافی** — احراز هویت HMAC با مدیریت چرخه توکن، rate limiting برای هر endpoint، circuit breaker، و اجرای سفارش به‌صورت پیش‌فرض غیرفعال (اول شبیه‌سازی؛ معامله واقعی نیازمند تنظیمات صریح + تأیید ادمین).
- **ابزارهای پیرامون** — بک‌تست با walk-forward، خط تولید دیتاست ویژگی/برچسب برای یادگیری از معاملات گذشته، و داشبورد فقط‌خواندنی با FastAPI و Jinja2.
- **تست‌شده** — ۳۶۹ تست pytest در ۳۷ فایل (fake ها، monkeypatching، fixture های متصل به دیتابیس).

### پلتفرم‌های وب پروداکشن (جنگو · ۲۰۲۳–۲۰۲۶)
ساخت و نگه‌داری پلتفرم‌های واقعی درآمدزا به‌صورت انفرادی:

- **فروشگاه اینترنتی برای چند برند** — کاتالوگ، سبد خرید سشنی با مدیریت رنگ/وارینت، سفارش‌ها، کد تخفیف، فاکتور PDF و ابزارهای ادمین.
- **پلتفرم خدمات (Lidoma — تأسیسات HVAC)** — فرآیند رزرو/سفارش، پنل کارکنان، مدل کاربر سفارشی مبتنی بر ایمیل، sitemap/سئو، و خطوط Celery برای ایمیل تراکنشی، بکاپ شبانه `pg_dump` روی Google Cloud Storage، و دریافت نظرات گوگل با کش Redis.
- **خط تولید محتوا با LLM** — نوشتن خودکار وبلاگ با OpenAI و پرامپت ساختاریافته، پارس JSON، حذف تکرار بر اساس شباهت، و تأمین خودکار تصویر از Pexels.
- **یکپارچه‌سازی‌های واقعی** — درگاه‌های پرداخت ایرانی (زیبال، پکیج درگاه بانکی، خرید اعتباری ترب با verify/settle/revert)، نوتیفیکیشن SMS.ir، اتوماسیون اینستاگرام، ورود با گوگل، نرخ ارسال پست.

### کتابخانه‌های پایتون بسته‌بندی‌شده
- **[pexels-python](https://github.com/Stink-Po/pexels-python)** — wrapper تایپ‌شده API پکسلز: اعتبارسنجی ورودی با Pydantic در هر فراخوان، تحلیلگر پاسخ، بسته‌بندی hatchling با ساختار src، و تست اختصاصی.
- **[boxoffice_api](https://github.com/Stink-Po/boxoffice_api)** — کتابخانه داده‌های باکس‌آفیس: اسکرپ با requests + BeautifulSoup به DataFrame پانداس با همروندی thread-pool، و انتشار خودکار در PyPI با GitHub Actions.

---

## مهارت‌ها (پشتیبانی‌شده با کد واقعی)

| حوزه | آنچه واقعاً استفاده می‌کنم |
|---|---|
| **زبان‌ها** | پایتون (اصلی)، جاوااسکریپت، HTML/CSS/SCSS |
| **فریم‌ورک‌های وب** | Django 5 (مدل/منیجر کاربر سفارشی، CMS/وبلاگ، سبد خرید، سفارش، ادمین)، FastAPI (app factory، روترها، داشبورد Jinja2) |
| **داده و ORM** | PostgreSQL، SQLAlchemy 2 + مایگریشن Alembic، Django ORM، Redis، RabbitMQ |
| **غیرهمزمان و Job ها** | Celery worker ها + زمان‌بندی django_celery_beat |
| **دواپس و دیپلوی** | استک‌های پروداکشن Docker Compose (TLS با nginx/certbot، گورنیکورن gevent، محدودیت منابع)، مدیریت VPS لینوکس، Google Cloud Storage |
| **تست** | pytest در مقیاس در ربات معامله‌گری؛ تست در پکیج‌های منتشرشده |
| **یکپارچه‌سازی‌ها** | درگاه‌های پرداخت (زیبال / درگاه بانکی / ترب)، SMS.ir، اینستاگرام، گوگل (OAuth/نظرات/استوریج)، OpenAI، API های ارسال کالا |
| **حوزه معامله‌گری** | احراز هویت REST/HMAC صرافی، rate limiting، چرخه حیات سفارش، کنترل ریسک افت سرمایه، بک‌تست، مهندسی ویژگی/برچسب |

## نحوه کار من

- رمزها فقط در تنظیمات محیطی (`.env` + pydantic-settings / python-decouple)؛ هر ریپو `.env.example` دارد؛ وابستگی‌ها pin شده‌اند.
- پیش‌فرض‌های ایمن در هر کاری که به پول مربوط است: حالت شبیه‌سازی به‌صورت پیش‌فرض، کلید توقف اصلی، توقف ماندگار افت سرمایه، `Decimal` برای پول، ثبت پوزیشن فقط پس از تأیید fill.
- توضیح‌پذیری به‌عنوان قابلیت: سیگنال‌ها و تصمیم‌های ریسک دلیلشان را همراه دارند؛ داشبوردها به‌صورت پیش‌فرض فقط‌خواندنی‌اند.
- جداسازی دامنه: فرمت‌های اختصاصی ارائه‌دهنده فقط در مرز سیستم نرمال‌سازی می‌شوند و به داخل نشت نمی‌کنند.

## در حال بهبود

- **تست خودکار در اپ‌های وب** — انضباط قوی در ربات معامله‌گری؛ در حال گسترش به پروژه‌های جنگو.
- **مهندسی امنیت** — بهداشت رمزها، احراز هویت endpoint ها و کانتینرهای حداقل‌دسترسی؛ حوزه تمرکز فعال و آگاهانه.
- **CI همه‌جا** — اتوماسیون انتشار با GitHub Actions؛ در حال استقرار pipeline تست در همه ریپوهای فعال.

## مسیر رشد

- **۲۰۲۲** — اولین برنامه‌های پایتون: ابزارهای CLI، مترجم‌ها، اتوماسیون‌های کوچک.
- **۲۰۲۳** — الگوریتم‌ها و بازی‌ها (هوش مصنوعی minimax برای دوز، pygame)، اولین اپلیکیشن‌های جنگو.
- **۲۰۲۳–۲۰۲۴** — فروشگاه‌های چندبرندی جنگو در پروداکشن: پرداخت، ارسال، پیامک، کد تخفیف.
- **۲۰۲۵–۲۰۲۶** — پلتفرم‌های پروداکشن با pipeline های Celery/LLM/اینستاگرام، پکیج‌های منتشرشده پایتون، و سیستم معامله‌گری ایمن‌محور با معماری لایه‌ای، کنترل‌های ریسک ماندگار و تست واقعی.

## ریپوهای عمومی منتخب

- [pexels-python](https://github.com/Stink-Po/pexels-python) — SDK پکسلز با اعتبارسنجی Pydantic
- [boxoffice_api](https://github.com/Stink-Po/boxoffice_api) — کتابخانه داده‌های باکس‌آفیس
- [tictoctoi_with_AI](https://github.com/Stink-Po/tictoctoi_with_AI) — بازی دوز با هوش مصنوعی minimax

*(پلتفرم‌های پروداکشن و ربات معامله‌گری در ریپوهای خصوصی قرار دارند.)*

## ارتباط

- ایمیل: fresh.pourya@gmail.com
- لینکدین: [pourya-mohamadi](https://www.linkedin.com/in/pourya-mohamadi/)
