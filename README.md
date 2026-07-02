<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
<meta charset="UTF-8">
<title>محدد نقاط البيع - للشركات الصغيرة</title>
<style>
body{font-family:'Tajawal',sans-serif;background:linear-gradient(135deg,#667eea,#764ba2);margin:0;padding:20px;min-height:100vh}
.container{max-width:800px;margin:0 auto;background:white;border-radius:20px;padding:35px;box-shadow:0 15px 40px rgba(0,0,0,0.2)}
h1{color:#5a67d8;text-align:center;margin-bottom:10px}
.sub{color:#718096;text-align:center;margin-bottom:30px}
.input-group{margin-bottom:20px}
label{display:block;margin-bottom:8px;color:#2d3748;font-weight:bold}
input,select{width:100%;padding:14px;border:2px solid #e2e8f0;border-radius:12px;font-size:16px;box-sizing:border-box;font-family:'Tajawal',sans-serif}
button{width:100%;background:#667eea;color:white;border:none;padding:16px;font-size:18px;border-radius:12px;cursor:pointer;font-weight:bold;margin-top:10px}
button:hover{background:#5a67d8}
.result{margin-top:30px;display:none}
.card{background:#f7fafc;border-right:5px solid #667eea;padding:20px;border-radius:12px;margin-bottom:15px}
.badge{display:inline-block;background:#c6f6d5;color:#22543d;padding:5px 12px;border-radius:20px;font-size:14px;margin-top:8px}
.tip{background:#fff5f5;border-right:4px solid #fc8181;padding:15px;border-radius:8px;margin-top:20px;color:#742a2a}
</style>
</head>
<body>
<div class="container">
<h1>📍 محدد نقاط البيع الذكي</h1>
<p class="sub">اعرفي أفضل 3 أماكن تبيعي فيها منتجك</p>

<div class="input-group">
<label>اسم شركتك/منتجك</label>
<input type="text" id="company" placeholder="مثال: حلويات سارة">
</div>

<div class="input-group">
<label>نوع المنتج/الخدمة</label>
<select id="type">
<option value="food">أكل ومشروبات</option>
<option value="clothes">ملابس واكسسوارات</option>
<option value="beauty">تجميل وعناية</option>
<option value="electronics">إلكترونيات وجوالات</option>
<option value="services">خدمات</option>
</select>
</div>

<div class="input-group">
<label>المدينة/المنطقة</label>
<input type="text" id="area" placeholder="مثال: عطبرة، سوق كبير">
</div>

<button onclick="findSpots()">حدد لي نقاط البيع</button>

<div id="result" class="result">
<h2 style="color:#2d3748">أفضل 3 مواقع مقترحة:</h2>
<div id="spots"></div>
<div class="tip">💡 نصيحة: ابدي بالموقع رقم 1 لمدة أسبوع، لو المبيعات كويسة ثبتي فيهو</div>
</div>
</div>

<script>
const spotsDB={
food:[
{name:"قرب المدارس والجامعات",reason:"كثافة طلاب عالية + وقت الفسحة",level:"ممتاز"},
{name:"المستشفيات والمراكز الطبية",reason:"زوار + موظفين 24 ساعة",level:"جيد جداً"},
{name:"سوق عطبرة الكبير",reason:"حركة مشي عالية يومياً",level:"ممتاز"}
],
clothes:[
{name:"سوق عطبرة الكبير/المولات",reason:"الناس ماشة للتسوق أصلاً",level:"ممتاز"},
{name:"قرب صالات الأفراح",reason:"مناسبات = شراء ملابس",level:"جيد"},
{name:"جامعة وادي النيل",reason:"الشباب بتابعو الموضة",level:"جيد جداً"}
],
beauty:[
{name:"قرب الكوافيرات في السوق الكبير",reason:"الزبونة جاية تتزين أصلاً",level:"ممتاز"},
{name:"المولات",reason:"بنات بتقضي وقت طويل",level:"ممتاز"},
{name:"جامعة وادي النيل - بنات",reason:"استهداف مباشر",level:"جيد جداً"}
],
electronics:[
{name:"سوق الجوالات عطبرة",reason:"الناس بتقارن الأسعار هناك",level:"ممتاز"},
{name:"قرب جامعة وادي النيل",level:"جيد جداً"},
{name:"شارع الموردة",reason:"ثقة الزبون أعلى",level:"جيد"}
],
services:[
{name:"المناطق الحكومية",reason:"موظفين محتاجين خدمات سريعة",level:"جيد"},
{name:"سوق عطبرة",reason:"الناس بتخلص شغلها وبتطلع",level:"جيد جداً"},
{name:"قرب المواصلات",reason:"نقطة تجمع عالية",level:"ممتاز"}
]
};

function findSpots(){
let company=document.getElementById('company').value.trim();
let type=document.getElementById('type').value;
let area=document.getElementById('area').value.trim();
let resultDiv=document.getElementById('result');
let spotsDiv=document.getElementById('spots');

if(!company ||!area){
alert("اكتبي اسم الشركة والمنطقة أول");
return;
}

let spots=spotsDB[type];
spotsDiv.innerHTML="";

spots.forEach((spot,i)=>{
spotsDiv.innerHTML+=`
<div class="card">
<h3>${i+1}. ${spot.name}</h3>
<p><b>السبب:</b> ${spot.reason}</p>
<p><b>المنطقة:</b> ${area}</p>
<span class="badge">التقييم: ${spot.level}</span>
</div>
`;
});

resultDiv.style.display="block";
resultDiv.scrollIntoView({behavior:"smooth"});
}
</script>
</body>
</html>
