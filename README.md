<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أحبك ❤️</title>
    <style>
        /* التنظيف الأساسي */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        /* الجسم والخلفية (تم تعديل التدرج اللوني وإضافة حركة) */
        body {
            font-family: 'Arial', sans-serif;
            /* تدرج لوني أعمق وأكثر دفئًا */
            background: linear-gradient(135deg, #7c2d82 0%, #d81b60 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            /* إضافة نبض بسيط للخلفية بالكامل */
            animation: backgroundPulse 10s infinite alternate;
        }
        
        @keyframes backgroundPulse {
            from { background: linear-gradient(135deg, #7c2d82 0%, #d81b60 100%); }
            to { background: linear-gradient(135deg, #d81b60 0%, #7c2d82 100%); }
        }

        /* حاوية المحتوى الرئيسية */
        .container {
            text-align: center;
            /* خلفية بيضاء شبه شفافة */
            background: rgba(255, 255, 255, 0.98);
            padding: 60px 40px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            max-width: 600px;
            /* حركة دخول لطيفة */
            animation: slideIn 0.8s ease-out;
            z-index: 10; /* للتأكد من أنها فوق النجوم */
            position: relative;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px) scale(0.9);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }
        
        /* أيقونة القلب (تم تحديد حجم الخط) */
        .heart {
            font-size: 80px; /* تم تصحيح الوحدة */
            margin-bottom: 20px;
            animation: heartBeat 1.5s infinite;
        }
        
        @keyframes heartBeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }
        
        /* العنوان */
        h1 {
            color: #d81b60; /* لون جديد متناسق */
            font-size: 52px; /* تم تكبيره قليلاً */
            margin-bottom: 20px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        /* الرسالة */
        .message {
            color: #333;
            font-size: 20px; /* تم تصحيح الوحدة */
            line-height: 1.8;
            margin: 15px 0; /* تم تصحيح الوحدة */
            font-weight: 500;
        }
        
        /* النص المميز */
        .special-text {
            color: #7c2d82; /* لون جديد متناسق */
            font-size: 32px; /* تم تكبيره قليلاً */
            margin: 30px 0;
            font-weight: 900; /* جعل الخط أثقل */
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
            transition: color 0.3s ease;
        }
        
        .button-group {
            margin-top: 40px;
            display: flex;
            gap: 25px; /* زيادة التباعد بين الأزرار */
            justify-content: center;
            flex-wrap: wrap;
        }
        
        button {
            padding: 15px 45px; /* زيادة مساحة التعبئة */
            font-size: 19px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            min-width: 150px; /* لضمان اتساق الحجم */
        }
        
        .yes-btn {
            background: #e74c3c;
            color: white;
        }
        
        .yes-btn:hover {
            background: #c0392b;
            transform: scale(1.1); /* تأثير أكبر عند التحويم */
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.3);
        }
        
        .no-btn {
            background: #95a5a6;
            color: white;
            position: relative; /* مهم لـ JS */
        }
        
        .no-btn:hover {
            background: #7f8c8d;
        }
        
        /* تأثيرات النجوم (تم تحسين الرسوم المتحركة) */
        .stars {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: 5;
        }
        
        .star {
            position: absolute;
            width: 3px; /* نجوم أكبر قليلاً */
            height: 3px;
            background: white;
            border-radius: 50%;
            opacity: 0;
            animation: twinkle 5s infinite;
            box-shadow: 0 0 5px rgba(255, 255, 255, 0.8);
        }
        
        @keyframes twinkle {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1); }
            100% { opacity: 0; transform: scale(0.5); }
        }
    </style>
</head>
<body>
    <div class="stars" id="stars"></div>
    
    <div class="container">
        <div class="heart">❤️</div>
        <h1>أحبك</h1>
        <div class="message">
            أنتِ أجمل شيء في حياتي، أنتِ كل أحلامي!
        </div>
        <div class="special-text">
            هل تقبلين حبي؟
        </div>
        <div class="button-group">
            <button class="yes-btn" onclick="handleYes()">نعم ❤️</button>
            <button class="no-btn" id="noButton" onclick="handleNo(event)">لا</button>
        </div>
    </div>
    
    <script>
        // إنشاء نجوم عشوائية (تمت زيادة حجمها وتأخيرها)
        function createStars() {
            const starsContainer = document.getElementById('stars');
            for (let i = 0; i < 70; i++) { // زيادة عدد النجوم
                const star = document.createElement('div');
                star.className = 'star';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                // زيادة عشوائية لتأخير الرسوم المتحركة
                star.style.animationDelay = Math.random() * 5 + 's'; 
                starsContainer.appendChild(star);
            }
        }
        
        function handleYes() {
            const container = document.querySelector('.container');
            
            // تغيير محتوى الصفحة إلى رسالة تهنئة
            container.innerHTML = `
                <div class="heart" style="font-size: 100px; animation: none;">🎉</div>
                <h1>أجمل قرار!</h1>
                <div class="message" style="font-size: 22px;">
                    لقد جعلتِ حياتي مضيئة! أنا سعيد للغاية يا عمري.
                </div>
                <div class="special-text" style="color: #1abc9c;">
                    أحبك إلى الأبد.
                </div>
            `;
            // إيقاف نبض الخلفية والقلب
            document.body.style.animation = 'none';
        }
        
        let noClicks = 0;
        function handleNo(event) {
            const btn = event.target;
            noClicks++;
            
            if (noClicks < 3) {
                // الحركة العشوائية لمرتين فقط
                btn.style.transition = 'all 0.2s ease-out';
                btn.style.position = 'absolute';
                
                // تحديد حدود للحركة ليبقى داخل الشاشة
                const newLeft = Math.random() * (window.innerWidth - btn.offsetWidth - 50);
                const newTop = Math.random() * (window.innerHeight - btn.offsetHeight - 50);
                
                btn.style.left = newLeft + 'px';
                btn.style.top = newTop + 'px';
            } else {
                // بعد المحاولة الثالثة، يختفي الزر نهائياً
                btn.style.transition = 'opacity 0.5s, transform 0.5s';
                btn.style.opacity = '0';
                btn.style.transform = 'scale(0)';
                
                // رسالة إضافية بسيطة 
                setTimeout(() => {
                    alert('لقد اختفى خيار "لا" الآن! ❤️');
                }, 500);
            }
        }
        
        // تشغيل وظيفة إنشاء النجوم عند تحميل الصفحة
        createStars();
    </script>
</body>
</html>
