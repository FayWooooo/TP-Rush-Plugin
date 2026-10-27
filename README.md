# Taipei Rush 臺北狂飆 - 外掛設定

歡迎來到 **Taipei Rush** 外掛程式設定指南！本專案整理了透過瀏覽器開發者工具（Console）直接修改遊戲內部 `state.data` 的實用指令，讓你輕鬆解鎖部分遊戲設定。

---
## 一、運行原理

### 🛠️ 核心存檔路徑
所有控制台指令均基於遊戲底層的核心狀態物件：
```javascript
const gameData = window.__game.renderer.gl.domElement.offsetParent.attributes[0].ownerDocument.defaultView.__xinyi.W.taxis.ctx.state.data; 
```

## 二、修改代碼教學
- ### 步驟一：於遊戲畫面上 **點擊右鍵 -> 檢查** 或是 **按下F12**。
- ### 步驟二：於最上排之選單選擇 **Console**。
- ### 步驟三 (若以設定可略)：於輸入區輸入 **allow pasting**。
- ### 步驟四：將下方之參考代碼貼上輸入區並按下 **Enter**。
## 三、參考代碼

### 💰 修改餘額
可自行修改金額數值：
```javascript
(() => { const v = window.__game?.renderer?.gl?.domElement?.ownerDocument?.defaultView || window; const findCtx = (o, d = 0) => { if (!o || d > 5 || typeof o !== 'object') return null; if (o.ctx?.state?.data) return o.ctx; for (let k in o) { try { let r = findCtx(o[k], d + 1); if (r) return r; } catch (e) {} } return null; }; const ctx = findCtx(v.__xinyi) || findCtx(window); if (ctx?.state?.data) { ctx.state.data.money = 999999; } })();
```
注：若金額超過一定限制，將會遭官方收回。
### 🎯 解鎖全任務
目前有142個任務，請依當前總任務數修改數值：
```javascript
window.__game.renderer.gl.domElement.offsetParent.attributes[0].ownerDocument.defaultView.__xinyi.W.taxis.ctx.state.data.completedMissions = Array.from({ length: 142 }, (_, i) => `mission_${i + 1}`);
```
### 🧭 修改遊玩時間
此時間為99年，請依需求調整遊玩時間：
```javascript
window.__game.renderer.gl.domElement.offsetParent.attributes[0].ownerDocument.defaultView.__xinyi.W.taxis.ctx.state.data.stats.playTime = 3122064000;
```
### 🐱 修改背包之招財貓
目前最多30隻，數量可超過限制：
```javascript
Object.keys(window.__game.renderer.gl.domElement.offsetParent.attributes[0].ownerDocument.defaultView.__xinyi.W.taxis.ctx.state.data.bag).forEach(key => window.__game.renderer.gl.domElement.offsetParent.attributes[0].ownerDocument.defaultView.__xinyi.W.taxis.ctx.state.data.bag[key] = 99);
```

--- 
這份專案是否有幫助到您？ 歡迎給出回饋！
