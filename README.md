# form-kerusakan-irigasi

<html>
<head>
  <title>Form Kerusakan Irigasi</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <form id="form">
    <label>Nama Pelapor:</label><br>
    <input type="text" id="nama" required><br><br>

    <label>Nama Saluran:</label><br>
    <input type="text" id="saluran" required><br><br>

    <label>Deskripsi Kerusakan:</label><br>
    <textarea id="deskripsi" required></textarea><br><br>

    <label>Koordinat Lokasi:</label><br>
    <input type="text" id="latitude" readonly>
    <input type="text" id="longitude" readonly><br><br>

    <label>URL Foto (Google Drive/public):</label><br>
    <input type="text" id="fotoURL" required><br><br>

    <button type="submit">Kirim</button>
  </form>

  <p id="status"></p>

  <script>
    // Ambil lokasi otomatis
    navigator.geolocation.getCurrentPosition(function(pos) {
      document.getElementById("latitude").value = pos.coords.latitude.toFixed(6).toString().replace(/\./g, "#").replace(/#(?=\d{3}(\D|$))/g, "").replace(/#/g, ".");
     document.getElementById("longitude").value = pos.coords.longitude.toFixed(6).toString().replace(/\./g, "#").replace(/#(?=\d{3}(\D|$))/g, "").replace(/#/g, ".");
    });

    // Submit form
    document.getElementById("form").addEventListener("submit", function(e) {
      e.preventDefault();

      const data = {
  nama: document.getElementById("nama").value,
  saluran: document.getElementById("saluran").value,
  deskripsi: document.getElementById("deskripsi").value,
  latitude: document.getElementById("latitude").value,
  longitude: document.getElementById("longitude").value,
  fotoURL: document.getElementById("fotoURL").value
};

      fetch('https://script.google.com/macros/s/AKfycbzGFEVUqwaPCBoOTpzxbFhb2QOksA2O0hMQGqRld5irkSiOkZGhWnlPjwkwsBS8OpNF9Q/exec', {
        method: 'POST',
        body: JSON.stringify(data)
      })
      .then(res => res.text())
      .then(msg => document.getElementById("status").innerText = msg);
    });
  </script>
</body>
</html>
