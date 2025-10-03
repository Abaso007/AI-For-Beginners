<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "6b11a37115944252ab3ed04e358d830d",
  "translation_date": "2025-10-03T09:32:17+00:00",
  "source_file": "AGENTS.md",
  "language_code": "uk"
}
-->
# AGENTS.md

## Огляд проєкту

AI for Beginners — це комплексна навчальна програма на 12 тижнів, що складається з 24 уроків, присвячених основам штучного інтелекту. Цей освітній репозиторій включає практичні уроки з використанням Jupyter Notebooks, тестів і лабораторних робіт. Програма охоплює:

- Символічний ШІ з представленням знань і експертними системами
- Нейронні мережі та глибоке навчання з TensorFlow і PyTorch
- Техніки та архітектури комп'ютерного зору
- Обробку природної мови (NLP), включаючи трансформери та BERT
- Спеціалізовані теми: генетичні алгоритми, навчання з підкріпленням, багатокомпонентні системи
- Етика ШІ та принципи відповідального використання ШІ

**Основні технології:** Python 3, Jupyter Notebooks, TensorFlow, PyTorch, Keras, OpenCV, Vue.js (для додатку тестів)

**Архітектура:** Репозиторій освітнього контенту з Jupyter Notebooks, організованими за тематичними областями, доповнений додатком тестів на основі Vue.js і підтримкою багатьох мов.

## Команди для налаштування

### Основне середовище розробки (Python/Jupyter)

Програма розроблена для роботи з Python і Jupyter Notebooks. Рекомендований підхід — використання miniconda:

```bash
# Clone the repository
git clone https://github.com/microsoft/ai-for-beginners
cd ai-for-beginners

# Create and activate conda environment
conda env create --name ai4beg --file environment.yml
conda activate ai4beg

# Start Jupyter Notebook
jupyter notebook
# OR
jupyter lab
```

### Альтернатива: Використання devcontainer

```bash
# Open in VS Code and select "Reopen in Container" when prompted
# The devcontainer will automatically set up the environment
```

### Налаштування додатку тестів

Додаток тестів — це окремий додаток на Vue.js, розташований у `etc/quiz-app/`:

```bash
cd etc/quiz-app
npm install
npm run serve  # Development server
npm run build  # Production build
npm run lint   # Lint and fix files
```

## Робочий процес розробки

### Робота з Jupyter Notebooks

1. **Локальна розробка:**
   - Активуйте середовище conda: `conda activate ai4beg`
   - Запустіть Jupyter: `jupyter notebook` або `jupyter lab`
   - Перейдіть до папок уроків і відкрийте файли `.ipynb`
   - Виконуйте комірки інтерактивно, щоб слідувати урокам

2. **VS Code з розширенням Python:**
   - Відкрийте репозиторій у VS Code
   - Встановіть розширення Python
   - VS Code автоматично визначає та використовує середовище conda
   - Відкривайте файли `.ipynb` безпосередньо у VS Code

3. **Хмарна розробка:**
   - **GitHub Codespaces:** Натисніть "Code" → "Codespaces" → "Create codespace on main"
   - **Binder:** Використовуйте значок Binder у README для запуску в браузері
   - Примітка: Binder має обмежені ресурси та деякі обмеження доступу до вебу

### Підтримка GPU для просунутих уроків

Пізніші уроки значно виграють від прискорення GPU:

- **Azure Data Science VM:** Використовуйте NC-серії VM з підтримкою GPU
- **Azure Machine Learning:** Використовуйте функції ноутбуків із обчисленнями на GPU
- **Google Colab:** Завантажуйте ноутбуки окремо (є безкоштовна підтримка GPU)

### Розробка додатку тестів

```bash
cd etc/quiz-app
npm run serve  # Hot-reload development server at http://localhost:8080
```

## Інструкції з тестування

Це освітній репозиторій, орієнтований на навчальний контент, а не на тестування програмного забезпечення. Традиційний набір тестів відсутній.

### Підходи до перевірки:

