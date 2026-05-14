# tz-drawing-analyzer

Анализирует соответствие строительных чертежей (PDF) техническому заданию (DOCX) через Vision AI.

## Как работает

1. Читает ТЗ из `inputs/*.docx`
2. Читает все PDF из `inputs/chertezhi/*.pdf`
3. Конвертирует каждую страницу PDF в Markdown через Vision AI (Gemini 2.5 Flash)
4. Сравнивает требования ТЗ с данными чертежей через LLM
5. Выдаёт `comparison_report.md` с таблицами совпадений, расхождений и отсутствующих данных

## Структура файлов

```
tz-drawing-analyzer/
├── app.py                        # основной скрипт
├── inputs/
│   ├── TZ_zadanie.docx           # техническое задание
│   └── chertezhi/
│       ├── 01.AS1-S1_...pdf
│       └── 02.AS2-S1_...pdf
├── comparison_report.md          # генерируется после анализа
├── requirements.txt
└── README.md
```

## Установка и запуск

```bash
pip install -r requirements.txt
streamlit run app.py
```

Открыть в браузере: http://localhost:8501

## Настройки

- **OpenRouter API Key** — вводится в боковой панели (получить на openrouter.ai)
- **Модель** — по умолчанию `google/gemini-2.5-flash-preview-05-20`

## Автокоммит на GitHub

```bash
git add . && git commit -m "апдейт" && git push
```

## Cloudflare Tunnel (доступ через интернет)

Если нужно открыть приложение по публичной ссылке:

```bash
# Установить cloudflared (один раз)
# macOS:
brew install cloudflare/cloudflare/cloudflared

# Windows: скачать с https://github.com/cloudflare/cloudflared/releases

# Запустить туннель (после того как streamlit уже запущен)
cloudflared tunnel --url http://localhost:8501
```

Cloudflared выдаст временную ссылку вида `https://xxxx.trycloudflare.com` — она работает пока запущен процесс.

Для постоянного туннеля (если нужен) — зарегистрировать аккаунт на cloudflare.com и создать Named Tunnel.
