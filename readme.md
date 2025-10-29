# 🎓 شات بوت جامعة الشام | AI University Assistant

<!-- 🎬 VERY IMPORTANT: Add a GIF or a high-quality screenshot here! A visual demonstration is the most powerful part of a README. -->
<!-- Example: <p align="center"><img src="images/chatbot-demo.gif" width="700"></p> -->

**شات بوت ذكي تم تطويره ليكون المساعد الأكاديمي الأول لطلاب جامعة الشام، حيث يوفر إجابات دقيقة وفورية حول كل ما يتعلق بالجامعة باستخدام أحدث تقنيات الذكاء الاصطناعي.**

---

### 🛠️ التقنيات المستخدمة (Tech Stack)

| Frontend | Backend & AI Core | Data & Vector DB | Deployment & Tools |
| :---: | :---: | :---: | :---: |
| ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white) | ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) | ![FAISS](https://img.shields.io/badge/FAISS-4A90E2?style=for-the-badge&logo=facebook&logoColor=white) | ![Git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white) |
| | ![Google Gemini](https://img.shields.io/badge/Google_Gemini-8E44AD?style=for-the-badge&logo=google&logoColor=white) | ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) | ![VSCode](https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white) |
| | ![LangChain](https://img.shields.io/badge/LangChain-000000?style=for-the-badge) | | |
| | ![Tesseract OCR](https://img.shields.io/badge/Tesseract-5F6368?style=for-the-badge) | | |


---

### 🌟 الميزات الرئيسية (Key Features)

- **🧠 نظام إجابة هجين وذكي:**
  - **دقة عالية:** يعطي الأولوية للإجابات من قاعدة بيانات الأسئلة الشائعة (FAQ) لضمان الدقة والسرعة.
  - **قدرة توليدية:** يستخدم نموذج Google Gemini للإجابة على الأسئلة المعقدة وغير المتوقعة.

- **📚 استرجاع معلومات معزز (RAG):**
  - يوظف قواعد بيانات المتجهات (FAISS) ونماذج التضمين (Embeddings) للبحث الدلالي وفهم سياق الأسئلة.

- **🌐 جمع بيانات شامل وتلقائي:**
  - **زحف الويب (Web Scraping):** يجمع النصوص تلقائياً من موقع الجامعة.
  - **التعرف الضوئي على الأحرف (OCR):** يستخلص المعلومات حتى من الصور والمستندات، لضمان عدم تفويت أي تفاصيل.

- **🎨 واجهة مستخدم تفاعلية:**
  - واجهة جذابة وسهلة الاستخدام مبنية باستخدام Streamlit.
  - حفظ سجل المحادثات، مع خيارات لإدارة وبدء محادثات جديدة.

---

<details>
<summary>🚀 <strong>دليل الإعداد والتشغيل (Setup & Run)</strong></summary>

لإعداد وتشغيل شات بوت جامعة الشام على جهازك، اتبع الخطوات التالية:

#### 1. المتطلبات الأساسية
- **Python 3.9+**
- **pip** (مدير حزم Python)
- **Tesseract OCR:** يجب تثبيته على نظامك (راجع [Tesseract Docs](https://github.com/tesseract-ocr/tesseract) لتعليمات التثبيت).

#### 2. إعداد البيئة
1.  **استنساخ المستودع:**
    ```bash
    git clone <رابط_المستودع>
    cd CHATBOT_SHAM
    ```
2.  **إنشاء وتفعيل بيئة افتراضية (موصى به):**
    ```bash
    python -m venv venv
    # Windows
    .\venv\Scripts\activate
    # macOS / Linux
    source venv/bin/activate
    ```
3.  **تثبيت المكتبات:**
    ```bash
    pip install streamlit langchain-community langchain-google-genai langchain-core sentence-transformers python-dotenv requests beautifulsoup4 pytesseract Pillow faiss-cpu
    ```
4.  **إعداد مفتاح Google API:**
    - أنشئ ملفًا جديدًا باسم `.env`.
    - أضف السطر التالي مع استبدال `YOUR_API_KEY_HERE` بمفتاحك:
      ```
      GOOGLE_API_KEY="YOUR_API_KEY_HERE"
      ```

#### 3. إعداد قواعد البيانات والمعرفة
1.  **جمع البيانات:** قم بتشغيل أحد السكريبتات لجمع البيانات من موقع الجامعة.
    ```bash
    # لجمع النصوص من HTML والصور (موصى به)
    python scrape_with_ocr.py
    ```
2.  **تنظيف البيانات:**
    ```bash
    python clean_data.py
    ```
3.  **إعداد ملف الأسئلة الشائعة (FAQ):** تأكد من أن ملف `university_faq_qa.txt` موجود ومنسق بشكل صحيح.

4.  **بناء قاعدة بيانات المتجهات:**
    ```bash
    python build_vector_db.py
    ```

#### 4. تشغيل الشات بوت
```bash
streamlit run app.py
افتح الرابط http://localhost:8501 في متصفحك.
</details>
<details>
<summary>🛠️ <strong>نظرة فنية على آلية العمل (Technical Deep-Dive)</strong></summary>
يعتمد الشات بوت على بنية RAG لتقديم إجابات دقيقة. تمر العملية بالمراحل التالية:
جمع البيانات (Data Ingestion):
يتم استخدام requests و BeautifulSoup لزحف صفحات الويب.
يتم استخدام pytesseract و Pillow لاستخلاص النصوص من الصور (OCR).
تنظيف البيانات (Data Cleaning):
تتم إزالة المسافات الزائدة، العبارات غير المفيدة، وضمان تفرد الفقرات لمنع التكرار.
بناء قواعد بيانات المتجهات (Vector DB Construction):
التضمين (Embedding): يتم استخدام نموذج distiluse-base-multilingual-cased-v1 من HuggingFace لتحويل الأسئلة في ملف الـ FAQ إلى متجهات رقمية (embeddings).
الفهرسة (Indexing): يتم استخدام مكتبة FAISS لإنشاء قاعدة بيانات متجهات قابلة للبحث بكفاءة من هذه التضمينات.
منطق الاستجابة (Response Logic):
عندما يطرح المستخدم سؤالاً، يتم تحويله إلى متجه.
يتم البحث عن أقرب متجه مطابق في قاعدة بيانات FAISS الخاصة بالأسئلة الشائعة.
إذا كان التشابه عالياً: يتم إرجاع الإجابة المحددة مسبقاً من الـ FAQ (دقة عالية).
إذا كان التشابه منخفضاً: يتم توجيه السؤال إلى نموذج Google Gemini لتوليد إجابة (مرونة عالية).
يتم عرض الإجابة للمستخدم مع تحديد مصدرها (FAQ أو LLM).
</details>
🤝 المساهمة (Contributing)
نرحب بالمساهمات لتحسين هذا المشروع. إذا كنت ترغب في المساهمة، يرجى اتباع الخطوات القياسية لطلبات الدمج (Pull Requests).
📄 الترخيص (License)
.
ملاحظة: هذا الشات بوت يجيب بناءً على معلومات تم جمعها آلياً. للحصول على أحدث المعلومات الرسمية، يرجى زيارة موقع الجامعة.
