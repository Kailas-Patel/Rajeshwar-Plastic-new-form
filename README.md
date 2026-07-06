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
<select class="product" onchange="updateFields(this)">
<option value="">Select Product</option>

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

<label id="typeLabel">Size / Type</label>

<select class="typeField">
<option>Select Product First</option>
</select>

<input
type="text"
class="customSize"
placeholder="Enter Size"
style="display:none;">

<label>Quantity</label>

<input
type="text"
class="quantity"
placeholder="Enter Quantity">

`;

document.getElementById("orders").appendChild(div);
}

function updateFields(productSelect){

let row=productSelect.parentElement;

let type=row.querySelector(".typeField");

let custom=row.querySelector(".customSize");

let quantity=row.querySelector(".quantity");

custom.style.display="none";

type.innerHTML="";

let product=productSelect.value;

let list=[];

if(product=="LD Bag" || product=="PP Bag" || product=="HM Bag"){

list=["Enter Manually"];

custom.style.display="block";

quantity.placeholder="Quantity in KG";

}

else if(product=="Corrugated Roll"){

list=["24","36","40"];

quantity.placeholder="Quantity in Rolls";

}

else if(product=="Sutli"){

list=["Neha","Dolphin","Packer"];

quantity.placeholder="Quantity in KG";

}

else if(product=="Patti"){

list=["2 KG Patti","10 KG Patti"];

quantity.placeholder="Quantity in Bundles";

}

else if(product=="Clip"){

list=["Standard"];

quantity.placeholder="Quantity in KG";

}

else if(product=="Marker"){

list=["Red","Blue","Black"];

quantity.placeholder="Quantity in Pieces / Boxes";

}

else if(product=="Color"){

list=[

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

quantity.placeholder="Quantity in Boxes";

}

list.forEach(function(item){

let op=document.createElement("option");

op.text=item;

op.value=item;

type.appendChild(op);

});

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

let type=row.querySelector(".typeField").value;

let custom=row.querySelector(".customSize").value;

if(custom!=""){
type=custom;
}

if(product!=="" && quantity!==""){
message+=`${index+1}. ${product} - ${type} - ${quantity}%0A`;
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
