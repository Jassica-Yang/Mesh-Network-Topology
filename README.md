# 📶 Real-Time Uplink / Downlink Speed Graph Demo

這是一個用 Chart.js 製作的網頁 Demo，用來模擬即時上/下載速度圖表。主要用於展示 router UI 中的 uplink/downlink 變化情境，可用於前端開發、UI 原型展示、或簡報 demo。

👉 **Live Demo 網址：**  
[https://uplink-downlink-graph.netlify.app/](https://uplink-downlink-graph.netlify.app/)

---

## 🚀 功能特色

- 模擬 **Uplink**（0 ~ 3 Mbps） 與 **Downlink**（5 ~ 35 Mbps）速度
- 每 **3 秒自動更新** 一筆資料
- 資料隨時間向左滾動，最多顯示 30 筆
- 使用 [Chart.js](https://www.chartjs.org/) 畫折線圖
- 無需後端、純前端、可直接部署在 Netlify 或 GitHub Pages

---

## 🧠 程式邏輯說明（模擬即時網速圖）

以下是 `index.html` 的 JavaScript 程式邏輯摘要與註解：

```js
// 取得 canvas 的繪圖上下文
const ctx = document.getElementById('speedChart').getContext('2d');

// 初始化三個陣列：標籤（時間）、上傳速度、下載速度
const labels = [];
const uplinkData = [];
const downlinkData = [];

// 建立 Chart.js 的線圖 (line chart)
const chart = new Chart(ctx, {
  type: 'line',
  data: {
    labels: labels, // 時間軸上的每一個點（例如 10:22:01）
    datasets: [
      {
        label: 'Uplink (Mbps)',        // 上行速度
        data: uplinkData,              // 對應資料陣列
        borderColor: 'orange',         // 線條顏色
        tension: 0.3                   // 曲線平滑程度
      },
      {
        label: 'Downlink (Mbps)',      // 下行速度
        data: downlinkData,
        borderColor: 'blue',
        tension: 0.3
      }
    ]
  },
  options: {
    animation: false, // 禁用動畫（即時圖表更新更順）
    responsive: true,
    scales: {
      y: {
        beginAtZero: true,
        title: { display: true, text: 'Speed (Mbps)' } // Y 軸標題
      },
      x: {
        title: { display: true, text: 'Time' } // X 軸標題
      }
    }
  }
});

// 模擬速度資料的函式，每次呼叫會新增一個數據點
function simulateSpeed() {
  const now = new Date().toLocaleTimeString(); // 當下時間字串

  // 最多只保留 30 筆資料，超過就移除最前面的（往左滑）
  if (labels.length > 30) {
    labels.shift();
    uplinkData.shift();
    downlinkData.shift();
  }

  labels.push(now);                                  // 時間點
  uplinkData.push((Math.random() * 3).toFixed(2));   // 上行速度模擬：0 ~ 3 Mbps
  downlinkData.push((Math.random() * 30 + 5).toFixed(2)); // 下行速度模擬：5 ~ 35 Mbps

  chart.update(); // 重新繪製圖表
}

// 設定每 3 秒呼叫一次 simulateSpeed()
setInterval(simulateSpeed, 3000);
