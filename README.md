6/23

6/22

6/21

6/20

6/19

6/18
- 了解 Pyhthon 專案資料夾結構 [📙](https://docs.astral.sh/uv/guides/projects/#creating-a-new-project) [📙](https://zsl0621.cc/python/src-layout-vs-flat-layout)
  - 分為 [flat layout 跟 src layout](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/)。後者為新專案的大宗，是為了
    - 避免開發者電腦有裝套件A，但是虛擬環境裏頭沒有裝，導致本地跑測試通過，上雲端跑卻失敗狀況。因為程式碼被關在 src/ 裡面，所以會強迫先檢查 pyproject.toml，並安裝套件
    - 避免套件的程式碼內 import 的 .py 檔跟開發者自己新增的.py檔名稱剛好相同時，import 錯誤造成的 crash
  - 使用 uv 指令初始化專案
    - <img width="441" height="412" alt="螢幕擷取畫面 2026-06-18 111305" src="https://github.com/user-attachments/assets/8288b90b-2110-4d7e-bca9-4e9bf5a65922" />
    - `uv init --lib`、`uv init --package`都會使用src layout，但前者比較適合做套件給別人用的場景，後者則是一般開 API 的場景

6/17

6/16

6/15

6/14

6/13

6/12

6/11
- 了解[uv](https://docs.astral.sh/uv/getting-started/installation/#next-steps)，並試用
  - uv 是 Python 專案管理與套件安裝工具（pip + virtualenv + poetry 的結合，就像前端的 vite）
  - 可以一次管理多版本的 Python (就像前端的 nvm)
  - 其核心哲學是「不污染全域環境」，所以 uv 管理的 Python 環境並不能直接透過 python 指令執行，必須透過 uv 來執行
  - uv 已整合 ruff，執行`uv format`就可整理.py檔案，不用自行安裝ruff。如果想要修改 ruff 設定可以新增 ruff.toml
  - uv 已整合 ty，執行`uv check`就可以對.py檔案做型別檢查，不用自行安裝ty

6/10

6/9

6/8

6/7

6/6

6/5

6/4

6/3

6/2
- 閱讀[前端渲染模式的選擇](https://app.notion.com/p/explainthisio/1122d1d1de188060a422debaa81af5e4)
  - 傳統SSR
    - 由伺服器渲染好整個頁面，再送給客戶端
    - 優點
      - 如果客戶端裝置爛、網路差，也不用擔心 JS 太大包，要下載與解析很久才能完成渲染
      - 伺服器送給客戶端的 HTML 裡面已經有內容，所以不用擔心 SEO
    - 缺點
      - 換頁的體驗差。(因此後來產生了CSR)

  - CSR
    - 由客戶端使用 JS 做渲染
    - 優點
      - 不需用由伺服器選染好，再送新的一頁到客戶端。因此不會因為換頁造成的不佳使用者體驗
      - 前後分離，比起前後不分的程式碼好維護
    - 缺點
      - 因為要執行JS，所以剛進網站的等待時間比較久
      - 即便Google的爬蟲能夠爬CSR網站，但有可能因為JS執行太久，而把爬取網站的額度用光，進而導致SEO較差 (回去用傳統SSR不是好方法，所以後來又產生了hydration)

  - hydration SSR
    - 第一個 frame 由 SSR 渲染，之後的 frame 交由 JS 處理。(如果不特意去啟用CSR、ISR模式) Next、Nuxt都使用這項技術
    - 優點
      - 相較 CSR，使用者能更快看到第一個畫面
      - 保有CSR換頁時的優良使用者體驗
    - 缺點
      - hydration執行完以前會有一段期間看得到畫面，但沒辦法有互動
      - 比起 CSR，部署會更複雜

  - streaming SSR
    - 由伺服器渲染 HTML，並客戶端。只要一小塊渲染好就傳給客戶端，如此重複多次
    - 優點
      - 使用者能比CSR、hydration更快看到第一個畫面，因此使用體驗會更好

  - 改良版 hydration SSR
    - 分為漸進式、島嶼架構，還有前兩者混合的選擇式注水
    - 漸進式注水，可以設定哪個部分先注水，在頁面剛加載時只注水重要的部分，其他部分等後續再注水。如果先注水的花比較久，後面注水的就會先被卡住
    - 島嶼架構把頁面拆成不同元件，只有需要互動的部分才注水。**某一塊的注水不影響另外一塊**，所以假如有某一塊元件要花比較久的時間處理，其他塊還是可以先完成注水 

  - SSG
    - build time事先把 HTML 都渲染好。根據使用者訪問的路由直接傳渲染好的 HTML 給客戶端
    - 優點
      - 不用等伺服器端渲染的時間，所以比 SSR 快。搭配 CDN 快取的話，又能更快
    - 缺點
      - 所有內容都在 build time 時渲染好，所以只要內容有更動就要重新 build，因此很耗資源。只適合內容很少更動、所有使用者都看到一樣內容的靜態網站

  - ISR
    - 產生 HTML 並快取起來，之後的請求會直接回傳這份靜態結果。可以設定 revalidate 時間。當超過這個時間後的第一個請求，伺服器會先回傳舊頁面，同時在伺服器背景重新生成新的 HTML，更新快取內容。下一次請求就會拿到新版頁面
    - 優點
      - 繼承 SSG 的所有優點
      - 不全部頁面重 build，只重 build 有更新的部分，所以比 SSG 省資源

6/1
