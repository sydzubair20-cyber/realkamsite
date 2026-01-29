<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>realkamsite</title>
<style>
body{
  margin:0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#ff4da6,#ff99cc);
  color:white;
  text-align:center;
}

header{
  padding:20px;
  font-size:28px;
  font-weight:bold;
  animation: glow 2s infinite alternate;
}

@keyframes glow{
  from{ text-shadow:0 0 10px white; }
  to{ text-shadow:0 0 25px yellow; }
}

.robot{
  font-size:80px;
  margin:10px 0;
  animation: float 3s ease-in-out infinite;
}

@keyframes float{
  0%,100%{ transform:translateY(0); }
  50%{ transform:translateY(-10px); }
}

.card{
  background:white;
  color:black;
  margin:15px auto;
  padding:15px;
  width:90%;
  max-width:400px;
  border-radius:15px;
  box-shadow:0 5px 15px rgba(0,0,0,0.2);
}

input,button{
  width:90%;
  padding:10px;
  margin:5px 0;
  border-radius:8px;
  border:none;
}

button{
  background:#ff4da6;
  color:white;
  font-weight:bold;
  cursor:pointer;
}

.template-box{
  background:#fff0f5;
  margin:10px;
  padding:10px;
  border-radius:10px;
}

img{
  max-width:100%;
  border-radius:10px;
}
</style>
</head>

<body>

<header>realkamsite - Reels Editing Templates</header>
<div class="robot">🤖</div>

<div class="card">
  <h3>Add Template</h3>
  <input type="text" id="templateLink" placeholder="Paste template link"/>
  <input type="file" id="qrUpload" accept="image/*"/>
  <button onclick="saveTemplate()">Upload</button>
</div>

<div id="templates"></div>

<script>
let templates = JSON.parse(localStorage.getItem("templates")) || [];

function saveTemplate(){
  const link = document.getElementById("templateLink").value;
  const fileInput = document.getElementById("qrUpload");
  const reader = new FileReader();

  reader.onload = function(){
    templates.push({link:link, qr:reader.result});
    localStorage.setItem("templates", JSON.stringify(templates));
    showTemplates();
  };

  if(fileInput.files[0]){
    reader.readAsDataURL(fileInput.files[0]);
  }
}

function showTemplates(){
  const box = document.getElementById("templates");
  box.innerHTML="";
  templates.forEach(t=>{
    box.innerHTML += `
      <div class="template-box">
        <a href="${t.link}" target="_blank">Open Template</a>
        <img src="${t.qr}" />
      </div>
    `;
  });
}

showTemplates();
</script>

</body>
</html>
