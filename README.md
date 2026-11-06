# Esg_travel_aiprompt
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>實戰課程專屬｜AI 指令庫</title>
  <style>
    :root {
      --bg: #F9F8F6;
      --card-bg: #FFFFFF;
      --text-main: #2D3748;
      --text-muted: #718096;
      --accent: #B08968;
      --accent-hover: #967259;
      --tag-bg: #EDE0D4;
      --tag-text: #7F5539;
      --border: #E8E3DF;
      --success: #38A169;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text-main);
      padding: 32px 16px;
      line-height: 1.6;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
    }

    /* 頂部標題 */
    header {
      text-align: center;
      margin-bottom: 32px;
    }

    header h1 {
      font-size: 26px;
      color: var(--text-main);
      margin-bottom: 8px;
    }

    header p {
      color: var(--text-muted);
      font-size: 15px;
    }

    /* 搜尋與篩選工具列 */
    .toolbar {
      display: flex;
      flex-direction: column;
      gap: 16px;
      margin-bottom: 28px;
    }

    .search-input {
      width: 100%;
      padding: 12px 16px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 15px;
      outline: none;
      background-color: var(--card-bg);
      transition: border-color 0.2s;
    }

    .search-input:focus {
      border-color: var(--accent);
    }

    .category-filter {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .filter-btn {
      padding: 6px 14px;
      border: 1px solid var(--border);
      border-radius: 20px;
      background: var(--card-bg);
      font-size: 14px;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .filter-btn:hover, .filter-btn.active {
      background: var(--accent);
      color: #fff;
      border-color: var(--accent);
    }

    /* 卡片清單 */
    .prompt-grid {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.03);
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
    }

    .card-title-group {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .card-title {
      font-size: 17px;
      font-weight: 600;
    }

    .card-tag {
      font-size: 12px;
      padding: 2px 8px;
      background-color: var(--tag-bg);
      color: var(--tag-text);
      border-radius: 4px;
    }

    .copy-btn {
      background-color: var(--accent);
      color: #fff;
      border: none;
      padding: 7px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      font-weight: 500;
      transition: background-color 0.2s;
      white-space: nowrap;
    }

    .copy-btn:hover {
      background-color: var(--accent-hover);
    }

    .copy-btn.copied {
      background-color: var(--success);
    }

    .card-desc {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 12px;
    }

    .prompt-box {
      background-color: #F8F9FA;
      border: 1px solid #ECECEC;
      border-radius: 6px;
      padding: 12px;
      font-family: monospace;
      font-size: 13.5px;
      color: #333;
      white-space: pre-wrap;
      word-break: break-all;
    }

    .empty-state {
      text-align: center;
      padding: 40px;
      color: var(--text-muted);
      display: none;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <h1>課程專屬｜AI 指令工具庫</h1>
      <p>點擊右上角「複製指令」按鈕，即可直接貼入 ChatGPT 或 Claude 使用。</p>
    </header>

    <div class="toolbar">
      <input type="text" id="searchInput" class="search-input" placeholder="🔍 搜尋指令關鍵字（如：客訴、簡報、文案）...">
      
      <div class="category-filter">
        <button class="filter-btn active" data-category="all">全部指令</button>
        <button class="filter-btn" data-category="顧客應對">顧客應對</button>
        <button class="filter-btn" data-category="文案推廣">文案推廣</button>
        <button class="filter-btn" data-category="日常行政">日常行政</button>
      </div>
    </div>

    <div class="prompt-grid" id="promptContainer">

      <!-- 示範卡片 1 -->
      <div class="card" data-category="顧客應對">
        <div class="card-header">
          <div class="card-title-group">
            <span class="card-title">處理顧客抱怨與安撫回覆</span>
            <span class="card-tag">顧客應對</span>
          </div>
          <button class="copy-btn" onclick="copyPrompt(this)">複製指令</button>
        </div>
        <div class="card-desc">適用情境：客人情緒激動或對服務流程有誤解時，產出同理心且具專業規範的文字。</div>
        <div class="prompt-box">請扮演專業親切的客服專家。請根據以下顧客反映的問題，撰寫一段回覆內容。

要求：
1. 先展現同理心，感謝對方的反映並致上歉意，不要直接推卸責任。
2. 清楚說明目前門市的處理方式與替代方案。
3. 語氣溫和堅定、展現誠意。

顧客反映內容：
[貼上顧客訊息]</div>
      </div>

      <!-- 示範卡片 2 -->
      <div class="card" data-category="文案推廣">
        <div class="card-header">
          <div class="card-title-group">
            <span class="card-title">活動推播與社群短文</span>
            <span class="card-tag">文案推廣</span>
          </div>
          <button class="copy-btn" onclick="copyPrompt(this)">複製指令</button>
        </div>
        <div class="card-desc">適用情境：門市新檔期優惠開跑，需要撰寫 LINE 群組或 FB 社群推播。</div>
        <div class="prompt-box">我想為門市活動撰寫一則簡短吸睛的社群推播訊息。

活動資訊：
- 活動主題：[例如：週末快閃購機專案]
- 核心亮點：[例如：指定機型現折千元、送原廠配件]
- 截止時間：[例如：本週日 22:00]

請輸出：
1. 吸睛的第 1 行標題（帶 Emoji）
2. 條列式優惠重點（不超過 3 點）
3. 明確的行動呼籲（CTA，引導到店或回傳確認）</div>
      </div>

      <!-- 示範卡片 3 -->
      <div class="card" data-category="日常行政">
        <div class="card-header">
          <div class="card-title-group">
            <span class="card-title">門市交接與晨會重點整理</span>
            <span class="card-tag">日常行政</span>
          </div>
          <button class="copy-btn" onclick="copyPrompt(this)">複製指令</button>
        </div>
        <div class="card-desc">適用情境：將零碎的交接記事快速整理為結構清晰的重點清單。</div>
        <div class="prompt-box">請將以下零碎的門市筆記整理為清楚的「交接與晨會通知」。

請分成三部分呈現：
1. 今日優先必辦事項（依緊急程度排序）
2. 待追蹤客件或未結案項目
3. 一般宣導與提醒

筆記內容：
[貼上零散文字]</div>
      </div>

      <div class="empty-state" id="emptyState">找不到符合的指令內容。</div>
    </div>
  </div>

  <script>
    // 一鍵複製功能
    function copyPrompt(button) {
      const card = button.closest('.card');
      const textToCopy = card.querySelector('.prompt-box').innerText;

      navigator.clipboard.writeText(textToCopy).then(() => {
        const originalText = button.innerText;
        button.innerText = '已複製 ✓';
        button.classList.add('copied');

        setTimeout(() => {
          button.innerText = originalText;
          button.classList.remove('copied');
        }, 1800);
      }).catch(err => {
        console.error('複製失敗:', err);
      });
    }

    // 搜尋與標籤篩選邏輯
    const searchInput = document.getElementById('searchInput');
    const filterBtns = document.querySelectorAll('.filter-btn');
    const cards = document.querySelectorAll('.card');
    const emptyState = document.getElementById('emptyState');

    let currentCategory = 'all';

    function filterCards() {
      const query = searchInput.value.toLowerCase().trim();
      let visibleCount = 0;

      cards.forEach(card => {
        const category = card.getAttribute('data-category');
        const text = card.innerText.toLowerCase();

        const matchesCategory = (currentCategory === 'all' || category === currentCategory);
        const matchesQuery = text.includes(query);

        if (matchesCategory && matchesQuery) {
          card.style.display = 'block';
          visibleCount++;
        } else {
          card.style.display = 'none';
        }
      });

      emptyState.style.display = visibleCount === 0 ? 'block' : 'none';
    }

    searchInput.addEventListener('input', filterCards);

    filterBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        filterBtns.forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        currentCategory = btn.getAttribute('data-category');
        filterCards();
      });
    });
  </script>
</body>
</html>
