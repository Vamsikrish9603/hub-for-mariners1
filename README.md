<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Marine Engineers Hub</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #eef;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    header, footer {
      background-color: #003366;
      color: white;
      padding: 20px;
    }
    .container {
      padding: 20px;
    }
    .subjects button {
      margin: 5px;
      padding: 10px 15px;
      background: #0066cc;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .subjects button:hover {
      background-color: #004d99;
    }
    input, select {
      padding: 8px;
      margin: 8px 0;
      width: 100%;
    }
    .section {
      background: white;
      margin: 20px 0;
      padding: 20px;
      border-radius: 8px;
    }
    .pdf-item {
      margin: 10px 0;
      padding: 10px;
      border-bottom: 1px solid #ccc;
    }
    .pdf-item a {
      margin-right: 10px;
    }
    iframe {
      width: 100%;
      height: 500px;
      border: none;
      margin-top: 20px;
      display: none;
    }
  </style>
</head>
<body>

<header>
  <h1>Welcome to Marine Engineers Hub</h1>
  <p>by Vamsi Krishna Koraganji | Email: vamsikrishnakoraganji96@gmail.com</p>
</header>

<div class="container">

  <div class="section subjects">
    <h2>Subject Categories</h2>
    <button onclick="showDrive('Thermodynamics')">Thermodynamics</button>
    <button onclick="showDrive('Marine Engines')">Marine Engines</button>
    <button onclick="showDrive('Naval Architecture')">Naval Architecture</button>
    <button onclick="showDrive('Fluid Mechanics')">Fluid Mechanics</button>
    <button onclick="showDrive('Marine Electrical Technology')">Marine Electrical Tech</button>
  </div>

  <div class="section">
    <h2>Upload PDF (Simulated)</h2>
    <form id="uploadForm">
      <input type="text" id="pdfTitle" placeholder="PDF Title" required />
      <select id="pdfSubject" required>
        <option value="">Select Subject</option>
        <option value="Thermodynamics">Thermodynamics</option>
        <option value="Marine Engines">Marine Engines</option>
        <option value="Naval Architecture">Naval Architecture</option>
        <option value="Fluid Mechanics">Fluid Mechanics</option>
        <option value="Marine Electrical Technology">Marine Electrical Technology</option>
      </select>
      <input type="file" id="pdfFile" accept="application/pdf" required />
      <button type="submit">Simulate Upload</button>
    </form>
  </div>

  <div class="section">
    <h2>Uploaded PDFs (Local Simulation)</h2>
    <div id="pdfContainer">
      <p>No PDFs uploaded yet.</p>
    </div>
  </div>

  <iframe id="pdfFrame"></iframe>

</div>

<footer>
  <p>Storage access via Google Drive | Contact: marinehubforengineers@gmail.com</p>
</footer>

<script>
  const driveLinks = {
    "Thermodynamics": "https://drive.google.com/drive/u/2/folders/1aIMYdPTgCbAbKjppX0bKCj6bErTN9_nw",
    "Fluid Mechanics": "https://drive.google.com/drive/u/2/folders/1aIMYdPTgCbAbKjppX0bKCj6bErTN9_nw",
    "Marine Engines": "https://drive.google.com/drive/u/2/folders/1ZFBVyREADZR919bLYINWT9RfXm-0DCFa",
    "Naval Architecture": "https://drive.google.com/drive/u/2/folders/15CIEGvMw1jCidhvjxfBEGQ_xua4n_5kZ",
    "Marine Electrical Technology": "https://drive.google.com/drive/u/2/folders/1Pqt5IYFM1Q0gRv4bgOW77QT8gDBofizi"
  };

  const uploadedPDFs = [];

  document.getElementById('uploadForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const title = document.getElementById('pdfTitle').value;
    const subject = document.getElementById('pdfSubject').value;
    const file = document.getElementById('pdfFile').files[0];

    if (title && subject && file) {
      const url = URL.createObjectURL(file); // local preview URL
      uploadedPDFs.push({ title, subject, url });
      updatePDFList();
      alert("PDF simulated as uploaded! Please manually upload it to your subject's Drive folder.");
      this.reset();
    }
  });

  function updatePDFList() {
    const container = document.getElementById('pdfContainer');
    if (uploadedPDFs.length === 0) {
      container.innerHTML = `<p>No PDFs uploaded yet.</p>`;
      return;
    }
    container.innerHTML = '';
    uploadedPDFs.forEach(pdf => {
      container.innerHTML += `
        <div class="pdf-item">
          <strong>${pdf.title}</strong> (${pdf.subject})<br/>
          <a href="${pdf.url}" target="_blank">View</a>
          <a href="${pdf.url}" download>Download</a>
        </div>
      `;
    });
  }

  function showDrive(subject) {
    const frame = document.getElementById('pdfFrame');
    if (driveLinks[subject]) {
      frame.src = driveLinks[subject];
      frame.style.display = "block";
    } else {
      frame.style.display = "none";
    }
  }
</script>

</body>
</html>
