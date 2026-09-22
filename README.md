![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white) ![Celery](https://img.shields.io/badge/Celery-37814A?style=for-the-badge&logo=celery&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white) ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Pourya Mohamadi — Python Backend & Production Systems Engineer

Self-taught Python developer. I don't just write application code — I build, deploy, operate, and maintain production systems that serve real customers and real revenue: multi-brand Django e-commerce and service platforms, a risk-first cryptocurrency trading bot, and packaged Python SDKs. My day-to-day covers the full path from model design to Dockerized production deployment on AWS and Linux servers, plus the operational work that keeps those systems alive.

---

## Major production projects

### 1. Lidoma Home Services — HVAC service platform (production)
Django 5 platform running the real business of an HVAC company in Winnipeg (lidomahomeservices.ca): booking and order workflows, staff area, content, and automation — operated end to end in Dockerized production.

- **Production stack:** Docker Compose with 8 services — nginx (TLS termination, 444 catch-all servers, ACME automation via certbot/dns-cloudflare), gunicorn with 5 gevent workers and max-request recycling, PostgreSQL 13, Redis, RabbitMQ, Celery worker + beat, and dedicated certbot request/renew containers with `unless-stopped` policies.
- **Background & automation:** Celery pipelines for transactional emails, Google Reviews fetching with Redis caching, and scheduled LLM blog writing (OpenAI, structured prompts, JSON parsing, similarity-based dedup, automated Pexels image sourcing).
- **Integrations:** Google OAuth sign-in, Google Reviews & Cloud Storage (nightly `pg_dump` backups), SMS.ir notifications, Instagram posting automation, Iranian bank payment gateways (az-iranian-bank-gateways, Zibal).
- **Django depth:** custom email-based user model with custom manager, social-auth pipeline customization, tagged blog with view-ranking in Redis, sitemaps and SEO for all content apps.
- **Operations:** nightly database backups, log management, container orchestration, and troubleshooting on the live Linux server.

### 2. Fapo Shop — multi-brand e-commerce platform (production)
A full Django e-commerce system running real stores (several generations, 2024–2026): product catalog with variants/colors, session carts, orders, coupons, PDF invoicing, and a staff area with its own dashboards.

- **Production stack:** Docker Compose — nginx + TLS via certbot, gunicorn (5 gevent workers), PostgreSQL, Redis (django-redis caching), RabbitMQ as Celery broker, separate celery_worker and celery_beat services.
- **Payments:** Zibal gateway integration (request/verify), Torob BNPL flow with JWT auth and full verify/settle/revert lifecycle, bank gateway package, order confirmation SMS via SMS.ir (OTP + status templates).
- **Shipping:** PostEx API integration for courier rates and destination lookup.
- **Ops tooling:** management commands for admin bootstrap and address/city data seeding, product availability updates, order/task pipelines, and admin-facing order management.

### 3. Winnipeg Furnace — HVAC services site (production, AWS)
Django platform for a furnace/duct services business in Winnipeg (winni-furnace.ca) — my deepest AWS-integrated deployment.

- **AWS services, verified in the code:** **RDS PostgreSQL** (dedicated DB instance), **S3** media/file storage via django-storages + boto3 (S3Boto3Storage, bucket in ca-central-1, presigned URLs), and **Amazon SES** transactional email (django-ses backend, email-smtp endpoint, ca-central-1) — including bulk mail features built directly on boto3 (presigned S3 asset URLs, email-to-all-users tooling).
- **Deployment:** Dockerized (Python 3.11 Alpine image, entrypoint with migrate + collectstatic), uWSGI application server, gunicorn as an alternate WSGI option, whitenoise static compression, and a settings structure separated for production.
- **Domain features:** service catalog (duct cleaning, furnace installation/repair/cleaning), quotes and offers, custom user accounts, password-reset email flows, service rating/scoring.

---

## Production & DevOps experience

Running these platforms has made deployment and operations a core part of my work, not an afterthought:

- **Docker in production:** multi-service Docker Compose stacks (nginx, gunicorn/uWSGI, PostgreSQL, Redis, RabbitMQ, Celery worker + beat, certbot TLS automation) with restart policies, resource limits, internal-only networks, and named volumes.
- **AWS:** production deployments backed by RDS, S3 (django-storages/boto3), and SES, alongside S3-compatible object storage (Google Cloud Storage) for backups in other projects.
- **Linux server administration:** hands-on operation of production Linux servers — services, logs, networking, permissions, processes, databases, and troubleshooting live incidents.
- **Web serving & TLS:** nginx reverse-proxy configs (upstreams, keepalive, gzip, catch-all 444 handling, ACME challenge routing) and automated Let's Encrypt certificate lifecycle (including DNS-challenge automation).
- **Data & caching infrastructure:** PostgreSQL administration and migrations (Alembic in the trading bot), Redis for caching and ranking, RabbitMQ message brokering, scheduled jobs via django_celery_beat.
- **Operational habits:** environment-based secrets (`.env` + pydantic-settings / python-decouple with `.env.example` in every repo), pinned dependencies, scheduled database backups to object storage.

---

## Trading systems (Python, 2026)

Author of an adaptive trading bot for the Bitpin exchange (~24k LOC, ~100 modules) — my strongest demonstration of architecture, risk engineering, and systems design:

- **Layered architecture** — exchange adapters normalize REST payloads into frozen domain dataclasses; strategy, risk, persistence, and execution never touch provider JSON directly.
- **Explainable strategy engine** — deterministic multi-timeframe signals (EMA trend, MACD momentum, ATR volatility, volume filters) carrying score, confidence, regime, and human-readable reasons per component.
- **Risk engine** — daily/monthly drawdown kill switches persisted to PostgreSQL so restarts cannot reset them; `Decimal` money math; hard blockers that always override signals.
- **Exchange client** — HMAC-signed auth with managed token lifecycle, per-endpoint rate limiting, circuit breaker, order execution gated off by default (simulation-first; live requires explicit config + admin approval).
- **Tooling around it** — backtesting with walk-forward splits, a feature/label pipeline for learning from past trades, and a read-only FastAPI + Jinja2 dashboard.
- **Tested** — 369 pytest tests across 37 files (fakes, monkeypatching, DB-backed fixtures).

---

## Skills (backed by shipped code)

| Area | What I actually use |
|---|---|
| **Languages** | Python (primary), JavaScript, HTML/CSS/SCSS |
| **Web frameworks** | Django 5 (custom user models/managers, e-commerce, CMS/blog, admin), FastAPI (app factory, routers, Jinja2 dashboard) |
| **Data & ORM** | PostgreSQL (incl. AWS RDS), SQLAlchemy 2 + Alembic, Django ORM, Redis, RabbitMQ |
| **Async & jobs** | Celery workers + django_celery_beat schedules |
| **Cloud & DevOps** | AWS (RDS, S3, SES) · Docker Compose production stacks · nginx + certbot TLS · Linux server administration (services, logs, networking, permissions, troubleshooting) |
| **Testing** | pytest at scale in the trading bot; test suites in published packages |
| **Integrations** | Payment gateways (Zibal / bank gateways / Torob BNPL), SMS.ir, Instagram API, Google (OAuth, Reviews, Cloud Storage), Amazon SES, OpenAI API, PostEx shipping |
| **Trading domain** | Exchange REST/HMAC auth, rate limiting, order lifecycle, drawdown risk controls, backtesting, feature/label engineering |

## How I work

- Secrets live in environment config only; every repo ships a `.env.example`; dependencies are pinned.
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
- **2023–2024** — first production AWS deployment (Winnipeg Furnace: RDS + S3 + SES) and multi-brand Django e-commerce in production.
- **2025–2026** — production platforms with Celery/LLM/Instagram pipelines, published Python packages, and a risk-first trading system with layered architecture, persistent risk controls, and a real test suite.

## Smaller projects & libraries

- [pexels-python](https://github.com/Stink-Po/pexels-python) — typed Pexels API SDK: Pydantic validation on every call, hatchling packaging, own test suite.
- [boxoffice_api](https://github.com/Stink-Po/boxoffice_api) — box office data library: BeautifulSoup scraping into pandas DataFrames, thread-pool concurrency, PyPI release via GitHub Actions.
- [tictoctoi_with_AI](https://github.com/Stink-Po/tictoctoi_with_AI) — tic-tac-toe with a minimax AI.

*(The production platforms and the trading bot live in private repositories.)*

## Contact

- Email: fresh.pourya@gmail.com
- LinkedIn: [pourya-mohamadi](https://www.linkedin.com/in/pourya-mohamadi/)

---

---

# پوریا محمدی — مهندس بک‌اند پایتون و سیستم‌های پروداکشن

توسعه‌دهنده پایتون خودآموخته. کارم فقط نوشتن کد اپلیکیشن نیست — سیستم‌های پروداکشنی را که مشتری و درآمد واقعی دارند می‌سازم، دیپلوی می‌کنم، راه‌اندازی و نگه‌داری می‌کنم: پلتفرم‌های فروشگاهی و خدماتی جنگو برای چند برند، ربات معامله‌گری ارز دیجیتال با رویکرد «اول ایمنی»، و کتابخانه‌های پایتون بسته‌بندی‌شده. کار روزانه من از طراحی مدل تا دیپلوی Docker شده روی AWS و سرورهای لینوکس و عملیاتی که این سیستم‌ها را زنده نگه می‌دارد را پوشش می‌دهد.

---

## پروژه‌های اصلی پروداکشن

### ۱. Lidoma Home Services — پلتفرم خدمات HVAC (پروداکشن)
پلتفرم Django 5 در حال اجرای کسب‌وکار واقعی یک شرکت تأسیسات در وینیپگ (lidomahomeservices.ca): فرآیند رزرو و سفارش، پنل کارکنان، محتوا و اتوماسیون — به‌صورت کامل در پروداکشن Docker شده اداره می‌شود.

- **استک پروداکشن:** Docker Compose با ۸ سرویس — nginx (پایان TLS، سرورهای catch-all با کد ۴۴۴، اتوماسیون ACME با certbot/dns-cloudflare)، گورنیکورن با ۵ ورکر gevent و بازیافت خودکار پردازش‌ها، PostgreSQL 13، Redis، RabbitMQ، کارگر و زمان‌بند Celery، و کانتینرهای جداگانه درخواست/تمدید گواهی certbot با سیاست `unless-stopped`.
- **کارهای پس‌زمینه و اتوماسیون:** خطوط Celery برای ایمیل‌های تراکنشی، دریافت نظرات گوگل با کش Redis، و نوشتن خودکار وبلاگ با LLM (OpenAI، پرامپت ساختاریافته، پارس JSON، حذف تکرار بر اساس شباهت، تأمین خودکار تصویر از Pexels).
- **یکپارچه‌سازی‌ها:** ورود با گوگل OAuth، نظرات گوگل و Google Cloud Storage (بکاپ شبانه `pg_dump`)، نوتیفیکیشن SMS.ir، اتوماسیون اینستاگرام، درگاه‌های پرداخت بانکی ایرانی (az-iranian-bank-gateways، زیبال).
- **عمق جنگو:** مدل کاربر سفارشی مبتنی بر ایمیل با منیجر سفارشی، سفارشی‌سازی pipeline ی social-auth، وبلاگ تگ‌دار با رتبه‌بندی بازدید در Redis، sitemap و سئو برای همه اپ‌های محتوایی.
- **عملیات:** بکاپ شبانه دیتابیس، مدیریت لاگ، ارکستراسیون کانتینرها، و عیب‌یابی روی سرور لینوکس واقعی.

### ۲. Fapo Shop — پلتفرم فروشگاهی چندبرندی (پروداکشن)
سیستم کامل فروشگاهی جنگو در حال اجرای فروشگاه‌های واقعی (چند نسل، ۲۰۲۴–۲۰۲۶): کاتالوگ محصولات با رنگ/وارینت، سبد خرید سشنی، سفارش‌ها، کد تخفیف، فاکتور PDF، و پنل کارکنان با داشبورد اختصاصی.

- **استک پروداکشن:** Docker Compose — nginx + TLS با certbot، گورنیکورن (۵ ورکر gevent)، PostgreSQL، Redis (کش django-redis)، RabbitMQ به‌عنوان بروکر Celery، و سرویس‌های جداگانه celery_worker و celery_beat.
- **پرداخت:** یکپارچه‌سازی درگاه زیبال (request/verify)، خرید اعتباری ترب با احراز هویت JWT و چرخه کامل verify/settle/revert، پکیج درگاه بانکی، پیامک تأیید سفارش با SMS.ir (OTP و قالب‌های وضعیت).
- **ارسال کالا:** یکپارچه‌سازی API پست (PostEx) برای نرخ پیک و یافتن مقصد.
- **ابزارهای عملیاتی:** management command های بوت‌استرپ ادمین و seed داده شهر/آدرس، به‌روزرسانی موجودی محصولات، pipeline های سفارش/تسک، و مدیریت سفارش در ادمین.

### ۳. Winnipeg Furnace — سایت خدمات تأسیسات (پروداکشن روی AWS)
پلتفرم جنگو برای کسب‌وکار خدمات بخاری/کانال‌کشی در وینیپگ (winni-furnace.ca) — عمیق‌ترین دیپلوی AWS من.

- **سرویس‌های AWS، تأییدشده در کد:** **RDS PostgreSQL** (اینستنس اختصاصی دیتابیس)، **S3** برای ذخیره فایل/مدیا با django-storages + boto3 (S3Boto3Storage، باکت در ca-central-1، URLهای امضاشده)، و **Amazon SES** برای ایمیل تراکنشی (بک‌اند django-ses، endpoint رسمی، ca-central-1) — شامل قابلیت ایمیل گروهی ساخته‌شده مستقیماً روی boto3 (URL امضاشده assetها در S3، ابزار ایمیل به همه کاربران).
- **دیپلوی:** Docker شده (ایمیج Python 3.11 Alpine، entrypoint با migrate + collectstatic)، سرور اپلیکیشن uWSGI، گورنیکورن به‌عنوان گزینه جایگزین WSGI، فشرده‌سازی استاتیک با whitenoise، و ساختار تنظیمات جدا برای پروداکشن.
- **قابلیت‌های دامنه:** کاتالوگ خدمات (کانال‌کشی، نصب/تعمیر/شستشوی بخاری)، پیش‌فاکتور و پیشنهادها، حساب کاربری سفارشی، فرآیند ایمیل ریست رمز، امتیازدهی خدمات.

---

## تجربه پروداکشن و دواپس

اداره این پلتفرم‌ها، دیپلوی و عملیات را به بخش اصلی کار من تبدیل کرده است، نه یک کار جنبی:

- **داکر در پروداکشن:** استک‌های چندسرویسی Docker Compose (nginx، گورنیکورن/uWSGI، PostgreSQL، Redis، RabbitMQ، کارگر و زمان‌بند Celery، اتوماسیون TLS با certbot) با سیاست ری‌استارت، محدودیت منابع، شبکه داخلی، و volume های نام‌دار.
- **AWS:** دیپلوی‌های پروداکشن مبتنی بر RDS، S3 (django-storages/boto3) و SES، به‌همراه object storage سازگار با S3 (Google Cloud Storage) برای بکاپ در پروژه‌های دیگر.
- **مدیریت سرور لینوکس:** بهره‌برداری عملی از سرورهای لینوکس پروداکشن — سرویس‌ها، لاگ‌ها، شبکه، دسترسی‌ها، پروسه‌ها، دیتابیس‌ها و عیب‌یابی رخدادهای زنده.
- **وب‌سرور و TLS:** کانفیگ nginx به‌عنوان reverse-proxy (upstream، keepalive، gzip، مدیریت درخواست‌های ناخواسته با ۴۴۴، مسیردهی چالش ACME) و چرخه عمر خودکار گواهی Let's Encrypt (شامل اتوماسیون DNS-challenge).
- **زیرساخت داده و کش:** مدیریت PostgreSQL و مایگریشن‌ها (Alembic در ربات معامله‌گری)، Redis برای کش و رتبه‌بندی، پیام‌رسانی RabbitMQ، Job های زمان‌بندی‌شده با django_celery_beat.
- **عادت‌های عملیاتی:** رمزها فقط از طریق تنظیمات محیطی (`.env` + pydantic-settings / python-decouple با `.env.example` در هر ریپو)، وابستگی‌های pin شده، بکاپ زمان‌بندی‌شده دیتابیس روی object storage.

---

## سیستم‌های معامله‌گری (پایتون، ۲۰۲۶)

نویسنده ربات معامله‌گری تطبیقی برای صرافی بیت‌پین (~۲۴ هزار خط کد، ~۱۰۰ ماژول) — قوی‌ترین نمایش معماری، مهندسی ریسک و طراحی سیستم در کارهای من:

- **معماری لایه‌ای** — آداپترهای صرافی پاسخ‌های REST را به دیتاکلاس‌های تغییرناپذیر نرمال‌سازی می‌کنند؛ لایه‌های استراتژی، ریسک، persistence و اجرا هرگز با JSON اختصاصی صرافی سروکار ندارند.
- **موتور استراتژی قابل توضیح** — سیگنال‌های قطعی چند‌تایم‌فریمی (روند EMA، مومنتوم MACD، نوسان ATR، فیلتر حجم) با امتیاز، اطمینان، رژیم بازار و دلیل قابل‌خواندن برای هر مؤلفه.
- **موتور ریسک** — کلیدهای توقف افت روزانه/ماهانه که در PostgreSQL ذخیره می‌شوند تا ری‌استارت نتواند آن‌ها را ریست کند؛ محاسبات مالی با `Decimal`؛ بلاکرهای سخت که همیشه بر سیگنال اولویت دارند.
- **کلاینت صرافی** — احراز هویت HMAC با مدیریت چرخه توکن، rate limiting برای هر endpoint، circuit breaker، و اجرای سفارش به‌صورت پیش‌فرض غیرفعال (اول شبیه‌سازی؛ معامله واقعی نیازمند تنظیمات صریح + تأیید ادمین).
- **ابزارهای پیرامون** — بک‌تست با walk-forward، خط تولید ویژگی/برچسب برای یادگیری از معاملات گذشته، و داشبورد فقط‌خواندنی با FastAPI و Jinja2.
- **تست‌شده** — ۳۶۹ تست pytest در ۳۷ فایل (fake ها، monkeypatching، fixture های متصل به دیتابیس).

---

## مهارت‌ها (پشتیبانی‌شده با کد واقعی)

| حوزه | آنچه واقعاً استفاده می‌کنم |
|---|---|
| **زبان‌ها** | پایتون (اصلی)، جاوااسکریپت، HTML/CSS/SCSS |
| **فریم‌ورک‌های وب** | Django 5 (مدل/منیجر کاربر سفارشی، فروشگاه، CMS/وبلاگ، ادمین)، FastAPI (app factory، روترها، داشبورد Jinja2) |
| **داده و ORM** | PostgreSQL (شامل AWS RDS)، SQLAlchemy 2 + Alembic، Django ORM، Redis، RabbitMQ |
| **غیرهمزمان و Job ها** | Celery worker ها + زمان‌بندی django_celery_beat |
| **کلود و دواپس** | AWS (RDS، S3، SES) · استک‌های پروداکشن Docker Compose · nginx + TLS با certbot · مدیریت سرور لینوکس (سرویس، لاگ، شبکه، دسترسی‌ها، عیب‌یابی) |
| **تست** | pytest در مقیاس در ربات معامله‌گری؛ تست در پکیج‌های منتشرشده |
| **یکپارچه‌سازی‌ها** | درگاه‌های پرداخت (زیبال / درگاه بانکی / ترب)، SMS.ir، اینستاگرام، گوگل (OAuth، نظرات، Cloud Storage)، Amazon SES، OpenAI، پست (PostEx) |
| **حوزه معامله‌گری** | احراز هویت REST/HMAC صرافی، rate limiting، چرخه حیات سفارش، کنترل ریسک افت سرمایه، بک‌تست، مهندسی ویژگی/برچسب |

## نحوه کار من

- رمزها فقط در تنظیمات محیطی؛ هر ریپو `.env.example` دارد؛ وابستگی‌ها pin شده‌اند.
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
- **۲۰۲۳–۲۰۲۴** — اولین دیپلوی پروداکشن AWS (Winnipeg Furnace: RDS + S3 + SES) و فروشگاه‌های چندبرندی جنگو در پروداکشن.
- **۲۰۲۵–۲۰۲۶** — پلتفرم‌های پروداکشن با pipeline های Celery/LLM/اینستاگرام، پکیج‌های منتشرشده پایتون، و سیستم معامله‌گری ایمن‌محور با معماری لایه‌ای، کنترل‌های ریسک ماندگار و تست واقعی.

## پروژه‌های کوچک‌تر و کتابخانه‌ها

- [pexels-python](https://github.com/Stink-Po/pexels-python) — SDK تایپ‌شده پکسلز: اعتبارسنجی Pydantic در هر فراخوان، بسته‌بندی hatchling، تست اختصاصی.
- [boxoffice_api](https://github.com/Stink-Po/boxoffice_api) — کتابخانه داده‌های باکس‌آفیس: اسکرپ با BeautifulSoup به DataFrame پانداس، همروندی thread-pool، انتشار PyPI با GitHub Actions.
- [tictoctoi_with_AI](https://github.com/Stink-Po/tictoctoi_with_AI) — بازی دوز با هوش مصنوعی minimax.

*(پلتفرم‌های پروداکشن و ربات معامله‌گری در ریپوهای خصوصی قرار دارند.)*

## ارتباط

- ایمیل: fresh.pourya@gmail.com
- لینکدین: [pourya-mohamadi](https://www.linkedin.com/in/pourya-mohamadi/)
