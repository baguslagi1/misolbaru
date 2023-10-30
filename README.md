<html>
  <head>
    <title>Ngemis Online</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
      body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #3498db;
        flex-direction: column;
      }

      .container {
        max-width: 600px;
        padding: 20px;
        background-color: #fff;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        text-align: center;
      }

      h1 {
        display: none;
      }

      p {
        margin: 10px 0;
      }

      button {
        display: inline-block;
        margin: 0 10px;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        background-color: #e74c3c;
        color: #fff;
      }

      #result {
        margin-top: 20px;
        text-align: center;
        font-weight: bold;
        color: #333;
      }

      #qris {
        display: none;
      }

      .qris-image {
        max-width: 300px;
      }

      #intro-text {
        display: block;
        font-weight: bold;
        color: #333;
      }

      /* Media query untuk perangkat seluler */
      @media (max-width: 768px) {
        .container {
          max-width: 90%;
        }

        button {
          padding: 5% 10%;
        }

        .qris-image {
          max-width: 100%;
        }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h1>MISOL</h1>
      <p id="intro-text">Ngemis Online :v</p>
      <button id="start" onclick="startTest()">Next</button>
      <h1>Tes Introvert atau Ekstrovert</h1>
      <div id="question-container" style="display: none">
        <p id="question">
          APAKAH ANDA MERASA LEBIH ENERGIK SAAT BERINTERAKSI DENGAN BANYAK ORANG
          (ya) atau saat anda sendiri atau bersama teman-teman dekat (tidak)?
        </p>
        <button id="yes" onclick="nextQuestion('ya')">YA</button>
        <button id="no" onclick="nextQuestion('tidak')">TIDAK</button>
      </div>
      <div id="result" style="display: none">
        <span id="result-text"></span>
        <br />
        <p id="result-description"></p>
        <button id="next" onclick="showQRIS()">Next</button>
      </div>
      <div id="qris">
        <img class="qris-image" src="qris.jpeg" alt="QRIS" />
      </div>
    </div>

    <script>
      let testStarted = false;

      function startTest() {
        document.getElementById("start").style.display = "none";
        document.getElementById("question-container").style.display = "block";
        testStarted = true;
      }

      const questions = [
        "APAKAH ANDA MERASA LEBIH ENERGIK SAAT BERINTERAKSI DENGAN BANYAK ORANG (ya) atau saat anda sendiri atau bersama teman-teman dekat (tidak)?",
        "APAKAH ANDA MERASA BERSEMANGAT SETELAH MENGHADIRI PESTA BESAR ATAU ACARA SOSIAL (ya) atau merasa perlu waktu untuk merenung dan merasakan energi kembali (tidak)?",
        "APAKAH ANDA CENDERUNG BERBICARA DENGAN ORANG YANG BARU ANDA TEMUI (ya) atau lebih selektif dalam memilih dengan siapa anda berbicara (tidak)?",
        "APAKAH ANDA SERING MENCARI KEGIATAN SOSIAL DAN BERKUMPUL DENGAN BANYAK ORANG (ya) atau lebih suka kegiatan yang lebih tenang dan individual (tidak)?",
        "APAKAH ANDA MERASA LEBIH BERSEMANGAT KETIKA BERADA DALAM SITUASI YANG MEMUNGKINKAN ANDA UNTUK BERBICARA DAN BERINTERAKSI DENGAN BANYAK ORANG (ya) atau ketika anda dapat berpikir dan merenung (tidak)?",
        "APAKAH ANDA SERING MENCARI KESEMPATAN UNTUK BERPARTISIPASI DALAM AKTIVITAS SOSIAL DAN MENCARI BANYAK TEMAN (ya) atau lebih suka memiliki sedikit teman dekat (tidak)?",
        "APAKAH ANDA MERASA NYAMAN SAAT HARUS BERBICARA DI DEPAN BANYAK ORANG (ya) atau merasa cemas dan lebih memilih menghindari situasi tersebut (tidak)?",
        "BAGAIMANA ANDA MERESPON KETIKA ANDA MERASA STRES? APAKAH ANDA CENDERUNG BERBICARA DENGAN TEMAN-TEMAN UNTUK MENCARI DUKUNGAN (ya) atau tetap tenang dan mencoba menemukan solusi (tidak)?",
        "APAKAH ANDA CENDERUNG MENGAMBIL INISIATIF DALAM MEMULAI PERCAKAPAN DENGAN ORANG BARU (ya) atau lebih pasif dalam hal itu (tidak)?",
        "BAGAIMANA ANDA MERASA SAAT BERADA DALAM KERUMUNAN ORANG YANG BESAR? APAKAH ANDA MERASA BERSEMANGAT DAN ANTUSIAS? (ya) atau cenderung merasa terlalu terpapar dan ingin keluar (tidak)?",
      ];
      const answers = [];

      let currentQuestion = 1;

      function nextQuestion(answer) {
        answers.push(answer);
        currentQuestion++;

        if (currentQuestion <= questions.length) {
          document.getElementById("question").innerText =
            questions[currentQuestion - 1];
          document.body.style.backgroundColor = getRandomColor();
        } else {
          showResult();
        }
      }

      function showResult() {
        const countYes = answers.filter((answer) => answer === "ya").length;
        const countNo = answers.length - countYes;
        let result = "";

        if (countYes > countNo) {
          result = "Anda adalah seorang ekstrovert!";
          document.getElementById("result-description").innerText =
            "Sebagai seorang ekstrovert, Anda mungkin lebih suka terlibat dalam aksi langsung. Kontribusi Anda ke QRIS saya adalah langkah konkret dalam mendukung apa yang Anda pedulikan. Awokwok :v";
        } else if (countNo > countYes) {
          result = "Anda adalah seorang introvert!";
          document.getElementById("result-description").innerText =
            "Orang introvert seringkali memiliki jaringan sosial yang lebih kecil, tetapi kontribusi Anda ke QRIS saya bisa memiliki dampak besar. Awokwok :v";
        } else {
          result = "Anda adalah seorang ambivert";
          document.getElementById("result-description").innerText =
            "Anda mungkin merasa nyaman dalam interaksi sosial sekaligus menikmati waktu untuk merenung. Dengan berpartisipasi dalam QRIS saya, Anda bisa merasakan keduanya. Awokwok :v";
        }

        document.getElementById("question-container").style.display = "none";
        document.getElementById("result").style.display = "block";
        document.getElementById("result-text").innerText = result;
      }

      function showQRIS() {
        document.getElementById("result").style.display = "none";
        document.getElementById("qris").style.display = "block";
      }

      function getRandomColor() {
        const letters = "0123456789ABCDEF";
        let color = "#";
        for (let i = 0; i < 6; i++) {
          color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
      }
    </script>
  </body>
</html>
