# ict-flashcard<!DOCTYPE html>
<html lang="zh-HK">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ICT 考試概念溫習卡片 (Postcard Mode)</title>
  <style>
    :root {
      --bg-color: #f4f6f9;
      --card-bg: #ffffff;
      --primary: #0056b3;
      --primary-hover: #004085;
      --text-main: #1f2937;
      --text-sub: #4b5563;
      --border: #e5e7eb;
      --accent-yellow: #fffbe6;
      --accent-border: #ffe58f;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      padding: 20px 15px;
    }

    .container {
      width: 100%;
      max-width: 680px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    header {
      text-align: center;
      margin-bottom: 8px;
    }

    header h1 {
      font-size: 1.5rem;
      color: var(--primary);
      margin-bottom: 4px;
    }

    header p {
      font-size: 0.9rem;
      color: var(--text-sub);
    }

    /* 進度與控制列 */
    .controls {
      background: var(--card-bg);
      padding: 12px 16px;
      border-radius: 12px;
      border: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 4px rgba(0,0,0,0.02);
    }

    .progress-text {
      font-weight: 600;
      font-size: 0.95rem;
    }

    .btn-action {
      background-color: #f3f4f6;
      border: 1px solid #d1d5db;
      padding: 6px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.85rem;
      transition: all 0.2s;
    }

    .btn-action:hover {
      background-color: #e5e7eb;
    }

    /* 溫習卡片主體 (Postcard) */
    .card-container {
      perspective: 1000px;
      width: 100%;
      min-height: 380px;
    }

    .card {
      width: 100%;
      min-height: 380px;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
      cursor: pointer;
    }

    .card.flipped {
      transform: rotateY(180deg);
    }

    .card-face {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      border-radius: 16px;
      background: var(--card-bg);
      border: 1px solid var(--border);
      box-shadow: 0 4px 12px rgba(0,0,0,0.05);
      padding: 24px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      box-sizing: border-box;
    }

    /* 正面樣式 */
    .card-front {
      background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
    }

    .card-tag {
      align-self: flex-start;
      background-color: #e0f2fe;
      color: #0369a1;
      padding: 4px 10px;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 600;
    }

    .concept-title {
      font-size: 1.8rem;
      font-weight: 700;
      text-align: center;
      color: #0f172a;
      margin: auto 0;
      line-height: 1.4;
    }

    .flip-hint {
      text-align: center;
      font-size: 0.85rem;
      color: #94a3b8;
    }

    /* 背面樣式 */
    .card-back {
      transform: rotateY(180deg);
      background-color: #ffffff;
      overflow-y: auto;
    }

    .section-title {
      font-size: 0.85rem;
      font-weight: 700;
      color: var(--primary);
      margin-top: 10px;
      margin-bottom: 4px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .def-box {
      font-size: 0.95rem;
      line-height: 1.5;
      color: #334155;
      background-color: #f8fafc;
      padding: 10px 12px;
      border-radius: 8px;
      margin-bottom: 8px;
    }

    .meta-box {
      background-color: var(--accent-yellow);
      border: 1px solid var(--accent-border);
      padding: 8px 12px;
      border-radius: 8px;
      font-size: 0.85rem;
      color: #78350f;
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
    }

    /* 底部操作按鈕 */
    .feedback-actions {
      display: flex;
      gap: 8px;
      margin-top: 10px;
    }

    .btn-status {
      flex: 1;
      padding: 10px 0;
      border: none;
      border-radius: 8px;
      font-weight: 600;
      font-size: 0.85rem;
      cursor: pointer;
      transition: opacity 0.2s;
    }

    .btn-status:hover {
      opacity: 0.85;
    }

    .btn-red { background-color: #fee2e2; color: #991b1b; }
    .btn-yellow { background-color: #fef3c7; color: #92400e; }
    .btn-green { background-color: #dcfce7; color: #166534; }
  </style>
</head>
<body>

<div class="container">
  <header>
    <h1>ICT 概念溫習 Postcard</h1>
    <p>點擊卡片查看詳細中英文定義與考試考點</p>
  </header>

  <div class="controls">
    <div class="progress-text" id="progressText">卡片 1 / 8</div>
    <button class="btn-action" onclick="shuffleCards()">🎲 隨機排序</button>
  </div>

  <div class="card-container">
    <div class="card" id="flashcard" onclick="flipCard()">
      <!-- 卡片正面 -->
      <div class="card-face card-front">
        <div class="card-tag" id="cardModule">A1_資訊處理</div>
        <div class="concept-title" id="cardConceptName">數據有效性檢驗<br><span style="font-size: 1.2rem; color: #64748b;">data validation</span></div>
        <div class="flip-hint">🔄 點擊卡片翻看完整定義與考點</div>
      </div>

      <!-- 卡片背面 -->
      <div class="card-face card-back">
        <div>
          <div class="section-title">中文定義</div>
          <div class="def-box" id="cardZhDef">數據有效性檢驗用規則檢查輸入數據是否合理及符合指定要求。</div>

          <div class="section-title">English Definition</div>
          <div class="def-box" id="cardEnDef">Data validation uses rules to check whether input data is reasonable and meets specified requirements.</div>

          <div class="meta-box">
            <div>📍 <strong>主要講解：</strong><span id="cardPageMain">P.33-34</span></div>
            <div>🔹 <strong>首次出現：</strong><span id="cardPageFirst">P.33</span></div>
          </div>
        </div>

        <div class="flip-hint" style="margin-top: 10px;">點擊下方按鈕切換下一張卡片</div>
      </div>
    </div>
  </div>

  <!-- 反饋控制按鈕 -->
  <div class="feedback-actions">
    <button class="btn-status btn-red" onclick="nextCard('unlearned')">🔴 未掌握</button>
    <button class="btn-status btn-yellow" onclick="nextCard('review')">🟡 需複習</button>
    <button class="btn-status btn-green" onclick="nextCard('mastered')">🟢 已掌握</button>
  </div>
</div>

<script>
  // 核心 ICT 概念資料集（無翻譯對譯功能）
  const dataset = [
    {
      module: "A1_資訊處理",
      conceptZh: "數據有效性檢驗",
      conceptEn: "data validation",
      zhDef: "數據有效性檢驗用規則檢查輸入數據是否合理及符合指定要求。[cite: 7, 8]",
      enDef: "Data validation uses rules to check whether input data is reasonable and meets specified requirements.[cite: 7, 8]",
      pageMain: "P.33-34",
      pageFirst: "P.33"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "奇偶檢測",
      conceptEn: "parity check",
      zhDef: "在二進制代碼的末尾附加一個奇偶檢驗位，以確保代碼中 1 的總數是偶數或奇數；這方法通常用於數據傳輸過程。[cite: 4]",
      enDef: "A parity bit is appended to the end of binary code to ensure that the total number of 1s is even or odd; this method is commonly used during data transmission.[cite: 4]",
      pageMain: "P.39",
      pageFirst: "P.39"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "數據庫管理系統",
      conceptEn: "database management system (DBMS)",
      zhDef: "數據庫管理系統用來管理數據庫，讓用戶組織、儲存、修改及提取數據。[cite: 9, 10]",
      enDef: "A database management system is used to manage a database, allowing users to organise, store, modify, and retrieve data.[cite: 9, 10]",
      pageMain: "P.31",
      pageFirst: "P.31"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "結構化查詢語言",
      conceptEn: "Structured Query Language (SQL)",
      zhDef: "書本指出，可使用結構化查詢語言 (SQL) 在數據庫中插入新記錄、更改或刪除現有記錄。[cite: 3]",
      enDef: "The book states that Structured Query Language (SQL) can be used to insert new records into a database and modify or delete existing records.[cite: 3]",
      pageMain: "P.45",
      pageFirst: "P.44"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "檢查數位",
      conceptEn: "check digit",
      zhDef: "檢查數位由特定算法生成，並附加到數據的結尾；如果數據的檢查數位與算法生成的檢查數位不匹配，該數據便無效。[cite: 4, 5]",
      enDef: "A check digit is generated by a specific algorithm and appended to the end of data; if the check digit in the data does not match the one generated by the algorithm, the data is invalid.[cite: 4, 5]",
      pageMain: "P.37",
      pageFirst: "P.37"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "圖形用戶界面",
      conceptEn: "graphical user interface (GUI)",
      zhDef: "用戶可使用圖形用戶界面（GUI）在數據庫中插入新記錄、更改或刪除現有記錄。[cite: 8, 9]",
      enDef: "Users can use a graphical user interface (GUI) to insert new records into a database and modify or delete existing records.[cite: 8, 9]",
      pageMain: "P.53",
      pageFirst: "P.31"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "無用輸入，無用輸出",
      conceptEn: "garbage in, garbage out (GIGO)",
      zhDef: "指出如果輸入的數據不正確，即使處理程序正確，輸出的結果亦會不可靠。[cite: 7, 8]",
      enDef: "Garbage in, garbage out (GIGO) means that if the input data is incorrect, the output will also be unreliable even when the processing is correct.[cite: 7, 8]",
      pageMain: "P.33",
      pageFirst: "P.33"
    },
    {
      module: "A1_資訊處理",
      conceptZh: "索引",
      conceptEn: "index",
      zhDef: "可以為經常被搜尋的欄位建立索引，以加快數據提取。[cite: 3]",
      enDef: "An index can be created for a frequently searched field to speed up data retrieval.[cite: 3]",
      pageMain: "P.46",
      pageFirst: "P.46"
    }
  ];

  let currentIndex = 0;
  let isFlipped = false;

  const cardElement = document.getElementById('flashcard');

  function renderCard() {
    const data = dataset[currentIndex];
    document.getElementById('progressText').innerText = `卡片 ${currentIndex + 1} / ${dataset.length}`;
    document.getElementById('cardModule').innerText = data.module;
    document.getElementById('cardConceptName').innerHTML = `${data.conceptZh}<br><span style="font-size: 1.2rem; color: #64748b; font-weight: normal;">${data.conceptEn}</span>`;
    document.getElementById('cardZhDef').innerText = data.zhDef;
    document.getElementById('cardEnDef').innerText = data.enDef;
    document.getElementById('cardPageMain').innerText = data.pageMain;
    document.getElementById('cardPageFirst').innerText = data.pageFirst;
  }

  function flipCard() {
    isFlipped = !isFlipped;
    if (isFlipped) {
      cardElement.classList.add('flipped');
    } else {
      cardElement.classList.remove('flipped');
    }
  }

  function nextCard(status) {
    if (isFlipped) {
      cardElement.classList.remove('flipped');
      isFlipped = false;
      setTimeout(() => {
        switchCardIndex();
      }, 300);
    } else {
      switchCardIndex();
    }
  }

  function switchCardIndex() {
    currentIndex = (currentIndex + 1) % dataset.length;
    renderCard();
  }

  function shuffleCards() {
    dataset.sort(() => Math.random() - 0.5);
    currentIndex = 0;
    if (isFlipped) {
      cardElement.classList.remove('flipped');
      isFlipped = false;
      setTimeout(renderCard, 300);
    } else {
      renderCard();
    }
  }

  // 初始化載入第一張卡片
  renderCard();
</script>

</body>
</html>