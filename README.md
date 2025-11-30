<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>বাংলাদেশ  ভোট সার্ভে</title>
  <style>
    body{font-family:Arial;background:#f2f2f2;padding:20px}
    .box{max-width:320px;margin:auto;background:#fff;padding:20px;border-radius:8px;
         box-shadow:0 2px 6px rgba(0,0,0,.1)}
    input,select,button{width:100%;padding:10px;margin-top:10px;font-size:1rem}
    button{background:#1976d2;color:#fff;border:none;border-radius:4px;cursor:pointer}
    p{text-align:center;margin-top:10px;font-weight:bold}
  </style>
</head>
<body>

<div class="box">
  <h2 style="text-align:center">ভোট সার্ভে</h2>

  <input id="name" placeholder="নাম" required>
  <input id="roll" placeholder="nid" required type="number" min="1" step="1">

  <select id="food">
    <option value="">পছন্দের দল নির্বাচন করুন</option>
    <option>BNP</option>
    <option>JAMAT</option>
    <option>ncb</option>
    <option>lig</option>
  </select>

  <button id="submitBtn">সাবমিট</button>
  <p id="status"></p>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
  import { getDatabase, ref, push } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyDk-flURRVAoDAw91F2rmUgutqyKcW9opc",
    authDomain: "votbangla.firebaseapp.com",
    databaseURL: "https://votbangla-default-rtdb.asia-southeast1.firebasedatabase.app",
    projectId: "votbangla",
    storageBucket: "votbangla.appspot.com", // এখানে ঠিক করা হয়েছে
    messagingSenderId: "36894884700",
    appId: "1:36894884700:web:a981979e3b271dd7847799"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  const $ = id => document.getElementById(id);

  $("submitBtn").onclick = async () => {
    const name = $("name").value.trim();
    const roll = $("roll").value.trim();
    const food = $("food").value;

    // রোল (NID) কেবল সংখ্যাবাচক এবং ১ বা তার বেশি কিনা চেক করা হয়েছে
    if (!name || !roll || !food || isNaN(roll) || Number(roll) < 1) {
      $("status").textContent = "সব ঘর সঠিকভাবে পূরণ করুন";
      $("status").style.color = "red";
      return;
    }

    await push(ref(db, "classSurvey"), {
      name,
      roll,
      food,
      time: Date.now()
    });

    $("status").textContent = "সাবমিট সফল!";
    $("status").style.color = "green";

    $("name").value = "";
    $("roll").value = "";
    $("food").value = "";
  };
</script>
তথ্য ভুল দিবেন তো ধরা খাবেন
demo 
mdyoumdyousufyeamjohanmahim@gmail.com
</body>
</html>
