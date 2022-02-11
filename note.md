主要規則：
1.個人帳號密碼登入後，會進入產品後台頁面 ( index.html )
2.若是帳號密碼錯誤即會退回登入頁 ( login.html )

參考文件：
Bootstrap 5 引入：https://getbootstrap.com/docs/5.1/getting-started/introduction/#quick-start
Axios CDN 路徑：https://cdnjs.cloudflare.com/ajax/libs/axios/0.24.0/axios.min.js
Vue CDN 路徑：https://cdnjs.com/libraries/vue
Axios 套件文件：https://github.com/axios/axios
MDN Cookie 文件：https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie
cookie token 參考文件 https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie#%E7%A4%BA%E4%BE%8B3_%E5%8F%AA%E6%89%A7%E8%A1%8C%E6%9F%90%E4%BA%8B%E4%B8%80%E6%AC%A1

任務拆解流程：Part 1 ---> Part 2

製作流程 Part 1：login.html / login.js
1. 先做 login 頁面
2. 引入 bs5 的 css js / axios 的 js  
3. 引入 本機 css / js 檔，並且設定 type="module"
4. 載入vue esm，接著 import { createApp } from 'https://cdnjs.cloudflare.com/ajax/libs/vue/3.0.9/vue.esm-browser.js'; 最後記得掛載上去 mount
5. 資料定義 apiUrl
6. 資料定義，因為要取得帳號密碼，先定義 user 輸入的  username / password，用 v-model 雙向綁定，畫面有變更，資料也會跟著變更
7. 帳號密碼輸入之後，觸發 form 表單或是點擊按鈕登入的函式 login()，綁在 form 可以由按鈕或任何表單事件觸發，綁在 button 只能是由點擊觸發 ，兩者觸發行為不同
8. 用 axios.post 發送登入的請求，帶入 api 並帶入user 帳號密碼
9. 使用 .then .catch 取得正確或錯誤回應
10.取得正確回應之後，取出 token, expired ，用解構形式定義變數
11. 寫入 cookie token ，並設置有效時間 expired 要用 unix timestamp 轉換，
時間戳格式撰寫 new Date(expired)，接著設定 cookie 為以下語法 ( 建議改為樣板字面值，也就是反引號)
document.cookie = `jiangsToken=${token};expires=${new Date(expired)}; path=/`;
12. cookie 設定完成後可以在網址列查看
13. 登入成功之後用 window.location 轉址到 products.html 產品頁面

製作流程 Part 2：index.html / index.js
1. 製作 Part 2：index 頁面
2. 引入 bs5 的 css js / axios 的 js  
3. 引入 本機 css / js 檔，並且設定 type="module"
4. 接著 import { createApp } from 'https://cdnjs.cloudflare.com/ajax/libs/vue/3.0.9/vue.esm-browser.js';
5. checkLogin 確認登入是否正確用POST請求 api/user/check
6. 把登入的資訊，透過 header 傳送 
7. 在 mounted 生命週期就直接觸發行為
8. 先取出 Token，每次發送請求時都把 token 加到 headers
9. getData 取得產品列表 products
10. 產品細節，暫存資料 tempProduct


製作流程 Part 3：modal 新增/編輯/刪除
1.樣板先載入
2.抓取列表
3.展開 modal 製作函式 openModal()
4.新增 modal
5.編輯 modal
6.刪除 modal