1. **Jupyter Notebooks:** Виконуйте комірки послідовно, щоб переконатися, що приклади коду працюють
2. **Тестування додатку тестів:** Ручне тестування через сервер розробки
3. **Перевірка перекладів:** Перевіряйте перекладений контент у папці `translations/`
4. **Linting додатку тестів:** `npm run lint` у `etc/quiz-app/`

### Виконання прикладів коду:

```bash
# Activate environment first
conda activate ai4beg

# Run Python scripts directly
python lessons/4-ComputerVision/07-ConvNets/pytorchcv.py

# Or execute notebooks
jupyter notebook lessons/3-NeuralNetworks/03-Perceptron/Perceptron.ipynb
```

## Стиль коду

### Стиль коду Python

- Стандартні конвенції Python для навчального коду
- Зрозумілий, читабельний код, що пріоритетно орієнтований на навчання, а не на оптимізацію
- Коментарі, що пояснюють ключові концепції
- Зручність для Jupyter Notebook: комірки мають бути максимально самодостатніми
- Відсутність суворих вимог до linting для навчального контенту

### JavaScript/Vue.js (додаток тестів)

- Конфігурація ESLint у `etc/quiz-app/package.json`
- Використовуйте `npm run lint` для перевірки та автоматичного виправлення проблем
- Конвенції Vue 2.x
- Архітектура на основі компонентів

### Організація файлів

```
lessons/
  ├── 0-course-setup/          # Setup instructions
  ├── 1-Intro/                 # Introduction to AI
  ├── 2-Symbolic/              # Symbolic AI
  ├── 3-NeuralNetworks/        # Neural Networks basics
  ├── 4-ComputerVision/        # Computer Vision
  ├── 5-NLP/                   # Natural Language Processing
  ├── 6-Other/                 # Other AI techniques
  ├── 7-Ethics/                # AI Ethics
  └── X-Extras/                # Additional content

etc/
  ├── quiz-app/                # Vue.js quiz application
  └── quiz-src/                # Quiz source files

translations/                  # Multi-language translations
```

## Збірка та розгортання

### Контент Jupyter

Процес збірки не потрібен — Jupyter Notebooks виконуються безпосередньо.

### Додаток тестів

```bash
cd etc/quiz-app

# Development
npm run serve

# Production build
npm run build  # Outputs to etc/quiz-app/dist/

# Deploy to Azure Static Web Apps
# Azure automatically creates GitHub Actions workflow
# See etc/quiz-app/README.md for detailed deployment instructions
```

### Сайт документації

Репозиторій використовує Docsify для документації:
- `index.html` слугує точкою входу
- Збірка не потрібна — сайт обслуговується безпосередньо через GitHub Pages
- Доступ за адресою: https://microsoft.github.io/AI-For-Beginners/

## Правила внесення змін

### Процес Pull Request

1. **Формат заголовка:** Чіткі, описові заголовки, що описують зміни
2. **Вимога CLA:** Потрібно підписати Microsoft CLA (автоматична перевірка)
3. **Рекомендації щодо контенту:**
   - Зберігайте освітній фокус і підхід, орієнтований на початківців
   - Тестуйте всі приклади коду в ноутбуках
   - Переконайтеся, що ноутбуки виконуються від початку до кінця
   - Оновлюйте переклади, якщо змінюєте англійський контент
4. **Зміни в додатку тестів:** Виконайте `npm run lint` перед комітом

### Внесення перекладів

- Переклади автоматизовані через GitHub Actions за допомогою co-op-translator
- Ручні переклади розміщуються в `translations/<language-code>/`
- Переклади тестів у `etc/quiz-app/src/assets/translations/`
- Підтримувані мови: понад 40 мов (див. README для повного списку)

### Активні області внесення змін

Див. `etc/CONTRIBUTING.md` для поточних потреб:
- Розділи глибокого навчання з підкріпленням
- Покращення виявлення об'єктів
- Приклади розпізнавання іменованих сутностей
- Зразки навчання власних вбудованих моделей

