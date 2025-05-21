# 📡 Mesh Network Topology Visualization (Demo)

這是一個使用 [vis-network](https://visjs.github.io/vis-network/) 製作的 Wi-Fi Mesh Network 拓撲圖示範頁面，可視覺化路由器與節點（Repeater / Client）之間的連線與上下游關係，並點擊節點查看詳細資訊。

---

## 🚀 Demo 網址

🔗 [https://uplink-downlink-graph.netlify.app/](https://uplink-downlink-graph.netlify.app/)  
（可自行部署）

---

## 🎯 功能特色

- 顯示 Wi-Fi Mesh 拓撲結構：節點之間的 **upstream/downstream** 連接關係
- 支援節點類型：
  - Router / Repeater
  - Client（如手機、電視盒、IoT 裝置）
- 點擊節點可展開顯示詳細資訊：
  - MAC / IP / Signal / Serial / Sync 狀態
- 圖示節點皆使用 `icons-wifi-router.png` 為背景圖
- 線段標示：
  - uplink 連線方向
  - client 所屬的 interface（如 2.4GHz / 5GHz / Ethernet）

---

## 📦 技術細節

- 使用 [vis-network](https://visjs.github.io/vis-network/) 建立拓撲圖
- 所有資料均來自內建 JSON 模擬資料，無需後端 API
- 網頁為純 HTML + JS，支援部署至 GitHub Pages / Netlify
- 節點自動判別名稱、連線狀態與資料顯示（來源：`wifi_re_list`, `wifi_re_paired_list`）

---

## 📁 專案結構

demo/uplink-downlink/
├── index.html # 拓撲圖主頁面（含 vis-network 視覺化）
├── image/icons-wifi-router.png # 節點 icon 圖片
├── README.md # 本文件

---

## 🧠 程式邏輯摘要（for 開發者）

- 解析兩組資料來源：
  - `wifi_re_paired_list`: Mesh 節點基本資料（MAC / name / serial）
  - `wifi_re_list`: 拓撲與上下游連線資訊（MAC / IP / signal / upstream / clients）
- 建立節點清單（nodes）與連線邊（edges）
- 將 AP / Client 分別接在對應節點下方
- 點擊節點時顯示 info panel（`#node-info`）

---

## 🛠️ 可擴充方向

- 從後端 API 實時讀取 `/cgi-bin/mesh_topology.cgi` 等資料
- 根據 signal 動態改變節點顏色 / 線條粗細
- 支援節點拖拉或自動物理佈局
- 加入節點在線 / 離線變化動畫
- Client 圖示與 Router 區分

---

## 📜 License

MIT License — 可自由使用、修改與擴充。



