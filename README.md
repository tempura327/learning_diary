10/15

10/14

10/13

10/12(S)

10/11(S)

10/10
- 了解如何透過改HTML、CSS優化效能 [📗](https://developer.chrome.com/docs/lighthouse/performance/dom-size?utm_source=lighthouse&utm_medium=devtools&hl=zh-tw) [📗](https://yaron-galperin.medium.com/memory-matters-understanding-heap-snapshots-in-javascript-with-chrome-devtools-53abc33ef9df)
   - 把DOM element 攤平 [📗](https://play.tailwindcss.com/frGPbi9PDL)
     <img width="1907" height="342" alt="螢幕擷取畫面 2025-09-09 212640" src="https://github.com/user-attachments/assets/68872db1-96e5-465f-a466-d116785b4c66" />
     <img width="1908" height="434" alt="螢幕擷取畫面 2025-09-09 221021" src="https://github.com/user-attachments/assets/59900e2e-81bd-4a65-9e09-d4396e222440" />
     以上圖中的兩個例子，都是左側效能會比較好
    - 看不到，或者變看不到的DOM element 不要掛到DOM上
       - infinite scroll
       - content-visibility + contain-intrinsic-size
    - 使用atom css，或者BEM，避免效能問題雪上加霜
- Tailwind 效能較好的原因
    - 無層級選擇器，所以不需要遍歷 DOM 樹檢查父子關係，瀏覽器可以直接用 hash table 查找，因此時間複雜度可趨近 O(1)
    - 樣式隔離：每個 class 只影響單一屬性，計算簡單
    - PurgeCSS，prod只保留用到的 classes

10/9
- 了解browsing context [📗](https://developer.mozilla.org/en-US/docs/Glossary/Browsing_context)
   - browsing context是一個環境，每個視窗、瀏覽器tab、iframe都有自己的browsing context
   - 每個browsing context都有自己的origin (protocol+domain+port)
   - browsing context包含window(e.g. history, opener)、active document(當前頁面的DOM) [📗](https://developer.mozilla.org/en-US/docs/Glossary/WindowProxy)
   - 有些browsing context可以跟同個origin的其他browsing context共享資訊 (e.g. localStorage, cookies)

- 了解reverse tab nabbing攻擊 [📗](https://aszx87410.github.io/beyond-xss/ch3/html-attack/) [📗](https://developer.chrome.com/docs/lighthouse/best-practices/external-anchors-use-rel-noopener?hl=zh-tw)
   - 使用noopener可以避免開啟的新頁面讀取window.opener，如此可禁止頁面N存取window.opener，進而把頁面O的的網址改成導向有危險的頁面
   - 不過只設noopener仍然會提供referrer資訊給HTTP header，如果不想要header內有referrer資訊，可以使用noreferrer
   - 當設了noreferrer會發生兩件事，1.不會提供referrer資訊給HTTP header，2.自動將noopener設為true [📗](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel/noreferrer) [📗](https://developer.mozilla.org/en-US/docs/Web/API/Window/open#noopener)
     ```html
     <a href="你要去的網頁N" target="_blank" rel="noreferrer">
     文字
     </a>
     ```
    
     ```js
     window.open(
       '你要去的網頁N',
       '_blank',
       'noreferrer',
     );
     ```
   
10/8

10/7

10/6

10/5(S)

10/4(S)

10/3

10/2

10/1

9/30

9/29

9/28(S)

9/27(S)

9/26

9/25

9/24

9/23 🚲
- 了解肥大的DOM 對效能的影響 [📗](https://www.debugbear.com/blog/excessive-dom-size?fbclid=IwY2xjawLjJGZleHRuA2FlbQIxMQABHq5gx9YywY3XY8Hk8fGFqxwXRyRXvH_hMuVZplvtybpE5FcuFubMI7vSms1y_aem_WBm8f-1Yxdh9tTAZJqRXeg) [📗](https://developer.chrome.com/docs/lighthouse/performance/dom-size?utm_source=lighthouse&utm_medium=devtools&hl=zh-tw)
  - 肥大的DOM意味著裡頭包含更多的DOM element，瀏覽器需要處理的東西會更多
  - 記憶體方面
    - DOM element本身的就有非常多屬性，而儲存屬性需要記憶體
    - 使用JS操作DOM element時，常會用document.querySelector()把DOM element的reference存到變數，再來操作，因此會消耗記憶體
    - DOM 越深，事件冒泡路徑越長，需要更多記憶體追蹤
  - CPU方面
    - 瀏覽器需要下載、解析較大的HTML
    - reflow、repaint的時間更長
      - 每次scroll都會需要瀏覽器repaint，所以卡頓常會出現在scroll時
    - CSS 計算更吃效能
      - 瀏覽器遍歷更多DOM element，並計算所有匹配的 CSS 規則，再根據權重決定最終樣式
      - 計算後的樣式值會被存到記憶體
      - 維護樣式繼承鏈
- 使用lighthouse檢測網頁效能時，有1個指標是關於DOM size，底下又拆成3個小項目
  - DOM element總數，唯一會影響效能分數的指標
  - 最大DOM深度(Maximum DOM Depth)，最好不要超過30
  - 最大子節點數(Maximum Child Nodes)，最好不要超過50
- 相關名詞
  - LCP (Largest Contentful Paint)，網頁主要內容載入完成的時間
    - HTML 檔案因為 DOM 多而變很大（如 500KB），下載時間變長，是影響 LCP、FCP的其中一個因素
  - FCP (First Contentful Paint)，網頁開始載入到第一個內容出現在畫面上的時間
  - INP (Interaction to Next Paint)，因使用者跟網頁互動產生的re-render所花的時間
    - scroll時出現卡頓，就是一種INP不佳的情況

9/22 🚲

9/21(S)

9/20(S)

9/19 🚲
- 了解瀏覽器渲染網頁的流程 [🔖](https://github.com/tempura327/learning_diary/blob/master/2024/README.md#1121)
   1. 下載HTML
   2. 下載CSS
   3. 解析HTML，產生DOM tree、解析CSS，產生CSSOM tree
   4. 將DOM tree跟CSSOM tree結合，產生render tree
   5. layout (reflow)，計算每個node的幾何資訊 (位置、大小)
   6. paint (repaint)，將每個node畫到螢幕上
- 了解瀏覽器怎麼計算網頁樣式 [📗](https://web.dev/articles/reduce-the-scope-and-complexity-of-style-calculations?hl=zh-tw) [📗](https://developer.chrome.com/docs/devtools/performance/selector-stats?hl=zh-tw)
   - 透過JS新增及移除元素、變更屬性、類別或播放動畫來變更 DOM，會導致瀏覽器重新計算元素樣式，這被稱作「樣式計算 (style calculation)」
   - 瀏覽器計算樣式的步驟
      1. 瀏覽器會根據CSSOM建立一組相符的選取器(matching selectors)，藉此判斷哪些CSS rule可以套用到哪些DOM element
       ```css
       // 假設有這些css rule
       span { color: red; }
       .text { color: blue; }
       p span { font-size: 14px; }
       #cat-food-advertisement-title { color: green; }
       ```
  
       ```html
       <p>
         <span id="cat-food-advertisement-title" class="text">文字</span>
       </p>
       ```
  
       在這個步驟會去看有哪一些css rule可以套用在這個 span 上
       ```
       matchedRules = [
         "span { color: red; }",        // ✓ 符合
         ".text { color: blue; }",      // ✓ 符合
         "p span { font-size: 14px; }"  // ✓ 符合
         "#cat-food-advertisement-title { color: green; }" // ✓ 符合
       ]
       ```

      2. 對比可以套用的CSS rule之間的選擇器權重，決定套用的CSS rule
        - 優先序為 !important > 內聯樣式 > ID > Class > Element
      3. 套用預設值，如果本身沒有設定該屬性，就使用瀏覽器預設值
      4. 處理樣式繼承，如果本身沒有設定該屬性且父元素有設定該屬性，則會再從父元素繼承，把預設的樣式值覆蓋掉
      5. 計算相對值 (e.g. 2rem = 32px、50% = 500px)
      6. 計算最終樣式值 (computed style values)，並存到記憶體
 - 影響樣式計算效能的因素
    - DOM element數量太多
    - CSS rule數量太多
    - CSS 選擇器複雜
      ```css
       /* 瀏覽器會從右到左匹配，這是CSSOM優化的其中一個機制，但在選擇器過長時效能反而更差，因為要檢查的項目變多了 */
       .container .list .item {
          color: #44AF69;
       }
       /* 匹配所有元素，效能最差 */
       * {
         color: #333333;
       }
       /* 選擇器過度複雜 */
       /* .list 底下第一層中，除了第一個.item元素外的所有.item兄弟元素 */
       .list > .item + .item {
          margin-top: 16px;
       }
      /* 偽類(pseudo-classes)的選擇器效能差 */
      /* 偽類選擇器是指:first-child、:not、:nth-child()、:hover、:active這類的選擇器，但是::before、::after並不是偽類選擇器，而是為偽元素(pseudo-elements)選擇器 */
      /* 偽類選擇器無法使用CSSOM的hash table機制快速查找，甚至當中有部分還要做real time的計算，因此效能差 */
       .item:not(:first-child) {
          margin-top: 16px;
       }
      ```
   - 大量使用style屬性控制樣式 (內聯樣式)會導致無法利用 CSS 快取、CSSOM 優化
       ```html
       <div class="product-list">
         <div style="display: flex; padding: 20px; margin: 10px; background: white; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); cursor: pointer; transition: all 0.3s;">
           <img style="width: 100px; height: 100px; object-fit: cover; border-radius: 4px; margin-right: 15px;" src="product1.jpg">
           <div style="flex: 1; display: flex; flex-direction: column; justify-content: space-between;">
             <h3 style="margin: 0; font-size: 18px; color: #333; font-weight: 600;">產品 1</h3>
             <p style="margin: 5px 0; color: #666; font-size: 14px; line-height: 1.5;">產品描述...</p>
             <span style="color: #ff6b6b; font-size: 20px; font-weight: bold;">$299</span>
           </div>
         </div>
         <!-- 同樣的樣式的div繼續重複 -->
       </div>
       ```


9/18

9/17 🚲
- [獵人頭談薪水: 你該告訴獵人頭(headhunter)你現在的薪水嗎?](https://www.ipibresume.com/blog/blog/do-i-need-to-leak-out-salary-to-headhunters/?trk=feed_main-feed-card_feed-article-content)
    - 不需要，因為這不是好籌碼
    - 不需要，獵頭、人資常常認為只該給求職者+10%的薪資
    - 例外的情況是你真的相信獵頭知道數字後會幫你爭取更高的薪水
- [轉職當工程師之後卡等了嗎？那你需要知道「職涯籌碼金字塔」](https://www.youtube.com/watch?v=nSwEuSMG_rY)
    - 籌碼=面試技巧+技術+資歷×頭銜×戰勳×內涵×作品×人脈
    	- 戰勳是乘數當中較能自己控制的
        - 戰勳=驅動(動力)+行動(執行)+成就(好的結果)+行銷(宣傳結果)

9/16 🚲
- 初步瞭解[Gin](https://github.com/gin-gonic/gin)是什麼
    - Golang的框架之一
    -  API設計直觀，容易上手，且效能比其他Go框架快40倍
- 瞭解一些Golang專案的慣例
    - 套件（package）指同個資料夾內所有的 .go 檔案，檔案內的package 宣告必須相同
        - 如果同一個資料夾內的 .go 檔案宣告不同的 package 名稱，Go 編譯器會直接報錯，無法編譯
    - /cmd放應用程式，/internal放private的package，/pkg放public的package
        - 放在 cmd/ 目錄下的程式碼，是應用程式的進入點，例如cli、server、serverless function等
        - 放在 internal/ 目錄下的程式碼，Go 編譯器會強制其他專案無法 import 來使用這些套件
    - 檔案命名snake_case、變數跟函式命名都用camelCase，private用camelCase，public用PascalCase(CamelCase)
    - /bin內裝編譯後的結果

9/15 🚲
- 初步了解Golang的Array跟Slice的差異 [📙](https://go.dev/tour/moretypes/11)
   ||Array|Slice|備注|
   |---|---|---|---|
   |長度|固定|不固定|只能用type來分是哪種|
   |機制|直接建立一個固定長度的Array|先建立一個匿名Array，然後建立一個slice指向它||
   |reference||Array的reference，跟JS的Array一樣是傳址||
   |重新賦值|標明型別再重新賦值，或者用copy、逐一手動賦值|標明型別再重新賦值，或者用copy、逐一手動賦值|
- 瞭解slice的length、capacity的概念 [📙](https://go.dev/tour/moretypes/11)
   - length是slice其包含的元素數量，可用len()取得
   - capacity是slice指向的底層array中元素的數量，計算方式是從slice當前起始位置到底層陣列結尾的元素個數，可用cap()取得
       ```golang
       func main() {
           s := []int{2, 3, 5, 7, 11, 13}
           printSlice(s)

           s = s[2:]
           // 計算方式是從slice當前起始位置到底層陣列結尾的元素個數，所以cap是4
           // len=4 cap=4 [5 7 11 13]
           printSlice(s)
       }

       func printSlice(s []int) {
           fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
       }
       ```

       ```golang
       func main() {
           s := []int{2, 3, 5, 7, 11, 13}
           printSlice(s)

           // 計算方式是從slice當前起始位置到底層陣列結尾的元素個數，所以cap是4
           // len=2 capa=4 [5 7]
           s = s[2:4]
           printSlice(s)
       }

       func printSlice(s []int) {
           fmt.Printf("len=%d capa=%d %v\n", len(s), cap(s), s)
       }

       ```


9/14(S)

9/13(S)

9/12

9/11

9/10
- 可觀測性(observability, o11y) [📗](https://www.explainthis.io/zh-hant/swe/what-is-observability-and-why-it-matters) [📗](https://www.explainthis.io/zh-hant/swe/how-should-sofhow-swe-do-monitoring)
  - 可觀測性是指能去衡量一個系統內部狀態的能力。當一個系統是可觀測的，開發人員可以輕易地去觀測到系統內部究竟發生什麼事
  - 監控則是指搜集不同的可觀測性資料，來判斷系統目前是否有異狀，並在異常時發出警報。透過監控可以提升可觀測性
  - 可觀測性數據分為日誌(logs)、指標(metrics)、追蹤(traces)。預設的情況下三者是獨立的，但也可以自行結合使用
  - metrics
    - metrics會持續收集系統的量化數據並呈現趨勢變化
    - 因為metrics提供了可量化、可比較的數值指標，它告訴你出了什麼問題 (e.g. 回應時間從 100ms 升到 500ms)
  - traces
    - traces 會記錄一個請求的完整生命週期 (e.g. request經過哪些服務、花了多少時間、有沒有錯誤、服務之間的依賴關係)
    - 因為traces知道整個過程經歷了什麼，它會告訴你哪個環節出了問題 (e.g. 80% 時間卡在資料庫查詢)
  - logs
    - log記錄系統中具體發生的事件，不管是不是錯誤都會記錄
    - 因為log知道具體發生了什麼，它會告訴你具體出錯的地方 (e.g. SQL 查詢語句、錯誤訊息)
  - 警報(alerts)是基於可觀測性數據設定的自動通知機制
- 初步了解AWS的CloudWatch
  - metrics: CloudWatch Metrics
  - traces: CloudWatch Application Signals (Traces) 或 X-Ray
  - logs: CloudWatch Logs
  - alerts: CloudWatch Alarms
  - dashboard(將metrics畫成圖表): CloudWatch Dashboard


9/9 🚲
- 初步了解空間預分配
   - 預分配是指程式開始時就準備好足夠大的記憶體空間，而不是需要時才分配，這可以避免頻繁操作記憶體
   - 頻繁的記憶體操作導致一些效能問題
      - 記憶體碎片化
         - 外部碎片 - 記憶體被切成很多小塊，找不到連續的大空間
         - 內部碎片 - 分配的空間比實際需要的大，造成浪費
         - 記憶體洩漏風險 - 頻繁分配容易忘記釋放，累積成記憶體洩漏
      - 垃圾回收壓力
         - GC頻繁觸發 - 產生太多小物件讓垃圾回收器工作更頻繁
         - 停頓時間增加 - GC執行時程式會暫停，影響回應速度
         - 記憶體使用量飆高 - 來不及回收的物件佔用大量記憶體
      - 系統穩定性
         - 記憶體不足 - 頻繁分配可能導致可用記憶體耗盡，嚴重時可能因為記憶體不足而crash
         - 系統變慢 - 作業系統忙於處理記憶體請求，整體效能下降
      - 效能
         - 擴衝容量時需要把舊資料複製到新位置，資料越大越慢
         - 記憶體位置改變會讓CPU快取失效，存取速度變慢

   - 空間預分配可解決以下問題
      - 記憶體碎片化問題
      - 垃圾回收壓力和程式暫停時間
      - CPU快取失效和存取延遲
      - 系統呼叫、記憶體拷貝開銷


9/8 🚲
- 了解Golang的make、new
  - new()
    - 回傳類型 - 回傳指標（pointer），指向零值初始化的記憶體
    - 適用範圍 - 可用於任何類型，但對slice/map/channel只是分配記憶體空間
    - 初始化程度 - 只進行零值初始化，不做底層資料結構的建立
    - 使用限制 - 對於slice還可勉強使用（配合append），但map和channel的nil狀態無法正常工作
    - 記憶體效果 - 單純分配記憶體並設為零值，需要額外步驟才能實際使用

  - make()
    - 回傳類型 - 回傳已初始化的值本身，可以立即使用
    - 專用類型 - 只能用於slice、map、channel這三種引用類型
    - 底層初始化 - 完整建立底層資料結構（記憶體分配、索引建立、預設值設定、運作機制）
    - 預分配功能 - 可指定長度和容量來預先分配空間，避免頻繁記憶體操作
      ```golang
      // slice長度5、容量10
      make([]int, 5, 10)

      // map預分配100元素空間
      make(map[string]int, 100)
       // channel緩衝區50元素
      make(chan int, 50)
      ```

9/7(S)
- 重新了解.map()、.filter()、.reduce()的運作方式
  - 未使用await把async function的結果resolve的情況，async function的回傳值一定是Promise物件
  -  map 只是將每個元素轉換成新值，所以callback是不是async function沒差
    ```js
    const res = await Promise.all(
      cabinetsData.map(async ({ id, ...rest }) => {
        const { data } = await queryCabinets({
          variables: {
            filter: {
              organizations: [organizationId],
              cabinetId: id,
            },
          },
        });
    
        const isExist = (data?.CabinetsQuery.cabinets.edges || []).length > 0;
    
        return isExist ? { id, ...rest } : null;
      }),
    );
    ```
  - filter則會涉及到邏輯判斷
    - Promise物件在布林判斷時永遠是 truthy，所以才會導致條件判斷失效
    ```js
    const res = await Promise.all(
      cabinetsData.filter(async ({ id, ...rest }) => {
        const { data } = await queryCabinets({
          variables: {
            filter: {
              organizations: [organizationId],
              cabinetId: id,
            },
          },
        });

        const isExist = (data?.CabinetsQuery.cabinets.edges || []).length > 0;

        return isExist;
      }),
    );   
    ```

  - reduce則會涉及到累積值的取得
    - reduce 期待每次迭代時，第一個參數要拿到「實際的值」來累加或者判斷後再累加，但是async function回傳的是Promise物件，所以會導致累加錯誤

    ```js
    const res = await Promise.all(
      cabinetsData.reduce(async (acc, { id, ...rest }) => {
        const { data } = await queryCabinets({
          variables: {
            filter: {
              organizations: [organizationId],
              cabinetId: id,
            },
          },
        });

        const isExist = (data?.CabinetsQuery.cabinets.edges || []).length > 0;

        if (isExist) {
          return [
            ...acc,
            { id, ...rest }
          ]
        }

        return acc;
      }, []),
    );   
    ```

9/6(S)

9/5

9/4

9/3

9/2
- 了解使用CSS達成按enter時將文字斷行
   - 使用JS達成效果效能較差的原因
	    - 每次創建新的 DOM element 都需要瀏覽器重新計算佈局（reflow）
    	- 多個元素意味著更多的記憶體使用

	    ```text
         本署「114年天氣分析與預報研討會」舉辦時間訂於114年9月2(二)~4日(四)，
         歡迎各位專家學者踴躍至本研討會專網報名。
   
          網址: https://conf.cwa.gov.tw/
        ```

		就算使用React之類的框架，效能還是會比用CSS差，因為每次 render 都要重新呼叫.split()

        ```js
        // React
        <div className="flex flex-col">
         {article.split('\n').map((text)=>(<span key={`text-index`}>{text}</span>))}
        </div>
        ```
   - white-space屬性
       - pre-wrap ⭐️
           ```css
           white-space: pre-wrap;
           ```
           保留空白字元，並且會自動換行
         	<img width="1060" height="180" alt="pre-wrap_0" src="https://github.com/user-attachments/assets/165c3d53-61b8-4bf1-8a96-8ed8f9f94e0b" />

          

       - pre-line ⭐️
           ```css
           white-space: pre-line;
           ```
           合併空白字元，但會保留換行符號
			<img width="1058" height="181" alt="pre-line_0" src="https://github.com/user-attachments/assets/f91ac950-2140-4e21-8694-1440a0eaa7e3" />

       - pre
           ```css
           white-space: pre;
           ```
           保留空白字元與換行符號 (使用者輸入什麼就是什麼)
			<img width="1102" height="180" alt="pre_0" src="https://github.com/user-attachments/assets/6e3b4d7b-8198-453a-84bc-6e194a963157" />



9/1(M) 🚲

7/28~8/31 休息

7/27(S)

7/26(S)

7/25
- 了解Go的pointer[📙](https://go.dev/tour/moretypes/1)
   - pointer儲存的是變數在記憶體中的位址，不是變數的值本身
   -透過pointer可以間接存取和修改另一個變數的值
   - 傳遞大型資料結構時，傳pointer比複製整個資料更有效率，因為更省記憶體
   - 多個函數可以透過pointer存取同一份資料
   - 未初始化的pointer值為nil，不指向任何記憶體位址
   ```go
   func main() {
      i, j := 42, 2701
   
     // 把i的記憶體位置存到變數p，變數p是一個pointer
      p := &i       
      // 取得p指向的記憶體位置所存的值(透過p讀取i的值)
      // *表示pointer底層的值(pointer指向的記憶體位置存的值)
      fmt.Println(*p)
      // 透過p間接改變i的值
      *p = 21
      fmt.Println(i)
   
      // 把p存的記憶體位置改成j的位址
      p = &j     
      // 透過p間接改變j的值  
      *p = *p / 37
      fmt.Println(j)
   }
   ```


7/24

7/23 🚲
- 了解Go的defer [📙](https://go.dev/tour/flowcontrol/12)
  - defer可以確保function一定會執行，即使函數中途return或發生panic，function仍一定會被呼叫，可避免memory leak
  - 其中一個優點是把「清理工作」寫在「獲取資源」的旁邊，讓程式碼更容易理解和維護，也不容易遺漏清理步驟
  - defer主要有記錄log、釋放資源、錯誤處理與恢復等用途，這些使用場景都跟`defer確保function一定會執行`的特點有關
    - 在函數進入和退出時自動記錄日誌，方便追蹤程式執行流程
    - 在函數結束時釋放資源（如關閉檔案、網路連線等），避免memory leak，因為用了
    - 在函數發生錯誤時恢復程式執行，避免crash
  - 會遵循stack的後進先出原則執行多個defer function
  ```go
    // 依counting, done, 109~100, 9~0的順序印出
    func main() {
      fmt.Println("counting")
  
      for i := 0; i < 10; i++ {
        defer fmt.Println(i)
      }
  
      for i := 100; i < 110; i++ {
        defer fmt.Println(i)
      }
  
      fmt.Println("done")
    }
  ```

- 閱讀[為什麼要手動resp.Body.Close()](https://www.zhangjiee.com/blog/2018/go-http-get-close-body.html)
  - 提高效率，http.Get 等請求的 TCP 連線是不會關閉的（再次向同一個網域請求時，重複使用連線），所以必須手動關閉，忘記Close()或程式中途退出，HTTP連線就會一直佔用系統資源，累積多了就可能導致系統無法建立新連線



7/22
- 了解Go的switch [📙](https://go.dev/tour/flowcontrol/11)
  - switch條件不需用()包起來，但執行的內容必須用{}包起來
  - switch的條件前可以短宣告，相當於先宣告變數再將該變數用於switch的條件
  - 每個case的最後Go都會自動加入break，所以不用自己寫
  - case不必是常數、整數，不必是常數指的是可以在case做計算
    ```go
    switch time.Saturday {
      case today + 0:
        fmt.Println("Today.")
      case today + 1:
        fmt.Println("Tomorrow.")
      case today + 2:
        fmt.Println("In two days.")
      default:
        fmt.Println("Too far away.")
    }
    ```
  - 沒有條件的switch會被當作是條件為true的switch，可以用它來代替一個很長的if-else結構

7/21 🚲

7/20(S)

7/19(S)

7/18

7/17

7/16
- 閱讀[Day5- 來概念解構 Fabric.js 吧 (3)-事件(events)與生命週期](https://ithelp.ithome.com.tw/articles/10343616)
 - 提供一些事件可以綁定到fabric.Canvas instance上，也可以自訂事件

- 閱讀[Day6- 小小介紹 Fabric.js 的歷史沿革](https://ithelp.ithome.com.tw/articles/10343926)
 - 用虛擬畫布、批次渲染來優化效能
 - 虛擬畫布指的是建立fabric.Canvas instance，但不傳入DOM元素
   ```js
   new fabric.Canvas(null, options)
   ```
   - `常用於`匯出圖片、在伺服器端產圖這類`不需要有可互動的`canvas的場景
 - 批次渲染是指逐步繪製畫布上的內容，而不一次完成繪製
   - 分成動態畫布、靜態的兩個畫布，然後疊一起讓它們看起來像一個畫布。靜態畫布上會放很少變動、不變動的東西
   - 只重繪有變動，所以需要重繪的部分，如此就可以省掉重繪靜態畫布的開銷


7/15
- 了解Go的if [📙](https://go.dev/tour/flowcontrol/7)
  - if條件不需用`()`包起來，但執行的內容必須用`{}`包起來
  - if的條件前可以短宣告，相當於先宣告變數再將該變數用於if的條件
  - if的短宣告的變數可以在一組的其他else block取用
- 閱讀 [Day4-來概念解構 Fabric.js 吧 (2)-物件導向特性與物件(Object)與擴展機制(extend)](https://ithelp.ithome.com.tw/articles/10343614) 作為side project參考
  - fabric分為動態畫布、靜態畫布，只有前者可以跟使用者互動
  - 可用`fabric.util.createClass()`、`fabric.[ClassName].prototype.extend()` 創建新的class、擴展class，因此fabric自由度很高

7/14
- 了解Go的迴圈 [📙](https://go.dev/tour/flowcontrol/4)
  - Go的for 迴圈、while迴圈都使用for keyword
  - for迴圈初始化變數用短宣告，後面是條件、post action，三者中間用 `;` 隔開，但不需要`()`包住
  - while迴圈則只有條件
  - 如果只有`for {}` 會變成無限迴圈

7/13(S)
- 常數宣告
  - 常數只能用const宣告，不能用短宣告 [📙](https://go.dev/tour/basics/15)
  - 如果宣告數字類的常數時沒有給型別，那Go會根據context變換它的型別，但是如果你讓Go把一個big int轉成int就會因為溢位出錯 [📙](https://go.dev/tour/basics/16)

7/12(S)
- 做side project

7/11 🚲
- 了解Makefile [📙](https://tutorialedge.net/golang/makefiles-for-go-developers/) [📙](https://hackmd.io/@sysprog/SySTMXPvl)
  - make是 run 和 build code的工具
    - Makefile是make設定檔，通常會放在專案的根目錄，但是一個專案內可以有多個Makefile
  - Makefile裡面定義指令
    - 如果專案的部份程式碼被修改，只會編譯被修改的程式
    - 縮排必須用tab，行尾不可有空格
    - 指令的名稱被稱作target，在終端機輸入 `make <target>` 即可執行指令
    ```
    // target是hello，內容則是echo "Hello"
    hello:
      echo "Hello"
    ```
 
    - Makefile中通常放該專案常用的指令 (e.g.: build, run, clean)，指令內容可以是任何shell command
    ```
    // 用於compile code，並把結果的binary檔放到bin資料夾
    build:
      go build -o bin/main main.go
    ```

    - 定義變數
    ```
    User=Tempura
  
    hello:
      echo "Hello $(User)"
    ```
    
    - 組合指令
    ```
    hello:
      echo "Hello"
     world:
      echo "world"
  
    helloWorld:
      hello world
    ```


7/10 🚲
- 做side project

7/9

7/8
- 做side project
- 閱讀 [Day1- Fabric.js 是什麼？他可以做些什麼](https://ithelp.ithome.com.tw/articles/10343461) ~ [Day3- 來概念解構 Fabric.js 吧 (1) - 核心概念](https://ithelp.ithome.com.tw/articles/10343610) 作為side project參考

7/7 🚲
- 讀 [Advice From a Software Engineer With 8 Years of Experience](https://medium.com/better-programming/advices-from-a-software-engineer-with-8-years-of-experience-8df5111d4d55) ~ Leave the comfort zone
撰寫工作週記，有助於公司內的年度評鑑、方便寫履歷時回顧
多嘗試自己負責的專案以外的內容，或者新技術

7/6(S)
- 閱讀[面試新創公司時，應該要問的問題](https://www.explainthis.io/zh-hant/career/questions-to-ask-when-interviewing-at-a-startup)
  - 重點在於公司是否已經達到產品市場契合度 (俗稱 PMF)，但不要直接問這個問題，而是要透過問問題來判斷
  - 公司的資金、募資計畫是否能支撐公司撐下去
- 閱讀[用 ChatGPT 幫自己修英文履歷 — 軟體工程師篇](https://www.explainthis.io/zh-hant/career/use-ChatGPT-to-help-you-polish-swe-resume)

7/5(S)

7/4

7/3
- 做side project

7/2
- 多變數群組宣告 (Grouped variable declaration)
   - 除了一般的宣告、短宣告以外，也可以把多個變數宣告包在`()`裡
 ```go
 var (
   ToBe   bool       = false
   AMinuteSeconds int     = 60
 )
 ```

 相當於

 ```go
 var ToBe = false

 // 一定要宣告在function block內
 AMinuteSeconds := 60
 ```

- zero value [📙](https://go.dev/tour/basics/12)
   - 如果使用var宣告，且沒給預設值，那預設值會是falsy value (e.g: 0, false, "")

- 型別轉換 [📙](https://go.dev/tour/basics/13)
   - Go 是 強型別語言，所以不像 JavaScript 可以隨便轉，但仍然有提供一些型別轉換的function

   - 如果真的想要隨便轉，需要透過[strconv](https://pkg.go.dev/strconv)

7/1 🚲
- 做side project
  ![螢幕擷取畫面 2025-07-01 215836](https://github.com/user-attachments/assets/518432f8-f1dc-4af4-8e96-09a2b60b5fa9)


