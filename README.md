import streamlit as st
import openai
import json

# --- إعدادات الصفحة ---
st.set_page_config(
    page_title="نظام الفهرسة الطبية الذكي | SQU",
    page_icon="🏥",
    layout="centered"
)

# --- تصميم الواجهة (CSS) ---
st.markdown("""
    <style>
    .main { background-color: #f8f9fa; }
    .stButton>button {
        width: 100%;
        background-color: #004a99;
        color: white;
        border-radius: 10px;
        height: 3em;
        font-weight: bold;
    }
    .header-box {
        background-color: #004a99;
        padding: 20px;
        border-radius: 15px;
        color: white;
        text-align: center;
        margin-bottom: 25px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    .result-card {
        background-color: white;
        padding: 20px;
        border-radius: 10px;
        border-right: 5px solid #004a99;
        margin-top: 20px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    }
    </style>
    """, unsafe_allow_html=True)

# --- الهيدر ---
st.markdown("""
    <div class="header-box">
        <h1 style="margin:0;">المكتبة الطبية - جامعة السلطان قابوس</h1>
        <p style="margin:5px 0 0 0;">نظام الفهرسة الآلي بالذكاء الاصطناعي (MARC 21 / MeSH)</p>
    </div>
    """, unsafe_allow_html=True)

# --- القائمة الجانبية للإعدادات ---
with st.sidebar:
    st.image("https://www.squ.edu.om/Portals/0/SQU-Logo.png", width=150)
    st.title("الإعدادات")
    api_key = st.text_input("أدخل مفتاح OpenAI API:", type="password")
    st.info("هذا النظام يستخدم GPT-4 لتحليل الكتاب واستخراج رؤوس الموضوعات الطبية بدقة.")

# --- واجهة الإدخال الرئيسية ---
st.subheader("🔍 فهرسة كتاب جديد")
isbn_input = st.text_input("أدخل رقم ISBN (بدون فواصل):", placeholder="مثال: 9780323596299")

if st.button("توليد بيانات الفهرسة"):
    if not api_key:
        st.error("⚠️ من فضلك أدخل مفتاح API في القائمة الجانبية.")
    elif not isbn_input:
        st.warning("⚠️ يرجى إدخال رقم ISBN للبدء.")
    else:
        try:
            client = openai.OpenAI(api_key=api_key)
            
            with st.spinner('جاري التواصل مع محرك الذكاء الاصطناعي...'):
                prompt = f"""
                You are a professional medical cataloger at Sultan Qaboos University. 
                Generate a catalog record for ISBN: {isbn_input}.
                Requirements:
                1. Subject headings must be from MeSH (Medical Subject Headings).
                2. Classification must be LCC (Library of Congress).
                3. Include a Medical Cutter number.
                4. Return the result strictly as a JSON object with keys: 
                   "title", "author", "edition", "pub_year", "mesh", "lcc", "cutter", "marc_21_raw".
                """
                
                response = client.chat.completions.create(
                    model="gpt-4",
                    messages=[{"role": "user", "content": prompt}],
                    response_format={ "type": "json_object" }
                )
                
                res_data = json.loads(response.choices[0].message.content)

                # --- عرض النتائج ---
                st.balloons()
                
                st.markdown(f"""
                <div class="result-card">
                    <h3 style="color:#004a99;">{res_data['title']}</h3>
                    <p><b>المؤلف:</b> {res_data['author']} | <b>الطبعة:</b> {res_data['edition']} | <b>السنة:</b> {res_data['pub_year']}</p>
                    <hr>
                    <p style="color:#2c3e50;"><b>رؤوس الموضوعات الطبية (MeSH):</b><br>{res_data['mesh']}</p>
                    <p style="color:#d35400;"><b>تصنيف مكتبة الكونجرس (LCC):</b> {res_data['lcc']}</p>
                    <p style="color:#d35400;"><b>رقم كتر (Cutter):</b> {res_data['cutter']}</p>
                </div>
                """, unsafe_allow_html=True)

                with st.expander("عرض حقول MARC 21 (Raw Data)"):
                    st.code(res_data['marc_21_raw'], language="text")
                
                st.download_button(
                    label="تحميل البيانات كملف نصي",
                    data=str(res_data),
                    file_name=f"catalog_{isbn_input}.txt",
                    mime="text/plain"
                )

        except Exception as e:
            st.error(f"حدث خطأ أثناء المعالجة: {str(e)}")

# --- التذييل ---
st.markdown("<br><hr><p style='text-align:center; color:grey;'>نظام تجريبي للمكتبة الطبية - جامعة السلطان قابوس</p>", unsafe_allow_html=True)
