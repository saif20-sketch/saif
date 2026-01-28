<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام الفهرسة الطبية - جامعة السلطان قابوس</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --success: #27ae60;
            --warning: #f39c12;
            --danger: #e74c3c;
            --accent: #1abc9c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --gray: #95a5a6;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background: white;
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .logo {
            margin-bottom: 20px;
        }

        .logo i {
            font-size: 60px;
            color: var(--accent);
            margin-bottom: 15px;
        }

        .logo h1 {
            font-size: 36px;
            color: var(--primary);
            margin-bottom: 10px;
        }

        .logo h2 {
            color: var(--gray);
            font-weight: normal;
            font-size: 18px;
        }

        .connection-status {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            background: linear-gradient(135deg, var(--success), #229954);
            color: white;
            padding: 12px 25px;
            border-radius: 25px;
            font-weight: bold;
            margin-top: 15px;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }

        @media (max-width: 1100px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
        }

        .card-title {
            color: var(--primary);
            font-size: 24px;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 3px solid var(--accent);
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--dark);
            font-size: 16px;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 15px;
            border: 2px solid #e0e6ed;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s;
            background: white;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            border-color: var(--secondary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }

        .btn {
            padding: 16px 30px;
            border: none;
            border-radius: 10px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: all 0.3s;
            min-width: 160px;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--secondary), #2980b9);
            color: white;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
        }

        .btn-primary:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(52, 152, 219, 0.4);
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success), #229954);
            color: white;
            box-shadow: 0 5px 15px rgba(39, 174, 96, 0.3);
        }

        .btn-success:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(39, 174, 96, 0.4);
        }

        .form-actions {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .alert {
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 15px;
            animation: slideDown 0.5s ease;
            border-left: 5px solid;
        }

        .alert-success {
            background: #d4edda;
            color: #155724;
            border-left-color: #28a745;
        }

        .alert-info {
            background: #d1ecf1;
            color: #0c5460;
            border-left-color: #17a2b8;
        }

        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border-left-color: #dc3545;
        }

        footer {
            text-align: center;
            padding: 30px;
            color: white;
            font-size: 16px;
            margin-top: 40px;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 10000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            width: 90%;
            max-width: 900px;
            border-radius: 25px;
            overflow: hidden;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
        }

        .modal-header {
            background: linear-gradient(135deg, var(--primary), #1a2530);
            color: white;
            padding: 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-modal {
            font-size: 36px;
            cursor: pointer;
        }

        .modal-body {
            padding: 30px;
            max-height: 70vh;
            overflow-y: auto;
        }

        .marc-display {
            background: #1e1e1e;
            color: #d4d4d4;
            padding: 25px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            white-space: pre-wrap;
            font-size: 14px;
            line-height: 1.8;
            max-height: 500px;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-book-medical"></i>
                <h1>نظام الفهرسة الذكي للمكتبة الطبية</h1>
                <h2>جامعة السلطان قابوس - كلية الطب</h2>
                <div class="connection-status">
                    <i class="fas fa-cloud"></i>
                    النظام مستضاف على الإنترنت
                </div>
            </div>
        </header>

        <div class="alert alert-info">
            <i class="fas fa-info-circle"></i>
            <div>
                <strong>مرحباً بك في نظام الفهرسة المتصل!</strong><br>
                أدخل عنوان الكتاب أو ISBN للبحث في قواعد البيانات الطبية.
            </div>
        </div>

        <main class="main-content">
            <section class="card">
                <h3 class="card-title">
                    <i class="fas fa-search"></i>
                    البحث والفهرسة
                </h3>

                <div class="form-group">
                    <label for="searchQuery">
                        <i class="fas fa-book"></i>
                        ابحث عن كتاب طبي
                    </label>
                    <input type="text" id="searchQuery" 
                           placeholder="أدخل العنوان، المؤلف، أو ISBN..."
                           required>
                </div>

                <div class="form-actions">
                    <button type="button" id="searchBtn" class="btn btn-success">
                        <i class="fas fa-search"></i>
                        بحث سريع
                    </button>
                    <button type="button" id="indexBtn" class="btn btn-primary">
                        <i class="fas fa-robot"></i>
                        فهرسة ذكية
                    </button>
                </div>

                <div id="resultsContainer" style="display: none; margin-top: 30px;">
                    <!-- نتائج البحث تظهر هنا -->
                </div>
            </section>

            <section class="card">
                <h3 class="card-title">
                    <i class="fas fa-database"></i>
                    الكتب المفهرسة
                </h3>

                <div id="booksList">
                    <p style="color: var(--gray); text-align: center; padding: 20px;">
                        <i class="fas fa-book-open" style="font-size: 48px; margin-bottom: 15px; display: block;"></i>
                        ابحث عن كتاب لبدء الفهرسة
                    </p>
                </div>
            </section>
        </main>

        <footer>
            <p>نظام الفهرسة الذكي للمكتبة الطبية - جامعة السلطان قابوس</p>
            <p>مستضاف على GitHub Pages | الإصدار 1.0</p>
        </footer>
    </div>

    <script>
        // كود JavaScript الأساسي
        document.addEventListener('DOMContentLoaded', function() {
            console.log('نظام الفهرسة الطبية جاهز للاستخدام');
            
            document.getElementById('searchBtn').addEventListener('click', function() {
                const query = document.getElementById('searchQuery').value;
                if (query) {
                    simulateSearch(query);
                }
            });
            
            document.getElementById('indexBtn').addEventListener('click', function() {
                const query = document.getElementById('searchQuery').value;
                if (query) {
                    simulateIndexing(query);
                }
            });
        });

        function simulateSearch(query) {
            const results = document.getElementById('resultsContainer');
            results.innerHTML = `
                <div style="background: #f8f9fa; padding: 25px; border-radius: 15px;">
                    <h4 style="color: var(--success); margin-bottom: 15px;">
                        <i class="fas fa-check-circle"></i>
                        تم العثور على نتائج لـ "${query}"
                    </h4>
                    <div style="display: grid; gap: 15px;">
                        <div style="background: white; padding: 20px; border-radius: 10px; border: 1px solid #e0e6ed;">
                            <strong>كتاب تجريبي في الطب الباطني</strong><br>
                            <small style="color: var(--gray);">المؤلف: د. أحمد محمد | الناشر: دار الطب الحديث</small>
                        </div>
                    </div>
                </div>
            `;
            results.style.display = 'block';
        }

        function simulateIndexing(query) {
            const results = document.getElementById('resultsContainer');
            results.innerHTML = `
                <div style="background: #e8f4fd; padding: 25px; border-radius: 15px; border: 2px solid #b3e0ff;">
                    <h4 style="color: var(--primary); margin-bottom: 15px;">
                        <i class="fas fa-robot"></i>
                        تمت فهرسة "${query}" ذكياً
                    </h4>
                    <div style="background: white; padding: 20px; border-radius: 10px;">
                        <p><strong>التصنيف:</strong> WB - الممارسة الطبية</p>
                        <p><strong>رؤوس الموضوعات:</strong> طب الباطنة، التشخيص، العلاج</p>
                        <p><strong>رقم MARC:</strong> 001-2024-001</p>
                    </div>
                    <button class="btn btn-success" style="margin-top: 15px;">
                        <i class="fas fa-save"></i> حفظ في قاعدة البيانات
                    </button>
                </div>
            `;
            results.style.display = 'block';
        }
    </script>
</body>
</html>
