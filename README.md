{ q: "كلمة تصف شعوركِ تجاه عبود الآن؟", a: ["راحة", "عشق", "إدمان"] },
        { q: "هل تعتبرين عبود هو سندكِ في الحياة؟", a: ["نعم، دائماً", "أكيد وبكل قوة", "أكثر من سند"] },
        { q: "ما هو التاريخ الذي لا تنسينه أبداً معنا؟", a: ["يوم اللقاء", "يوم أول كلمة حلوة", "كل يوم معكِ ذكرى"] },
        { q: "لو خيروكِ بين كنوز العالم وبين عبود؟", a: ["عبود طبعاً", "لا يقارن بأحد", "أختار قلبه"] },
        { q: "هل تحبين اهتمام عبود بكِ؟", a: ["أعشقه", "يجعلني سعيدة", "هو سر قوتي"] },
        { q: "ما هو العهد الذي تقطعينه لقلب عبود؟", a: ["البقاء للأبد", "الإخلاص الدائم", "أن لا أحب غيره"] },
        { q: "هل أنتي مستعدة لتكوني أميرة بيت عبود؟", a: ["نعم، وبكل فخر", "هذا حلمي", "بانتظار هذه اللحظة"] }
    ];

    let currentQ = 0;

    function createHeart() {
        const heart = document.createElement('div');
        heart.classList.add('heart');
        heart.innerHTML = '✨';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.animationDuration = Math.random() * 2 + 3 + 's';
        document.body.appendChild(heart);
        setTimeout(() => { heart.remove(); }, 4000);
    }

    function openMessage() {
        // تشغيل المؤثرات (النجوم/القلوب)
        for(let i=0; i<20; i++) {
            setTimeout(createHeart, i * 100);
        }
        document.getElementById('welcome-screen').style.display = 'none';
        document.getElementById('quiz-zone').style.display = 'block';
        updateProgress(1);
    }

    function handleLoveResponse(isYes) {
        const options = document.getElementById('options-container');
        const qText = document.getElementById('question-text');
        
        options.innerHTML = '';
        if(isYes) {
            qText.innerText = "أنا أحبكِ أكثر من كل شيء في هذا الكون، يا أجمل أقداري... 💖";
            const btn = document.createElement('button');
            btn.innerText = "أنا أيضاً... وأكثر! ❤️";
            btn.onclick = nextQuestion;
            options.appendChild(btn);
        } else {
            qText.innerText = "أنجبي تحبيني غصباً عنكِ... قلبي لا يقبل إلا حبكِ! 😉❤️";
            const btn = document.createElement('button');
            btn.innerText = "ههههههه طيب يلا جاوبي 😉";
            btn.onclick = nextQuestion;
            options.appendChild(btn);
        }
    }

    function nextQuestion() {
        if (currentQ < questions.length) {
            const data = questions[currentQ];
            document.getElementById('question-text').innerText = data.q;
            const options = document.getElementById('options-container');
            options.innerHTML = '';
            
            data.a.forEach(ans => {
                const btn = document.createElement('button');
                btn.innerText = ans;
                btn.onclick = () => {
                    currentQ++;
                    createHeart();
                    nextQuestion();
                };
                options.appendChild(btn);
            });
            updateProgress(currentQ + 2);
        } else {
            document.getElementById('quiz-zone').style.display = 'none';
            document.getElementById('final-msg').style.display = 'block';
            setInterval(createHeart, 300); // استمرار المؤثرات في النهاية
        }
    }

    function updateProgress(num) {
        document.getElementById('progress').innerText = خطوة ${num} من 15;
    }
</script>

</body>
</html>
