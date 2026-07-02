<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>بحث عن الآية - جيب اسم السورة</title>
<style>
    body {
        font-family: 'Amiri', serif;
        background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        margin: 0;
        padding: 20px;
    }
   .card {
        background: white;
        padding: 30px;
        border-radius: 20px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        max-width: 650px;
        width: 100%;
        text-align: center;
    }
    h1 { color: #1565c0; margin-bottom: 10px; }
    p { color: #555; margin-bottom: 20px; }
    textarea {
        width: 95%;
        height: 90px;
        padding: 12px;
        font-size: 22px;
        border: 3px solid #64b5f6;
        border-radius: 12px;
        text-align: center;
        font-family: 'Amiri', serif;
        resize: none;
    }
    textarea:focus { outline: none; border-color: #1976d2; }
    button {
        background: #1976d2;
        color: white;
        border: none;
        padding: 14px 35px;
        font-size: 20px;
        border-radius: 12px;
        cursor: pointer;
        margin-top: 15px;
        transition: 0.3s;
        font-weight: bold;
    }
    button:hover { background: #0d47a1; transform: scale(1.05); }
    #result {
        margin-top: 25px;
        font-size: 26px;
        line-height: 2.2;
        color: #0d47a1;
        min-height: 70px;
        font-weight: bold;
    }
    #details {
        color: #2e7d32;
        font-size: 18px;
        margin-top: 12px;
        background: #e8f5e9;
        padding: 10px;
        border-radius: 8px;
    }
   .hint { font-size: 14px; color: #777; margin-top: 10px; }
</style>
</head>
<body>
<div class="card">
    <h1>🔍 ابحث عن اسم السورة</h1>
    <p>اكتب أي جزء من الآية حتى لو كلمتين بس</p>

    <textarea id="ayahInput" placeholder="مثال: تبارك الذي، قل هو الله، والشمس تجري"></textarea>
    <br>
    <button onclick="searchAyah()">جيب لي اسم السورة</button>

    <div id="result"></div>
    <div id="details"></div>
    <div class="hint">💡 اكتبي بدون تشكيل للحصول على نتيجة أدق</div>
</div>

<script>
// قاعدة بيانات الآيات - زيدي فيها براحتك
const quranDB = [const quranDB=[
{surah:"الملك",quarter:"سورة كاملة",ayahs:["تبارك الذي بيده الملك","الذي خلق الموت والحياة"]},
{surah:"القلم",quarter:"سورة كاملة",ayahs:["ن والقلم وما يسطرون","ما أنت بنعمة ربك بمجنون"]},
{surah:"الحاقة",quarter:"سورة كاملة",ayahs:["الحاقة","ما الحاقة","وما أدراك ما الحاقة"]},
{surah:"المعارج",quarter:"سورة كاملة",ayahs:["سأل سائل بعذاب واقع"]},
{surah:"نوح",quarter:"سورة كاملة",ayahs:["إنا أرسلنا نوحا إلى قومه"]},
{surah:"الجن",quarter:"سورة كاملة",ayahs:["قل أوحي إلي أنه استمع نفر من الجن"]},
{surah:"المزمل",quarter:"سورة كاملة",ayahs:["يا أيها المزمل","قم الليل إلا قليلا"]},
{surah:"المدثر",quarter:"سورة كاملة",ayahs:["يا أيها المدثر","قم فأنذر"]},
{surah:"القيامة",quarter:"سورة كاملة",ayahs:["لا أقسم بيوم القيامة"]},
{surah:"الإنسان",quarter:"سورة كاملة",ayahs:["هل أتى على الإنسان حين من الدهر"]},
{surah:"المرسلات",quarter:"سورة كاملة",ayahs:["والمرسلات عرفا","فالعاصفات عصفا"]}
];
    { surah: "يس", quarter: "الربع الأول 1-27", ayahs: ["يس", "والقرآن الحكيم", "إنك لمن المرسلين", "على صراط مستقيم", "تنزيل العزيز الرحيم", "لتنذر قوما ما أنذر آباؤهم", "إنا نحن نحي الموتى"] },
    { surah: "يس", quarter: "الربع الثاني 28-54", ayahs: ["يا حسرة على العباد", "والشمس تجري لمستقر لها", "والقمر قدرناه منازل"] },
    { surah: "يس", quarter: "الربع الثالث 55-70", ayahs: ["إن أصحاب الجنة اليوم", "سلام قولا من رب رحيم", "وما علمناه الشعر"] },
    { surah: "يس", quarter: "الربع الرابع 71-83", ayahs: ["أولم يروا أنا خلقنا لهم", "قل يحييها الذي أنشأها أول مرة", "فسبحان الذي بيده ملكوت كل شيء"] },
    { surah: "الملك", quarter: "سورة كاملة", ayahs: ["تبارك الذي بيده الملك", "الذي خلق الموت والحياة", "هو الذي جعل لكم الأرض ذلولا"] },
    { surah: "الإخلاص", quarter: "سورة كاملة", ayahs: ["قل هو الله أحد", "الله الصمد", "لم يلد ولم يولد"] },
    { surah: "الفاتحة", quarter: "سورة كاملة", ayahs: ["الحمد لله رب العالمين", "الرحمن الرحيم", "إياك نعبد وإياك نستعين", "اهدنا الصراط المستقيم"] },
    { surah: "الكرسي", quarter: "آية الكرسي - البقرة 255", ayahs: ["الله لا إله إلا هو الحي القيوم", "لا تأخذه سنة ولا نوم", "وسع كرسيه السماوات والأرض"] },
    { surah: "الناس", quarter: "سورة كاملة", ayahs: ["قل أعوذ برب الناس", "ملك الناس", "إله الناس"] },
    { surah: "الفلق", quarter: "سورة كاملة", ayahs: ["قل أعوذ برب الفلق", "من شر ما خلق"] }
];

// دالة تنظيف النص من التشكيل والهمزات
function cleanText(text) {
    return text.replace(/[ًٌٍَُِّْ~ٰٱإأآ]/g, '').replace(/\s+/g, ' ').trim();
}

function searchAyah() {
    let input = document.getElementById('ayahInput').value.trim();
    let resultDiv = document.getElementById('result');
    let detailsDiv = document.getElementById('details');

    if(!input) {
        resultDiv.innerText = "اكتبي جزء من الآية أول 😊";
        detailsDiv.innerText = "";
        return;
    }

    input = cleanText(input);
    let results = [];

    // نلف على كل السور والآيات ونفتش
    for(let item of quranDB) {
        for(let ayah of item.ayahs) {
            let cleanAyah = cleanText(ayah);

            // الشرط الجديد: لو الآية فيها الكلمة المدخلة، أو العكس
            if(cleanAyah.includes(input) || input.includes(cleanAyah.substring(0, 5))) {
                results.push({
                    ayah: ayah,
                    surah: item.surah,
                    quarter: item.quarter
                });
            }
        }
    }

    if(results.length > 0) {
        // نعرض أول نتيجة
        let r = results[0];
        resultDiv.innerHTML = "﴿ " + r.ayah + " ﴾";
        detailsDiv.innerHTML = "📖 <b>سورة: " + r.surah + "</b> | " + r.quarter;

        // لو في نتائج تانية نوري الزول
        if(results.length > 1) {
            detailsDiv.innerHTML += "<br><small>في " + results.length + " نتائج تانية، جربي تكتبي كلمات أكتر</small>";
        }
    } else {
        resultDiv.innerText = "ما لقيت الآية دي في قاعدة البيانات 😔";
        detailsDiv.innerText = "جربي تكتبي أول 3-5 كلمات من الآية بدون تشكيل";
    }
}

// البحث يشتغل بالـ Enter
document.getElementById('ayahInput').addEventListener('keypress', function(e) {
    if(e.key === 'Enter' &&!e.shiftKey) {
        e.preventDefault();
        searchAyah();
    }
});
</script>
</body
