<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>سما بغداد</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{
 font-family:Tahoma;
 direction:rtl;
 background:#eef2f3;
 padding:10px
}
.box{
 background:#fff;
 padding:15px;
 border-radius:10px;
 max-width:400px;
 margin:auto
}
h2{text-align:center;color:#006}
input,textarea,button{
 width:100%;
 padding:10px;
 margin:5px 0;
 font-size:15px
}
button{
 background:#006;
 color:#fff;
 border:none;
 border-radius:5px
}
.item{
 background:#f5f5f5;
 padding:8px;
 margin-top:5px;
 border-radius:5px
}
</style>
</head>

<body>

<div class="box">
<h2>سما بغداد</h2>

<input id="shop" placeholder="اسم المحل">
<input id="phone" placeholder="رقم الهاتف">
<textarea id="note" placeholder="ملاحظات"></textarea>

<button onclick="getLocation()">📍 أخذ الموقع</button>
<button onclick="takePhoto()">📸 إضافة صورة</button>
<button onclick="save()">💾 حفظ الزيارة</button>

<div id="msg"></div>

<hr>
<div id="list"></div>
</div>

<script>
let locationText="غير محدد";
let photoCount=0;

function getLocation(){
 if(!navigator.geolocation){
  msg.innerText="الموقع غير مدعوم";
  return;
 }
 navigator.geolocation.getCurrentPosition(
  p=>{
   locationText =
   p.coords.latitude + "," + p.coords.longitude;
   msg.innerText="تم حفظ الموقع";
  },
  e=>{
   msg.innerText="لم يتم السماح بالموقع";
  }
 );
}

function takePhoto(){
 let i=document.createElement("input");
 i.type="file";
 i.accept="image/*";
 i.capture="environment";
 i.onchange=()=>{
  photoCount++;
  msg.innerText="تمت إضافة صورة";
 };
 i.click();
}

function save(){
 if(!shop.value || !phone.value){
  msg.innerText="أدخل اسم المحل ورقم الهاتف";
  return;
 }

 let d=new Date().toLocaleString();
 let data={
  shop:shop.value,
  phone:phone.value,
  note:note.value,
  loc:locationText,
  date:d
 };

 localStorage.setItem(Date.now(),JSON.stringify(data));
 show();
 msg.innerText="تم حفظ الزيارة";
}

function show(){
 list.innerHTML="";
 Object.keys(localStorage).forEach(k=>{
  let v=JSON.parse(localStorage[k]);
  list.innerHTML+=`
  <div class="item">
   <b>${v.shop}</b><br>
   📞 ${v.phone}<br>
   🕒 ${v.date}<br>
   📍 ${v.loc}
  </div>`;
 });
}
show();
</script>

</body>
</html>
