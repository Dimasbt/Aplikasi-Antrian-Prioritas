# Aplikasi-Antrian-Prioritas
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Antrean Rumah Sakit</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f4f6f9;
    padding:20px;
}

.container{
    max-width:800px;
    margin:auto;
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 0 10px rgba(0,0,0,0.1);
}

h1{
    text-align:center;
    color:#2c3e50;
}

input, select, button{
    width:100%;
    padding:10px;
    margin-top:10px;
}

button{
    background:#3498db;
    color:white;
    border:none;
    cursor:pointer;
}

button:hover{
    background:#2980b9;
}

table{
    width:100%;
    border-collapse:collapse;
    margin-top:20px;
}

th, td{
    border:1px solid #ddd;
    padding:10px;
    text-align:center;
}

th{
    background:#3498db;
    color:white;
}

.next{
    margin-top:20px;
    padding:15px;
    background:#e8f5e9;
    border-left:5px solid green;
}
</style>
</head>
<body>

<div class="container">

<h1>Sistem Antrean Rumah Sakit</h1>

<input type="text" id="nama" placeholder="Nama Pasien">

<select id="kategori">
    <option value="4">Umum</option>
    <option value="3">Anak</option>
    <option value="2">Lansia</option>
    <option value="1">Gawat Darurat</option>
</select>

<button onclick="tambahPasien()">Tambah Antrean</button>

<button onclick="panggilPasien()">Panggil Pasien Berikutnya</button>

<div class="next" id="pasienBerikutnya">
    Belum ada pasien dipanggil.
</div>

<table>
<thead>
<tr>
    <th>No Antrean</th>
    <th>Nama</th>
    <th>Kategori</th>
</tr>
</thead>
<tbody id="daftarAntrean">
</tbody>
</table>

</div>

<script>

let antrean = [];
let nomor = 1;

function kategoriText(prioritas){
    switch(prioritas){
        case 1: return "Gawat Darurat";
        case 2: return "Lansia";
        case 3: return "Anak";
        default: return "Umum";
    }
}

function tambahPasien(){

    let nama = document.getElementById("nama").value;
    let prioritas = parseInt(document.getElementById("kategori").value);

    if(nama === ""){
        alert("Masukkan nama pasien");
        return;
    }

    antrean.push({
        nomor: nomor++,
        nama: nama,
        prioritas: prioritas
    });

    antrean.sort((a,b)=>a.prioritas-b.prioritas);

    tampilkanAntrean();

    document.getElementById("nama").value="";
}

function tampilkanAntrean(){

    let tbody = document.getElementById("daftarAntrean");
    tbody.innerHTML="";

    antrean.forEach(pasien=>{
        tbody.innerHTML += `
        <tr>
            <td>${pasien.nomor}</td>
            <td>${pasien.nama}</td>
            <td>${kategoriText(pasien.prioritas)}</td>
        </tr>
        `;
    });
}

function panggilPasien(){

    if(antrean.length===0){
        alert("Tidak ada antrean");
        return;
    }

    let pasien = antrean.shift();

    document.getElementById("pasienBerikutnya").innerHTML =
        `<strong>Dipanggil:</strong><br>
        No. ${pasien.nomor} - ${pasien.nama}<br>
        (${kategoriText(pasien.prioritas)})`;

    tampilkanAntrean();
}

</script>

</body>
</html>
