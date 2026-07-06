<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rajeshwar Plastic Order Form</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700;800&display=swap" rel="stylesheet">
  <style>
    *{margin:0;padding:0;box-sizing:border-box;font-family:Poppins,sans-serif;}
    body{background:linear-gradient(135deg,#0F4C81,#1E88E5);padding:20px;min-height:100vh;}
    .container{max-width:700px;margin:auto;background:white;border-radius:20px;padding:25px;box-shadow:0 10px 30px rgba(0,0,0,.25);}
    .header{display:flex;align-items:center;justify-content:center;gap:15px;margin-bottom:25px;}
    .logo{width:70px;height:70px;border-radius:50%;}
    .company{font-size:34px;font-weight:800;color:#0F4C81;letter-spacing:2px;}
    .input-group{margin-bottom:18px;}
    .input-group label{display:block;font-weight:600;margin-bottom:6px;color:#333;}
    .input-group input{width:100%;padding:12px;border-radius:10px;border:1px solid #ccc;font-size:16px;}
    .order-card{margin-top:20px;background:#F8F9FA;padding:18px;border-radius:15px;border:2px solid #E5E5E5;}
    .order-title{font-size:20px;font-weight:700;color:#0F4C81;margin-bottom:15px;}
    .order-card label{font-weight:600;margin-top:10px;display:block;}
    .order-card select,.order-card input{width:100%;padding:12px;margin-top:5px;border-radius:10px;border:1px solid #ccc;font-size:15px;}
    .button{width:100%;padding:15px;border:none;border-radius:12px;font-size:18px;font-weight:700;cursor:pointer;margin-top:18px;transition:.3s;}
    .add{background:#1565C0;color:white;}
    .add:hover{background:#0D47A1;}
    .send{background:#25D366;color:white;}
    .send:hover{background:#128C7E;}
    .footer{text-align:center;margin-top:20px;font-size:13px;color:#666;}
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <img src="logo.png" class="logo">
      <div class="company">RAJESHWAR PLASTIC</div>
    </div>

    <div class="input-group">
      <label>Party Name *</label>
      <input type="text" id="party">
    </div>

    <div class="input-group">
      <label>Phone Number *</label>
      <input type="tel" id="phone">
    </div>

    <div id="orders">
      <div class="order-card">
        <div class="order-title">Order Item 1</div>
        <label>Product</label>
        <select class="product" onchange="changeProduct(this)">
          <option>Select Product</option>
          <option>LD Bag</option>
          <option>PP Bag</option>
          <option>100g Bag</option>
          <option>50g Bag</option>
          <option>HM Bag</option>
          <option>Corrugated Roll</option>
          <option>Sutli</option>
          <option>Patti</option>
          <option>Clip</option>
          <option>Marker</option>
          <option>Color</option>
        </select>
        <label>Size / Type</label>
        <select class="size"><option>Select Product First</option></select>
        <label>Quantity</label>
        <input type="text" class="qty" placeholder="Enter Quantity">
      </div>
    </div>

    <button class="button add" onclick="addOrder()">+ Add More Order</button>
    <button class="button send" onclick="sendWhatsApp()">Send Order On WhatsApp</button>
    <div class="footer">Rajeshwar Plastic © 2026</div>
  </div>

<script>
let orderCount=1;

function addOrder(){
  orderCount++;
  const orderHTML=`
    <div class="order-card">
      <div class="order-title">Order Item ${orderCount}</div>
      <label>Product</label>
      <select class="product" onchange="changeProduct(this)">
        <option>Select Product</option>
        <option>LD Bag</option>
        <option>PP Bag</option>
        <option>HM Bag</option>
        <option>Corrugated Roll</option>
        <option>Sutli</option>
        <option>Patti</option>
        <option>Clip</option>
        <option>Marker</option>
        <option>Color</option>
      </select>
      <label>Size / Type</label>
      <select class="size"><option>Select Product First</option></select>
      <label>Quantity</label>
      <input type="text" class="qty" placeholder="Enter Quantity">
      <button style="margin-top:15px;background:#E53935;color:white;padding:10px;width:100%;border:none;border-radius:10px;font-weight:bold;cursor:pointer;" onclick="this.parentElement.remove()">Remove Order</button>
    </div>`;
  document.getElementById("orders").insertAdjacentHTML("beforeend",orderHTML);
}

function changeProduct(select){
  const card=select.parentElement;
  const size=card.querySelector(".size");
  const qty=card.querySelector(".qty");
  size.innerHTML="";
  size.style.display="block";
  let value=select.value;

  if(value=="LD Bag"||value=="PP Bag"||value=="HM Bag"){
    size.innerHTML="<option>Custom Size</option>";
    size.insertAdjacentHTML("afterend",'<input class="customSize" placeholder="Enter Size Example 6×8">');
    qty.placeholder="Enter Quantity in KG";
    return;
  }
  card.querySelectorAll(".customSize").forEach(e=>e.remove());

  function addOptions(arr){arr.forEach(item=>{size.innerHTML+=`<option>${item}</option>`;});}

  if(value=="Corrugated Roll"){addOptions(["24","36","40"]);qty.placeholder="Enter Quantity in Rolls";}
  if(value=="Sutli"){addOptions(["Neha","Dolphin","Packer"]);qty.placeholder="Enter Quantity in KG";}
  if(value=="Patti"){addOptions(["2 KG Patti","10 KG Patti"]);qty.placeholder="Enter Quantity in Bundles";}
  if(value=="Clip"){size.innerHTML="<option>No Size Required</option>";qty.placeholder="Enter Quantity in KG";}
  if(value=="Marker"){addOptions(["Red","Blue","Black"]);qty.placeholder="Enter Quantity in Pieces / Boxes";}
  if(value=="Color"){addOptions(["Pink 100G","Pink 500G","Pink 1KG","Blue 100G","Blue 500G","Blue 1KG","Green 100G","Green 500G","Green 1KG"]);qty.placeholder="Enter Quantity in Boxes";}
}

function sendWhatsApp(){
  let party=document.getElementById("party").value.trim();
  let phone=document.getElementById("phone").value.trim();
  if(party==""){alert("Please Enter Party Name");return;}
  if(phone==""){alert("Please Enter Phone Number");return;}

  let msg="*RAJESHWAR PLASTIC ORDER*%0A%0A";
  msg+="*Party Name:* "+party+"%0A";
  msg+="*Phone:* "+phone+"%0A%0A";

  let cards=document.querySelectorAll(".order-card");
  cards.forEach(function(card,index){
    let product=card.querySelector(".product").value;
    if(product=="Select Product") return;
    let size="";
    let custom=card.querySelector(".customSize");
    if(custom){size=custom.value;}else{size=card.querySelector(".size").value;}
    let qty=card.querySelector(".qty").value;
    if(qty=="") return;
    msg+=(index+1)+". "+product+"%0A";
    if(product!="Clip"){msg+="Type/Size : "+size+"%0A";}
    msg+="Quantity : "+qty+"%0A%0A";
  });

  window.open("https://wa.me/9594459534/?text="+msg,"_blank");
}
</script>
</body>
</html>
