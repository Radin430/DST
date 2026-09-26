<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DS5 | PS5 DNS</title>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}

body{
  font-family:Tahoma,Arial,sans-serif;
  background:#05070b;
  color:white;
  min-height:100vh;
  overflow-x:hidden;
}

/* پس‌زمینه */
body::before{
  content:"";
  position:fixed;
  width:500px;
  height:500px;
  background:#00ff8840;
  filter:blur(130px);
  border-radius:50%;
  top:-180px;
  right:-150px;
  z-index:-1;
}

body::after{
  content:"";
  position:fixed;
  width:450px;
  height:450px;
  background:#00aaff30;
  filter:blur(140px);
  border-radius:50%;
  bottom:-180px;
  left:-150px;
  z-index:-1;
}

/* هدر */
header{
  position:sticky;
  top:0;
  z-index:10;
  backdrop-filter:blur(15px);
  background:#05070bcc;
  border-bottom:1px solid #ffffff12;
  padding:18px 7%;
  display:flex;
  justify-content:space-between;
  align-items:center;
}

.logo{
  font-size:34px;
  font-weight:900;
  letter-spacing:3px;
  color:#62ff9b;
  text-shadow:0 0 25px #00ff88;
}

.logo span{
  color:white;
}

.status{
  color:#62ff9b;
  font-size:13px;
  border:1px solid #62ff9b55;
  padding:8px 14px;
  border-radius:30px;
  background:#62ff9b0d;
}

/* هیرو */
.hero{
  text-align:center;
  padding:90px 20px 60px;
}

.hero .tag{
  display:inline-block;
  padding:9px 16px;
  border-radius:30px;
  background:#62ff9b12
