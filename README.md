<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام متابعة وحساب الدرجات الدراسية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3498db;
            --secondary: #2ecc71;
            --accent: #e74c3c;
            --light: #f8f9fa;
            --dark: #2c3e50;
            --gray: #7f8c8d;
            --anatomy: #9b59b6;
            --physiology: #3498db;
            --chemistry: #e74c3c;
            --histology: #2ecc71;
            --embryology: #f1c40f;
            --ethics: #1abc9c;
            --baath: #e67e22;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: var(--dark);
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
        }
        
        .header-desc {
            font-size: 1.2rem;
            max-width: 800px;
            margin: 0 auto;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 25px;
        }
        
        @media (max-width: 992px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .subjects-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px;
        }
        
        .subject-card {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .subject-card:hover {
            transform: translateY(-7px);
            box-shadow: 0 12px 20px rgba(0, 0, 0, 0.15);
        }
        
        .subject-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 5px;
            height: 100%;
        }
        
        .subject-card.anatomy::before { background-color: var(--anatomy); }
        .subject-card.physiology::before { background-color: var(--physiology); }
        .subject-card.chemistry::before { background-color: var(--chemistry); }
        .subject-card.histology::before { background-color: var(--histology); }
        .subject-card.embryology::before { background-color: var(--embryology); }
        .subject-card.ethics::before { background-color: var(--ethics); }
        .subject-card.baath::before { background-color: var(--baath); }
        
        .subject-title {
            font-size: 1.6rem;
            margin-bottom: 20px;
            text-align: center;
            padding-bottom: 15px;
            border-bottom: 2px dashed #eee;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .subject-card.anatomy .subject-title { color: var(--anatomy); }
        .subject-card.physiology .subject-title { color: var(--physiology); }
        .subject-card.chemistry .subject-title { color: var(--chemistry); }
        .subject-card.histology .subject-title { color: var(--histology); }
        .subject-card.embryology .subject-title { color: var(--embryology); }
        .subject-card.ethics .subject-title { color: var(--ethics); }
        .subject-card.baath .subject-title { color: var(--baath); }
        
        .input-group {
            margin-bottom: 18px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            justify-content: space-between;
        }
        
        .max-grade {
            color: var(--gray);
            font-weight: normal;
        }
        
        input[type="number"] {
            width: 100%;
            padding: 14px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1.1rem;
            transition: border-color 0.3s;
        }
        
        input[type="number"]:focus {
            border-color: var(--primary);
            outline: none;
        }
        
        .calculate-btn {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 14px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1rem;
            width: 100%;
            transition: opacity 0.3s;
            font-weight: 600;
            margin-top: 10px;
        }
        
        .calculate-btn:hover {
            opacity: 0.9;
        }
        
        .result {
            margin-top: 20px;
            padding: 18px;
            background-color: var(--light);
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
            font-size: 1.3rem;
            display: none;
            border: 2px solid #eee;
        }
        
        .sidebar {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            height: fit-content;
            position: sticky;
            top: 20px;
        }
        
        .sidebar-title {
            font-size: 1.8rem;
            color: var(--primary);
            margin-bottom: 20px;
            text-align: center;
            padding-bottom: 15px;
            border-bottom: 2px dashed #eee;
        }
        
        .total-result {
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #3498db 0%, #2ecc71 100%);
            color: white;
            border-radius: 12px;
            margin-top: 25px;
            display: none;
        }
        
        .total-result h2 {
            margin-bottom: 15px;
            font-size: 1.8rem;
        }
        
        .subject-result {
            display: flex;
            justify-content: space-between;
            padding: 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .subject-result:last-child {
            border-bottom: none;
        }
        
        .overall-average {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 2px solid rgba(255, 255, 255, 0.3);
            font-size: 1.5rem;
        }
        
        .progress-bar {
            height: 10px;
            background: #e0e0e0;
            border-radius: 5px;
            margin-top: 10px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            border-radius: 5px;
            transition: width 0.5s ease;
        }
        
        .progress-fill.excellent { background: #2ecc71; }
        .progress-fill.very-good { background: #3498db; }
        .progress-fill.good { background: #f1c40f; }
        .progress-fill.pass { background: #e67e22; }
        .progress-fill.fail { background: #e74c3c; }
        
        .grade-status {
            display: flex;
            justify-content: space-between;
            margin-top: 5px;
            font-size: 0.9rem;
            color: var(--gray);
        }
        
        .save-load-container {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        
        .save-btn, .load-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: opacity 0.3s;
        }
        
        .save-btn {
            background: var(--secondary);
            color: white;
        }
        
        .load-btn {
            background: var(--primary);
            color: white;
        }
        
        .save-btn:hover, .load-btn:hover {
            opacity: 0.9;
        }
        
        .instructions {
            background: #fff8e1;
            padding: 20px;
            border-radius: 8px;
            margin-top: 25px;
            border-right: 5px solid #ffc107;
        }
        
        .instructions h3 {
            color: #ff9800;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .instructions ul {
            padding-right: 20px;
            line-height: 1.8;
        }
        
        .instructions li {
            margin-bottom: 10px;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: var(--gray);
        }
        
        @media (max-width: 768px) {
            .subjects-container {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-graduation-cap"></i> نظام متابعة وحساب الدرجات الدراسية</h1>
            <p class="header-desc">أدخل درجاتك لكل مادة وسيقوم النظام بحساب النتائج النهائية وتقديم إحصائيات مفصلة عن أدائك</p>
        </header>
        
        <div class="main-content">
            <div class="subjects-container">
                <!-- التشريح -->
                <div class="subject-card anatomy">
                    <h3 class="subject-title"><i class="fas fa-brain"></i> التشريح</h3>
                    <div class="input-group">
                        <label>العملي المد <span class="max-grade">(10 درجة)</span></label>
                        <input type="number" id="anatomy_practical_mid" min="0" max="10" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري المد <span class="max-grade">(20 درجة)</span></label>
                        <input type="number" id="anatomy_theoretical_mid" min="0" max="20" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>العملي الفاينل <span class="max-grade">(20 درجة)</span></label>
                        <input type="number" id="anatomy_practical_final" min="0" max="20" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري الفاينل <span class="max-grade">(50 درجة)</span></label>
                        <input type="number" id="anatomy_theoretical_final" min="0" max="50" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculateAnatomy()">حساب درجة التشريح</button>
                    <div class="result" id="anatomy_result"></div>
                </div>
                
                <!-- الفسلجة -->
                <div class="subject-card physiology">
                    <h3 class="subject-title"><i class="fas fa-heartbeat"></i> الفسلجة</h3>
                    <div class="input-group">
                        <label>العملي المد <span class="max-grade">(10 درجة)</span></label>
                        <input type="number" id="physiology_practical_mid" min="0" max="10" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري المد <span class="max-grade">(25 درجة)</span></label>
                        <input type="number" id="physiology_theoretical_mid" min="0" max="25" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>العملي الفاينل <span class="max-grade">(10 درجة)</span></label>
                        <input type="number" id="physiology_practical_final" min="0" max="10" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري الفاينل <span class="max-grade">(50 درجة)</span></label>
                        <input type="number" id="physiology_theoretical_final" min="0" max="50" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>السمنر <span class="max-grade">(2 درجة)</span></label>
                        <input type="number" id="physiology_seminar" min="0" max="2" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>الكوزات <span class="max-grade">(3 درجة)</span></label>
                        <input type="number" id="physiology_quizzes" min="0" max="3" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculatePhysiology()">حساب درجة الفسلجة</button>
                    <div class="result" id="physiology_result"></div>
                </div>
                
                <!-- الكيمياء -->
                <div class="subject-card chemistry">
                    <h3 class="subject-title"><i class="fas fa-flask"></i> الكيمياء</h3>
                    <div class="input-group">
                        <label>العملي المد <span class="max-grade">(13 درجة)</span></label>
                        <input type="number" id="chemistry_practical_mid" min="0" max="13" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري المد <span class="max-grade">(20 درجة)</span></label>
                        <input type="number" id="chemistry_theoretical_mid" min="0" max="20" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>العملي الفاينل <span class="max-grade">(13 درجة)</span></label>
                        <input type="number" id="chemistry_practical_final" min="0" max="13" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري الفاينل <span class="max-grade">(50 درجة)</span></label>
                        <input type="number" id="chemistry_theoretical_final" min="0" max="50" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>السمنر/البوستر <span class="max-grade">(4 درجة)</span></label>
                        <input type="number" id="chemistry_seminar" min="0" max="4" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculateChemistry()">حساب درجة الكيمياء</button>
                    <div class="result" id="chemistry_result"></div>
                </div>
                
                <!-- الأنسجة -->
                <div class="subject-card histology">
                    <h3 class="subject-title"><i class="fas fa-microscope"></i> الأنسجة</h3>
                    <div class="input-group">
                        <label>العملي المد <span class="max-grade">(10 درجة)</span></label>
                        <input type="number" id="histology_practical_mid" min="0" max="10" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري المد <span class="max-grade">(20 درجة)</span></label>
                        <input type="number" id="histology_theoretical_mid" min="0" max="20" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>العملي الفاينل <span class="max-grade">(13 درجة)</span></label>
                        <input type="number" id="histology_practical_final" min="0" max="13" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>النظري الفاينل <span class="max-grade">(55 درجة)</span></label>
                        <input type="number" id="histology_theoretical_final" min="0" max="55" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>لوك بوك <span class="max-grade">(2 درجة)</span></label>
                        <input type="number" id="histology_lookbook" min="0" max="2" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculateHistology()">حساب درجة الأنسجة</button>
                    <div class="result" id="histology_result"></div>
                </div>
                
                <!-- الأجنة -->
                <div class="subject-card embryology">
                    <h3 class="subject-title"><i class="fas fa-baby"></i> الأجنة</h3>
                    <div class="input-group">
                        <label>امتحان المد <span class="max-grade">(30 درجة)</span></label>
                        <input type="number" id="embryology_mid" min="0" max="30" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>امتحان الفاينل <span class="max-grade">(70 درجة)</span></label>
                        <input type="number" id="embryology_final" min="0" max="70" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculateEmbryology()">حساب درجة الأجنة</button>
                    <div class="result" id="embryology_result"></div>
                </div>
                
                <!-- أخلاقيات الطب -->
                <div class="subject-card ethics">
                    <h3 class="subject-title"><i class="fas fa-hand-holding-heart"></i> أخلاقيات الطب</h3>
                    <div class="input-group">
                        <label>امتحان المد <span class="max-grade">(30 درجة)</span></label>
                        <input type="number" id="ethics_mid" min="0" max="30" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <div class="input-group">
                        <label>امتحان الفاينل <span class="max-grade">(70 درجة)</span></label>
                        <input type="number" id="ethics_final" min="0" max="70" step="0.5" placeholder="أدخل الدرجة">
                    </div>
                    <button class="calculate-btn" onclick="calculateEthics()">حساب درجة الأخلاقيات</button>
                    <div class="result" id="ethics_result"></div>
                </div>
                
                <!-- جرائم حزب البعث -->
                <div class="subject-card baath">
                    <h3 class="subject-title"><i class="fas fa-gavel"></i> جرائم حزب البعث</h3>
                    <div class="input-group">
                        <label>امتحان المد <span class="max-grad
