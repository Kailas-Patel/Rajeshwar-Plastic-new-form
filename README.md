<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Rajeshwar Plastic Order Form</title>

<style>
body{
    margin:0;
    padding:15px;
    font-family:Arial,sans-serif;
    background:linear-gradient(135deg,#0d47a1,#1976d2,#42a5f5);
}

.container{
    max-width:650px;
    margin:auto;
    background:white;
    border-radius:20px;
    padding:20px;
    box-shadow:0 5px 20px rgba(0,0,0,0.3);
}

.header{
    display:flex;
    align-items:center;
    justify-content:center;
    gap:15px;
    margin-bottom:25px;
}

.logo{
    width:70px;
    height:70px;
    border-radius:50%;
}

.company-name{
    font-size:30px;
    font-weight:900;
    color:#0d47a1;
    letter-spacing:2px;
}

label{
    font-weight:bold;
    margin-top:10px;
    display:block;
}

input,select{
    width:100%;
    padding:12px;
    margin-top:5px;
    margin-bottom:10px;
    border:1px solid #ccc;
    border-radius:10px;
    box-sizing:border-box;
}

.order-row{
    border:2px solid #e0e0e0;
    padding:15px;
    border-radius:15px;
    margin-top:15px;
    background:#f9f9f9;
}

button{
    width:100%;
    padding:15px;
    border:none;
    border-radius:10px;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
}

.add-btn{
    background:#1976d2;
    color:white;
    margin-top:15px;
}

.whatsapp-btn{
    background:#25D366;
    color:white;
    margin-top:15px;
}
</style>
</head>

<body>

<div class="container">

<div class="header">
<img src="logo.png" class="logo">
<div class="company-name">RAJESHWAR PLASTIC</div>
</div>

<label>Party Name *</label>
<input type="text" id="partyName" required>

<label>Phone Number *</label>
<input type="tel" id="phoneNumber" required>

<div id="orders"></div>

<button class="add-btn" onclick="addOrder()">+ Add More Order</button>

<button class="whatsapp-btn" onclick="sendWhatsApp()">
Send Order on WhatsApp
</button>

</div>

<script>

const whatsappNumber="1234567890";

function addOrder(){

let div=document.createElement("div");

div.className="order-row";

div.innerHTML=`

<label>Product</label>
<select class="product" onchange="updateVariety(this)">
<option value="">Select Product</option>
<option>Bag</option>
<option>Corrugated Roll</option>
<option>Sutli</option>
<option>Patti</option>
<option>Clip</option>
<option>Marker</option>
<option>Color</option>
</select>

<label>Variety</label>
<select class="variety">
<option>Select Product First</option>
</select>

<input type="text" class="customVariety"
placeholder="Enter Custom Variety"
style="display:none;">

<label>Quantity</label>
<input type="text" class="quantity"
placeholder="Enter Quantity">

`;

document.getElementById("orders").appendChild(div);
}

function updateVariety(productSelect){

let row=productSelect.parentElement;
let variety=row.querySelector(".variety");
let quantity=row.querySelector(".quantity");
let custom=row.querySelector(".customVariety");

custom.style.display="none";

let product=productSelect.value;

let options=[];

if(product==="Bag"){
options=[
"LD",
"PP",
"HM",
"50G",
"100G",
"150G",
"200G",
"300G",
"Custom"
];
quantity.placeholder="Enter Quantity in KG";
}

if(product==="Corrugated Roll"){
options=["24","36","40"];
quantity.placeholder="Enter Quantity in Rolls";
}

if(product==="Sutli"){
options=["Neha","Dolphin","Packer"];
quantity.placeholder="Enter Quantity in KG";
}

if(product==="Patti"){
options=["2 KG Patti","10 KG Patti"];
quantity.placeholder="Enter Quantity in Bundles";
}

if(product==="Clip"){
options=["Standard"];
quantity.placeholder="Enter Quantity in KG";
}

if(product==="Marker"){
options=["Red","Blue","Black"];
quantity.placeholder="Enter Quantity in Pieces or Boxes";
}

if(product==="Color"){
options=[
"Pink 100G",
"Pink 500G",
"Pink 1KG",
"Blue 100G",
"Blue 500G",
"Blue 1KG",
"Green 100G",
"Green 500G",
"Green 1KG"
];
quantity.placeholder="Enter Quantity in Boxes";
}

variety.innerHTML="";

options.forEach(function(item){
let opt=document.createElement("option");
opt.value=item;
opt.text=item;
variety.appendChild(opt);
});

variety.onchange=function(){
if(this.value==="Custom"){
custom.style.display="block";
}else{
custom.style.display="none";
}
}
}

function sendWhatsApp(){

let party=document.getElementById("partyName").value.trim();
let phone=document.getElementById("phoneNumber").value.trim();

if(party===""){
alert("Please enter Party Name");
return;
}

if(phone===""){
alert("Please enter Phone Number");
return;
}

let message=
`*RAJESHWAR PLASTIC ORDER*%0A%0A`;

message+=`*Party Name:* ${party}%0A`;
message+=`*Phone:* ${phone}%0A%0A`;

let rows=document.querySelectorAll(".order-row");

rows.forEach((row,index)=>{

let product=row.querySelector(".product").value;
let variety=row.querySelector(".variety").value;
let custom=row.querySelector(".customVariety").value;
let quantity=row.querySelector(".quantity").value;

if(variety==="Custom" && custom!==""){
variety=custom;
}

if(product!=="" && quantity!==""){
message+=`${index+1}. ${product} - ${variety} - ${quantity}%0A`;
}
});

window.open(
`https://wa.me/${whatsappNumber}?text=${message}`,
'_blank'
);

}

addOrder();

</script>

</body>
</html>