## Конфігурація середовища

### Необхідні залежності

```bash
# Core Python packages (from requirements.txt)
tensorflow==2.17.0
torch (via conda)
torchvision (via conda)
keras==3.5.0
opencv (via conda)
scikit-learn
numpy==1.26
pandas==2.2.2
matplotlib==3.9
jupyter
```

### Змінні середовища

Спеціальні змінні середовища не потрібні для базового використання.

Для розгортання на Azure (додаток тестів):
- `AZURE_STATIC_WEB_APPS_API_TOKEN` (встановлюється автоматично Azure)

## Виправлення помилок і усунення несправностей

### Поширені проблеми

**Проблема:** Створення середовища conda не вдалося
- **Рішення:** Спочатку оновіть conda: `conda update conda -y`
- Переконайтеся, що є достатньо місця на диску (рекомендується 50 ГБ)

**Проблема:** Ядро Jupyter не знайдено
- **Рішення:** 
  ```bash
  conda activate ai4beg
  python -m ipykernel install --user --name ai4beg
  ```

**Проблема:** GPU не виявлено в ноутбуках
- **Рішення:** 
  - Перевірте встановлення CUDA: `nvidia-smi`
  - Перевірте GPU у PyTorch: `python -c "import torch; print(torch.cuda.is_available())"`
  - Перевірте GPU у TensorFlow: `python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"`

**Проблема:** Додаток тестів не запускається
- **Рішення:**
  ```bash
  cd etc/quiz-app
  rm -rf node_modules package-lock.json
  npm install
  npm run serve
  ```

**Проблема:** Binder не відповідає або блокує завантаження
- **Рішення:** Використовуйте GitHub Codespaces або локальне налаштування для кращого доступу до ресурсів

### Проблеми з пам'яттю

Деякі уроки потребують значного обсягу оперативної пам'яті (рекомендується 8 ГБ+):
- Використовуйте хмарні VM для ресурсомістких уроків
- Закрийте інші програми під час навчання моделей
- Зменшіть розмір партій у ноутбуках, якщо пам'ять закінчується

## Додаткові примітки

### Для викладачів курсу

- Див. `lessons/0-course-setup/for-teachers.md` для рекомендацій щодо викладання
- Уроки є самодостатніми та можуть викладатися послідовно або вибірково
- Орієнтовний час: 12 тижнів по 2 уроки на тиждень

### Хмарні ресурси

- **Azure для студентів:** Безкоштовні кредити доступні для студентів
- **Microsoft Learn:** Додаткові навчальні шляхи, пов'язані з уроками
- **Binder:** Безкоштовний, але з обмеженими ресурсами та деякими мережевими обмеженнями

### Варіанти виконання коду

1. **Локально (рекомендується):** Повний контроль, найкраща продуктивність, підтримка GPU
2. **GitHub Codespaces:** Хмарний VS Code, добре для швидкого доступу
3. **Binder:** Jupyter у браузері, безкоштовно, але обмежено
4. **Azure ML Notebooks:** Корпоративний варіант із підтримкою GPU
5. **Google Colab:** Завантажуйте ноутбуки окремо, доступний безкоштовний рівень GPU

### Робота з ноутбуками

- Ноутбуки розроблені для виконання комірка за коміркою для навчання
- Багато ноутбуків завантажують набори даних під час першого запуску (це може зайняти час)
- Деякі моделі потребують GPU для прийнятного часу навчання
- Використовуються попередньо навчені моделі, де це можливо, щоб зменшити вимоги до обчислень

### Міркування щодо продуктивності

- Пізніші уроки з комп'ютерного зору (CNN, GAN) виграють від GPU
- Уроки з трансформерами NLP можуть потребувати значного обсягу оперативної пам'яті
- Навчання з нуля є освітнім, але займає багато часу
- Приклади перенесення навчання мінімізують час навчання

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, звертаємо вашу увагу, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникли внаслідок використання цього перекладу.