2/15(S)

2/14(S)

2/13

2/12
- 了解後端專案的分層[📙](https://medium.com/@harshgharat663/understanding-handlers-services-repositories-middlewares-request-context-in-backend-2977539931d9)
  - 基於需求不同後端專案的分層設計都會有點不同
    - 所以有時候handler會改用controller，或者分層會多出mediator、middleware等層
    - 所以有時候會有雙層handler(HTTP handler + business handler)
  - request的lifecycle
    1. 前端發request，DNS解析得到ip後，打到server
    2. router對比路徑
    3. router分工給 HTTP handler
    4. HTTP handler叫Business handler處理request，business handler叫service處理完回給它，它再返回response給HTTP handler，HTTP handler再返回response給前端
  - handler的職責
    - request object內有parameter、body、headers之類的資料，HTTP handler會從request object裡取出parameters、body
    - HTTP handler把body裡的內容從字串轉成物件，並檢查前端該傳入的值是不是都有、都合法，或者把前端傳入的值做轉換
    - HTTP handler呼叫business handler，business handler叫service
  - Service的職責
    - Service裡裝的是純邏輯，它不會跟HTTP、資料庫有任何接觸
    - Service只加工組裡來自handler的資料、flow的安排、呼叫Repo
    - Repo的職責
  - 操作資料庫，並返回結果給Service


2/11
- 了解為什麼要幫GitHub Actions做快取 [📗](https://oldmo860617.medium.com/%E6%B7%BA%E8%AB%87-github-actions-workflows-%E7%9A%84-cache-%E6%A9%9F%E5%88%B6-f63db6f7929a)
  - 導入快取機制，可以達到沒有必要時就不用重複安裝依賴套件、重複執行專案的 build ，以此盡量減少 CI 的執行時間
    - 以前端而言，常用來快取 node_modules 或 build 結果
    - 可以使用官方提供的 [actions/cache@v6](https://github.com/actions/cache)


 - 快取行為及限制
  - GitHub Actions 可以 access 與 restore 當前分支、base分支的快取 [📗](https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching#restrictions-for-accessing-a-cache)
    - 一個Repo中快取檔案的上限是10GB，超過容量、超過7天未被使用的快取會被自動刪除
    - 步驟
      1. 去找符合key的快取
      2. 找不到的話去找符合 key 的一部分的快取
     
      3. 再找不到的話再使用 restore-keys 去找快取
      4. (需自行設置條件)都找不到的話就執行 install 或 build
      ```
       - name: Cache node modules
         id: cache-npm
         uses: actions/cache@v4
         env:
           cache-name: cache-node-modules
         with:
           # npm cache files are stored in `~/.npm` on Linux/macOS
           path: ~/.npm
           key: ${{ runner.os }}-build-${{ env.cache-name }}-${{ hashFiles('**/package-lock.json') }}
           restore-keys: |
             ${{ runner.os }}-build-${{ env.cache-name }}-
             ${{ runner.os }}-build-
             ${{ runner.os }}-

       # 設置條件才會只在 cache miss 的情況下執行
       # 如果有用setup-node，且有設定cache，那就可直接把global package data放到node_modules，不然就要從npm registry下載
       - if: ${{ steps.cache-npm.outputs.cache-hit != 'true' }}
         name: List the state of node modules
         continue-on-error: true
         run: npm list
      ```

- [actions/cache@v6](https://github.com/actions/cache)
    - 用了的話，除了執行`restore cache step`之外，最後還會自動執行一個`post cache step`
    - 傳入
      - path，要存入快取的內容所在的路徑
      - key，用於唯一標識快取的key
      - restore-keys，cache-miss時使用的fallback key
    - 如果cache hit，會顯示`Cache restored from key: {key}`
    - 如果cache miss，會顯示`Cache not found for input keys: {key}, {restore-keys}`，且在`post cache step`會顯示`Cache saved with key: {key}`
    - 搭配[actions/setup-node@v6](https://github.com/actions/setup-node#caching-global-packages-data) 一起用可以達成best practice
      - setup-node負責cache global package data，cache負責cache node_modules
      - 如果執行`setup-node step`時cache hit，會顯示 `Cache restored from key: node-cache-{runner os}-{package manager}-{hash}`

2/10
- 了解transform: translate [📗](https://www.w3.org/TR/css-transforms-1/) [📗](https://ithelp.ithome.com.tw/articles/10362313)
  - translate 是用來達到位移效果的。它**只是視覺上的位移**，不改變元素在document flow中的真實位置 
  - 因為translate只移動視覺位置，所以實際上在document flow內的真實位置並沒改變，所以真實位置沒改變就不會觸發reflow，只會在compositing階段做視覺上的位移

- 了解Gecko rendering [📗](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Fundamentals)
  - Gecko是一個瀏覽器渲染引擎，它優化了對HTML、CSS、canvas的渲染。Gekco的優化減少了因為scroll之類事件產生的repaint
  - 簡單的場境會使用系統圖形合成器(system compositor)的專用硬體渲染，一些複雜的場景則會使用GPU渲染，以提升效能
    - 使用了animation、transform: translate 的話，視複雜度可能會由GPU渲染

2/9

2/8(S)

2/7(S)

2/6

2/5

2/4

2/3

2/2

2/1(S)

1/31(S)
- 了解為何position: absolute會導致崩塌
  - **建立stacking context跟跳脫document flow無關** [🔖](https://github.com/tempura327/learning_diary/tree/master?tab=readme-ov-file#16)
  - 先不提加上z-index來建立stacking context [🖌️](https://play.tailwindcss.com/lVy997dVWQ)
    - 只要[position: absolute](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position#absolute) 就會跳脫document flow，這就是導致崩塌的原因 
    - <img width="1908" height="752" alt="螢幕擷取畫面 2026-01-31 170042" src="https://github.com/user-attachments/assets/3c4f91b1-3e25-4ad6-8f3a-dd1257e1aa86" />

1/30
- 了解sticky [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position#sticky) [🖌️](https://play.tailwindcss.com/EE7BahkKVO)
  - sticky元素會建立stacking context [🔖](https://github.com/tempura327/learning_diary?tab=readme-ov-file#16)
  - 排的依據是外層最近的可滑動的**block** element [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#1125)
  - sticky不會因為外層元素使用position: absolute/relative + z-index被影響產生偏移，但是會被transform: translateY() 影響 [🖌️](https://play.tailwindcss.com/8a1jkEj5kD)
  - 導致sticky失效的原因
    - 外層元素有 overflow
    - 外層元素的高度沒有大於要sticky的元素
    - 沒有幫sticky元素設置top或bottom

1/29

1/28
- 了解為什麼DB會踩不到index [📙](https://medium.com/johnliu-%E7%9A%84%E8%BB%9F%E9%AB%94%E5%B7%A5%E7%A8%8B%E6%80%9D%E7%B6%AD/database-%E5%85%AB%E5%80%8B-index-%E7%B4%A2%E5%BC%95-%E7%84%A1%E6%B3%95%E7%94%9F%E6%95%88%E7%9A%84-sql-%E5%AF%AB%E6%B3%95-cdc7d2e72f51)
  - B tree是有階層結構的，必須一層一層往下走
    - 多個條件時，某個條件的欄位沒有設index
    - 複合式 index 使用順序錯誤
  - B tree裡的每個節點都是一個具體的key(正面表述)
    - 傳入負面表述的條件 (e.g. NOT, !=)
    - LIKE語句中%的位置在開頭 (e.g. '%abc', '%abc%')
  - B tree裡的每個節點存的是欄位原始值
    - 使用函數語句包裝作為條件的欄位 (e.g. UPPER(name))
    - 對欄位做運算 (e.g. 1+1)

1/27

1/26
- 了解function overload [📗](https://www.typescriptlang.org/docs/handbook/2/functions.html)
  - 有時候我們會需要把function定義成可以被以多個不同數量、型別的參數呼叫，或者回傳不同型別的值，此時就會需要用到function overload
    - 用function keyword宣告的function，使用一般的overload function即可
      - <img width="639" height="812" alt="overload signature" src="https://github.com/user-attachments/assets/e4cd09d0-dcec-413c-8e6a-590473da0816" />
    - arrow function不支援overload signature，所以必須使用call signature才可達到同樣的效果 [](https://blog.logrocket.com/implementing-function-overloading-typescript/)
  - 至少要有2個overload signature，且實作一定要兼容所有overload signature
  - 如果2個overload signature的參數數量都一樣，且回傳值型別一樣，那應該使用union type改寫成non-overloaded function [](https://aaronbos.dev/posts/function-overload-typescript)

1/25(S)

1/24(S)

1/23

1/22

1/21

1/20

1/19(S)
- 閱讀[資料庫索引 (database index) 是什麼? 如何選擇加在哪個欄位上?](https://www.notion.so/explainthisio/database-index-2cc2d1d1de188008a045c4b70e665c5c)

  - 建置index是為了讓搜尋的效率更好
    - 沒有特別設定index的狀況下，資料庫會掃過每一行，然後把符合條件的資料找出來，相對沒有效率。tree資料結構就是為了解決這個問題

  - B-tree
    - 它的每個節點比binary tree帶有比較多的鍵，雖然節點越多越佔空間，但是控制在一定數量下，不會帶來太多額外成本
    - 它減少了讀取磁碟的 I/O 所需時間，所以比起二元搜尋樹，是個讓搜尋能更快完成的資料結構

  - B+tree
    - B-tree的改良版，用於解決B-tree根據範圍搜尋的弱點
    - 在最底下的子節點外的節點都有重複出現
    - 分為內部節點 (internal nodes) 與葉節點 (leaf nodes)，內部節點只會作為指標 (pointer)，指向最終的葉節點，具體的值只會在葉節點
    - 因為內部節點通常容易快取，實際發生大量 I/O 的地方是葉節點，當這樣設計就能有效減少讀取磁碟，讓整體的速度更快

  - 為什麼不直接幫每個欄位都建index？
    - tree是一種用空間換時間的方式，且每次寫入資料也必須更新tree，如果建太多index會導致寫入變很慢

  - uuid當primary key是好主意嗎？
    - primary key本身就是一種index
    - uuid v6以下的版本因為uuid的值是隨機的hash
    - 如果拿hash當index的話，可能會導致寫入時更新tree更花時間

1/18(S)

1/17

1/16
- 閱讀[如何有效通過試用期、降低被 PIP 的風險](https://www.notion.so/explainthisio/PIP-27f2d1d1de18801b8281fd00028333f7)
  - 沒有做對的事
    - 「對的事」是指團隊、直屬主管對你的期待
    - 了解績效是如何決定的，這跟所謂的「對的事」有關
    - 在前期可跟直屬主管約談，頻率盡量做到一週能一次 ，以快速得到反饋並修正。待久了以後最好也維持三個月約談一次

  - 與團隊協作
    - 觀察在團隊中評價好的人。如果不知道誰評價好，可以直接問直屬主管，或者團隊成員
    - 先建立信任，再引入、推動新的計畫

  - 快速了解系統，並有產出 [如何快速上手程式碼庫](https://www.notion.so/explainthisio/2392d1d1de18800fb865f231313f3d9f) 
    - 不要花時間讀所有技術設計文件、source code。在選擇要讀的內容時，以最新的為主，藉此了解近期有的新設計或變動
    - 如果團隊有留下技術設計的文件（為什麼那麼設計、嘗試過但不採用的其他方案），閱讀那些文件了解設計概念後會比較好理解程式碼
    - 使用Deepwiki等AI協助理解程式碼
    - 
1/15

1/14

1/13

1/12

1/11(S)

1/10(S)

1/9
- 了解absolute、relative 移動的基準 [🖌](https://play.tailwindcss.com/vsR4F2speO) 

  https://github.com/user-attachments/assets/65e79d81-25e8-4972-ad7d-1ce77f509614

  內層的element會以外層element為基準一起移動

  https://github.com/user-attachments/assets/7c422e7b-87b3-4e12-957c-b9af4481a87d

  https://github.com/user-attachments/assets/de2309d7-0fda-4c33-a401-20b7149d0433

  如果是外層relative，內層absolute，或者反過來，都是內層的element會以外層element為基準一起移動

1/8

1/7

#### 1/6
- 了解stacking context [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Stacking_context) [📗](https://ithelp.ithome.com.tw/articles/10217945) [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#1125)
  - 元素預設會以 document flow 來排列，但當元素套用 position非static的屬性，會建立新的 stacking context，~~並跳脫document flow~~但**不一定會跳脫document flow**
    - 若脫離document flow，stacking context內的元素、屬性變動並不會觸發reflow
  - Stacking Context 是隔離的容器，子元素的 z-index 只在父容器的 stacking context 內有效
    - 同一個stacking context的元素才可立於同樣的基準點來比較z-index [🖌️](https://play.tailwindcss.com/3wHeONfZa7) [🖌️](https://codepen.io/GaryChu/pen/wvwQWjE)
  - 常見的建立stacking context的CSS
    ||position: fixed|postion: sticky|position: relative + z-index|position: absolute + z-index|opacity: 小於1|translate|flex + z-index|grid + z-index|
    |---|---|---|---|---|---|---|---|---|
    |建立stacking context|○|○|○|○|○|○|○|○|
    |跳脫document flow|○|×|×|○|×|×|×|×|

1/5
- 簡單了解Playwright Test Agents [📗](https://playwright.dev/docs/test-agents)
  - 整套由planner agent、generator agent、healer agent組成
  - 步驟
    - 執行`npx playwright init-agents --loop=vscode`
    - 如果有每個測試前都要做的動作，可以寫到seed test。這份檔案也會被AI當作撰寫測試的範本
    - 告訴planner agent，規格、商業需求，已取得已mark down撰寫的test plan
    - 要求generator agent參照test plan生成test case
    - 要求healer agent執行測試，並一直修復到所有測試都可以成功執行。這個很耗token，如果想減少token消耗勢必要人力介入
- 簡單了解Playwright BDD [📗]((https://vitalets.github.io/playwright-bdd/#/writing-features/chatgpt)
  - 步驟 [📗](https://www.youtube.com/watch?v=xVIk_X3H7rM&list=PLf8vT0W16iNP7PVpW1lXuUNFmTBjAGm4V) 
    - 新增`playwright.config.js`
    - 自行撰寫，或者請AI幫以Gherkin style撰寫step (Given / When / Then 的語意化結構)
    - `bddgen export`取得一份簡單的測項描述
    - 把上個步驟地到的文字加上prompt丟給AI，並把AI生成的內容貼到feature file [📗](https://vitalets.github.io/playwright-bdd/#/writing-features/chatgpt)
      在`playwright.config.js`，定義BDD config，並把feature file、step file的路徑貼到config內
    - `npx bddgen`讓AI產出test case
    - `npx playwright test`執行測試
  - feature file跟step file並雖然描述的內容會一樣，但並沒有固定誰是源頭。前者是給一般人看得，後者是給工程師、AI看的
 
1/4(S)

1/3(S)

1/2

- 了解Golang的receiver [📙](https://go.dev/ref/spec#Receiver) 
  - receiver是綁定function到特定type成為其method的一個參數，分為value receiver、pointer receiver [📙](https://go.dev/tour/methods/4)
  - Go的function和method的差別在於是否有receiver。method有reciever，function則沒有
  - receiver的型別稱為base type。不可以是interface或pointer，且必須定義在與method同個package中
  - Struct底下不能直接定義func，若需要的話通常會搭配receiver，或者直接定義成interface [📙](https://matthung0807.blogspot.com/2021/06/go-what-is-receiver.html)

1/1


