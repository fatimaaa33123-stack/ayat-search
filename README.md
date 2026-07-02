<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
<meta charset="UTF-8">
<title>بحث عن الآية - جزء تبارك</title>
<style>
body{font-family:'Amiri',serif;background:linear-gradient(135deg,#e3f2fd,#bbdefb);display:flex;justify-content:center;align-items:center;min-height:100vh;margin:0;padding:20px}
.card{background:white;padding:35px;border-radius:25px;text-align:center;max-width:650px;width:100%;box-shadow:0 8px 25px rgba(0,0,0,0.15)}
h1{color:#1565c0;margin-bottom:25px}
textarea{width:95%;height:100px;font-size:24px;border:3px solid #64b5f6;border-radius:15px;text-align:center;padding:10px;font-family:'Amiri',serif}
button{background:#1976d2;color:white;border:none;padding:16px 40px;font-size:22px;border-radius:15px;margin-top:20px;cursor:pointer;font-weight:bold}
button:hover{background:#1565c0}
#result{margin-top:30px;font-size:28px;color:#0d47a1;font-weight:bold;min-height:50px}
#details{color:#2e7d32;font-size:20px;margin-top:15px;background:#e8f5e9;padding:12px;border-radius:10px}
</style>
</head>
<body>
<div class="card">
<h1>🔍 ابحث عن اسم السورة - جزء تبارك</h1>
<textarea id="ayahInput" placeholder="اكتبي أول 3 كلمات من الآية: تبارك الذي، ن والقلم"></textarea><br>
<button onclick="searchAyah()">جيب لي اسم السورة</button>
<div id="result"></div><div id="details"></div>
</div>
<script>
const quranDB=[
{surah:"الملك",ayahs:["تبارك الذي بيده الملك","الذي خلق الموت والحياة"]},
{surah:"القلم",ayahs:["ن والقلم وما يسطرون","ما أنت بنعمة ربك بمجنون"]},
{surah:"الحاقة",ayahs:["الحاقة","ما الحاقة","وما أدراك ما الحاقة"]},
{surah:"المعارج",ayahs:["سأل سائل بعذاب واقع","للكافرين ليس له دافع"]},
{surah:"نوح",ayahs:["إنا أرسلنا نوحا إلى قومه","أن أنذر قومك"]},
{surah:"الجن",ayahs:["قل أوحي إلي أنه استمع نفر من الجن","فقالوا إنا سمعنا قرآنا عجبا"]},
{surah:"المزمل",ayahs:["يا أيها المزمل","قم الليل إلا قليلا"]},
{surah:"المدثر",ayahs:["يا أيها المدثر","قم فأنذر"]},
{surah:"القيامة",ayahs:["لا أقسم بيوم القيامة","ولا أقسم بالنفس اللوامة"]},
{surah:"الإنسان",ayahs:["هل أتى على الإنسان حين من الدهر","إنا خلقنا الإنسان من نطفة"]},
{surah:"المرسلات",ayahs:["والمرسلات عرفا","فالعاصفات عصفا"]},
{surah:"النبأ",ayahs:["عم يتساءلون","عن النبأ العظيم"]},
{surah:"النازعات",ayahs:["والنازعات غرقا","والناشطات نشطا"]},
{surah:"عبس",ayahs:["عبس وتولى","أن جاءه الأعمى"]},
{surah:"التكوير",ayahs:["إذا الشمس كورت","وإذا النجوم انكدرت"]},
{surah:"الانفطار",ayahs:["إذا السماء انفطرت","وإذا الكواكب انتثرت"]},
{surah:"المطففين",ayahs:["ويل للمطففين","الذين إذا اكتالوا على الناس"]},
{surah:"الانشقاق",ayahs:["إذا السماء انشقت","وأذنت لربها وحقت"]},
{surah:"البروج",ayahs:["والسماء ذات البروج","واليوم الموعود"]},
{surah:"الطارق",ayahs:["والسماء والطارق","وما أدراك ما الطارق"]},
{surah:"الأعلى",ayahs:["سبح اسم ربك الأعلى","الذي خلق فسوى"]},
{surah:"الغاشية",ayahs:["هل أتاك حديث الغاشية","وجوه يومئذ خاشعة"]},
{surah:"الفجر",ayahs:["والفجر","وليال عشر"]},
{surah:"البلد",ayahs:["لا أقسم بهذا البلد","وأنت حل بهذا البلد"]},
{surah:"الشمس",ayahs:["والشمس وضحاها","والقمر إذا تلاها"]},
{surah:"الليل",ayahs:["والليل إذا يغشى","والنهار إذا تجلى"]},
{surah:"الضحى",ayahs:["والضحى","والليل إذا سجى"]},
{surah:"الشرح",ayahs:["ألم نشرح لك صدرك","ووضعنا عنك وزرك"]},
{surah:"التين",ayahs:["والتين والزيتون","وطور سين"]},
{surah:"العلق",ayahs:["اقرأ باسم ربك الذي خلق","خلق الإنسان من علق"]},
{surah:"القدر",ayahs:["إنا أنزلناه في ليلة القدر","وما أدراك ما ليلة القدر"]},
{surah:"البينة",ayahs:["لم يكن الذين كفروا من أهل الكتاب","حتى تأتيهم البينة"]},
{surah:"الزلزلة",ayahs:["إذا زلزلت الأرض زلزالها","وأخرجت الأرض أثقالها"]},
{surah:"العاديات",ayahs:["والعاديات ضبحا","فالموريات قدحا"]},
{surah:"القارعة",ayahs:["القارعة","ما القارعة"]},
{surah:"التكاثر",ayahs:["ألهاكم التكاثر","حتى زرتم المقابر"]},
{surah:"العصر",ayahs:["والعصر","إن الإنسان لفي خسر"]},
{surah:"الهمزة",ayahs:["ويل لكل همزة لمزة","الذي جمع مالا وعدده"]},
{surah:"الفيل",ayahs:["ألم تر كيف فعل ربك بأصحاب الفيل"]},
{surah:"قريش",ayahs:["لإيلاف قريش","إيلافهم رحلة الشتاء والصيف"]},
{surah:"الماعون",ayahs:["أرأيت الذي يكذب بالدين","فذلك الذي يدع اليتيم"]},
{surah:"الكوثر",ayahs:["إنا أعطيناك الكوثر","فصل لربك وانحر"]},
{surah:"الكافرون",ayahs:["قل يا أيها الكافرون","لا أعبد ما تعبدون"]},
{surah:"النصر",ayahs:["إذا جاء نصر الله والفتح","ورأيت الناس يدخلون"]},
{surah:"المسد",ayahs:["تبت يدا أبي لهب وتب","ما أغنى عنه ماله"]},
{surah:"الإخلاص",ayahs:["قل هو الله أحد","الله الصمد","لم يلد ولم يولد"]},
{surah:"الفلق",ayahs:["قل أعوذ برب الفلق","من شر ما خلق"]},
{surah:"الناس",ayahs:["قل أعوذ برب الناس","ملك الناس","إله الناس"]}
];
function cleanText(t){return t.replace(/[ًٌٍَُِّْ~ٰٱإأآ]/g,'').replace(/\s+/g,' ').trim()}
function searchAyah(){let input=cleanText(document.getElementById('ayahInput').value.trim());let r=document.getElementById('result');let d=document.getElementById('details');if(!input){r.innerText="اكتبي جزء من الآية أول";d.innerText="";return}for(let item of quranDB){for(let ayah of item.ayahs){if(cleanText(ayah).includes(input)){r.innerHTML="﴿ "+ayah+" ﴾";d.innerHTML="📖 سورة: <b>"+item.surah+"</b>";return}}}r.innerText="ما لقيتها 😔";d.innerText="جربي أول 3 كلمات من بداية الآية"}
</script>
</body>
</html>
