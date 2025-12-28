<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>سما بغداد</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{font-family:Tahoma;direction:rtl;background:#f4f4f4;padding:15px}
.box{background:#fff;padding:15px;border-radius:8px;max-width:400px;margin:auto}
input,textarea,button{width:100%;padding:10px;margin:5px 0}
button{background:#006;color:#fff;border:none}
</style>
</head>
<body>

<div class="box">
<h2>سما بغداد</h2>

<input id="shop" placeholder="اسم المحل">
<input id="phone" placeholder="رقم الهاتف">
<textarea id="note" placeholder="ملاحظات"></textarea>

<button onclick="savePDF()">حفظ PDF</button>
</div>

<script>
function savePDF(){
 let w=window.open("");
 w.document.write(`
 <h2>سما بغداد</h2>
 <p>اسم المحل: ${shop.value}</p>
 <p>الهاتف: ${phone.value}</p>
 <p>ملاحظات: ${note.value}</p>
 <p>التاريخ: ${new Date().toLocaleString()}</p>
 `);
 w.print();
}
</script>

</body>
</html>
