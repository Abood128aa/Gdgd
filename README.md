<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مفاجأة خاصة</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --main-color: #ff4d6d;
            --secondary-color: #ff758f;
            --bg-gradient: linear-gradient(135deg, #fff1f2 0%, #ffd1dc 100%);
        }

        body {
            margin: 0; padding: 0;
            display: flex; justify-content: center; align-items: center;
            min-height: 100vh;
            font-family: 'Tajawal', sans-serif;
            background: var(--bg-gradient);
            overflow: hidden;
        }

        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.8);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
            max-width: 400px; width: 90%;
            border: 2px solid white;
            z-index: 10;
        }

        /* تنسيق الصورة القابلة للتكبير */
        .img-wrapper {
            cursor: zoom-in;
            margin-bottom: 20px;
            display: inline-block;
        }

        .profile-img {
            width: 150px;
            height: 150px;
            border-radius: 20px; /* زوايا منحنية بدلاً من دائرة كاملة لتبدو احترافية */
            border: 4px solid white;
            object-fit: cover;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .profile-img:hover {
            transform: scale(1.05);
        }

        h1 { color: #4a4a4a; font-size: 22px; margin-bottom: 25px; }

        .buttons-container { display: flex; flex-direction: column; gap: 15px; }

        .btn {
            text-decoration: none; padding: 15px 25px;
            border-radius: 50px; font-weight: bold;
            transition: all 0.3s ease; cursor: pointer;
            border: none; font-size: 16px; text-align: center;
        }

        .btn-profile { background-color: #1877f2; color: white; }
        .btn-surprise { background-color: var(--main-color); color: white; box-shadow: 0 5px 15px rgba(255, 77, 109, 0.4); }

        /* نافذة التكبير (Full Screen Image) */
        #image-overlay {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); justify-content: center; align-items: center;
            z-index: 2000; cursor: zoom-out;
        }

        #image-overlay img {
            max-width: 90%; max-height: 90%;
            border-radius: 10px; box-shadow: 0 0 30px rgba(255,255,255,0.2);
            animation: zoomIn 0.3s ease;
        }

        /* نافذة المفاجأة */
        #surprise-overlay {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85); justify-content: center; align-items: center;
            z-index: 1000; color: white; text-align: center; padding: 20px;
        }

        .heart { position: absolute; color: var(--main-color); font-size: 20px; pointer-events: none; animation: fall linear forwards; }

        @keyframes zoomIn { from { transform: scale(0.5); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        @keyframes fall { to { transform: translateY(100vh) rotate(360deg); } }
    </style>
</head>
<body>

    <div class="container">
        <div class="img-wrapper" onclick="openLightbox()">
            <img src="https://i.ibb.co/5WgXmYqc/FB-IMG-1772058101659.jpg" alt="Special Image" class="profile-img">
        </div>
        
        <h1>أهلاً بكِ في هذه المساحة الخاصة ✨</h1>
        
        <div class="buttons-container">
            <a href="https://www.facebook.com/share/18CFRsDyg2/" target="_blank" class="btn btn-profile">زيارة الحساب الشخصي 👤</a>
            <button onclick="showSurprise()" class="btn btn-surprise">اكتشفي المفاجأة 🎁</button>
        </div>
    </div>

    <div id="image-overlay" onclick="closeLightbox()">
        <img src="https://i.ibb.co/5WgXmYqc/FB-IMG-1772058101659.jpg" alt="Zoomed Image">
    </div>

    <div id="surprise-overlay" onclick="this.style.display='none'">
        <div>
            <h2 id="typing-text" style="font-size: 1.8rem; line-height: 1.6;"></h2>
            <p style="margin-top: 20px; color: #ff758f;">(اضغطي في أي مكان للإغلاق)</p>
        </div>
    </div>

    <script>
        function openLightbox() {
            document.getElementById('image-overlay').style.display = 'flex';
        }

        function closeLightbox() {
            document.getElementById('image-overlay').style.display = 'none';
        }

        function showSurprise() {
            document.getElementById('surprise-overlay').style.display = 'flex';
            const text = "كل عام وأنتِ الأجمل.. هذه المفاجأة بسيطة لتعبر عن مكانتك العالية! 🌹✨";
            let i = 0;
            const element = document.getElementById('typing-text');
            element.innerHTML = "";
            
            function typeWriter() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(typeWriter, 80);
                }
            }
            typeWriter();
            createHearts();
        }

        function createHearts() {
            for(let i=0; i<40; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.classList.add('heart');
                    heart.innerHTML = '❤️';
                    heart.style.left = Math.random() * 100 + 'vw';
                    heart.style.animationDuration = Math.random() * 2 + 3 + 's';
                    heart.style.opacity = Math.random();
                    document.body.appendChild(heart);
                    setTimeout(() => heart.remove(), 5000);
                }, i * 150);
            }
        }
    </script>
</body>
</html>
