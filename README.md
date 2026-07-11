# Accounting-Client-Tracking
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Accounting Client Dashboard</title>

<style>
body{
    font-family:Arial,sans-serif;
    background:#f4f6f9;
    margin:20px;
}

h1{
    color:#2c3e50;
}

.dashboard{
    display:flex;
    gap:20px;
    margin-bottom:20px;
}

.card{
    background:white;
    padding:15px;
    border-radius:10px;
    box-shadow:0 2px 8px rgba(0,0,0,.1);
    width:200px;
}

table{
    width:100%;
    border-collapse:collapse;
    background:white;
}

th,td{
    padding:12px;
    border-bottom:1px solid #ddd;
}

th{
    background:#34495e;
    color:white;
}

.overdue{
    color:red;
    font-weight:bold;
}

.paid{
    color:green;
}

button{
    padding:8px 15px;
    margin-bottom:10px;
}
</style>

</head>
<body>

<h1>Accounting Client Dashboard</h1>

<div class="dashboard">
<div class="card">
<h3>Total Clients</h3>
<h2 id="clients">0</h2>
</div>

<div class="card">
<h3>Outstanding</h3>
<h2 id="outstanding">$0</h2>
</div>

<div class="card">
<h3>Overdue</h3>
<h2 id="overdue">0</h2>
</div>
</div>

<table id="clientTable">
<thead>
<tr>
<th>Client</th>
<th>Service</th>
<th>Invoice</th>
<th>Amount</th>
<th>Due Date</th>
<th>Status</th>
</tr>
</thead>
<tbody></tbody>
</table>

<script>

const clients=[
{
name:"ABC Construction",
service:"Bookkeeping",
invoice:"INV-1001",
amount:1500,
due:"2026-07-15",
status:"Pending"
},
{
name:"Jones Law",
service:"Tax Return",
invoice:"INV-1002",
amount:900,
due:"2026-06-30",
status:"Overdue"
},
{
name:"Smith Dental",
service:"Payroll",
invoice:"INV-1003",
amount:750,
due:"2026-07-05",
status:"Paid"
}
];

const tbody=document.querySelector("tbody");

let outstanding=0;
let overdue=0;

clients.forEach(client=>{

const row=document.createElement("tr");

if(client.status!="Paid")
outstanding+=client.amount;

if(client.status=="Overdue")
overdue++;

row.innerHTML=`
<td>${client.name}</td>
<td>${client.service}</td>
<td>${client.invoice}</td>
<td>$${client.amount}</td>
<td>${client.due}</td>
<td class="${client.status=="Paid"?"paid":"overdue"}">${client.status}</td>
`;

tbody.appendChild(row);

});

document.getElementById("clients").innerText=clients.length;
document.getElementById("outstanding").innerText="$"+outstanding;
document.getElementById("overdue").innerText=overdue;

</script>

</body>
</html>
