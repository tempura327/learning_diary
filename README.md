9/22

9/21(S)

9/20(S)

9/19

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

6/30

6/29(S)
- 了解Go的變數宣告 [📙](https://go.dev/tour/basics/10)
  - 在function之外，每個statement 都要以keyword 開頭，所以short variable declaration不能用於 function 外

6/28(S)

6/27
- 了解CSS新功能 [📗](https://medium.com/@onix_react/new-css-features-you-should-know-958ed1d34464)
  - 將component id 傳給@scope()可以限制樣式生效的scope
  - `@scope()`跟CSS module一樣，可以`避免樣式衝突`，但是由於是瀏覽器原生支援，所以效能會更好
  - @support()可以用來檢查瀏覽器是否支援某個CSS功能，如果支援的話再套用某個自定義樣式
  - `@support()`可以解決使用者瀏覽器較舊，而不支援某個樣式的問題，因為可以透過這個方式`設置樣式的fallback`
- 了解可以優化效能的CSS [📗](https://medium.com/@onix_react/new-css-features-you-should-know-958ed1d34464)
  - `content-visibility`可以讓瀏覽器能夠跳過element的render，直到需要該element時才render，從而顯著`提升`大型或複雜佈局的載入和`渲染效能`

6/26
- 了解Go的function如何定義
- 了解Go的具名回傳、多重回傳 [📙](https://go.dev/tour/basics/7)
  - 多重回傳要自己宣告變數
    ```go
    func swap(x, y string) (string, string) {
        z := x + " " + y
        w := "Good morning " + x
	
        return z, w
    }

    func main() {
        a := swap("hello", "world")
	
        fmt.Println(a)
    }
    ```
  
  - 具名回傳只有在export變數的function具名，使用時仍然是用順序在取值
    ```go
    func split(sum int) (y,x int) {
       // 具名回傳的話，Go 會自動宣告好x和y，所以只要用=賦值，不必用:=宣告
       x = sum * 4 / 9
       y = sum - x
       return
    }

    func main() {
       a, b := split(17)
       fmt.Println(b, a) // 7 10
       fmt.Println(a, b) // 10 7
    }
    ```
  
- 了解Go的變數宣告

| Go 寫法       | JS 對照概念          | 說明                  |
| ----------- | ---------------- | ------------------- |
| `var x int` | `let x;`         | 宣告但不一定馬上賦值，型別要指定    |
| `x := 123`  | `const x = 123;` | 自動根據值推斷型別並賦值（限於block內） |


6/25
- 試著import pkg.go.dev上的套件、local module並使用 [📙](https://go.dev/doc/tutorial/create-module) [📙](https://go.dev/doc/tutorial/call-module-code)
  - 一個 .go 檔內只能有一個`package main`，因為每個 .go 檔案只能屬於一個套件
  - 同一個資料夾下的 .go 檔，都必須是同一個 package
  - 只有 `package main` 是整個程式的entry，因此只有`package main` 才能被 `go run` 或 `go build`
- 讀Because of Winn-Dixie ~chapter 22 學英文
  - crepe paper (皺紋紙)
  - shimmery (金蔥狀的閃亮)

6/24
- 安裝Go，並用Go寫一個Hello world [📙](https://go.dev/doc/tutorial/getting-started)

| Go       | Node.js             |
| -------- | ------------------- |
| `go.mod` | `package.json`      |
| `go.sum` | `package-lock.json` |
| `go mod init` | `npm init` |
| `go mod tidy` | `npm i && npm prune` |


6/23
- 了解CSS if() [📗](https://www.amitmerchant.com/the-if-function-in-css/)
  - 使用if()可以達到條件判斷元素應該顯示的樣式，配合CSS變數、attr()使用的話會更好用
- 了解data attribute
  - data attribute是 HTML5 規範專門設計來讓你儲存「與呈現無關的自定資料」用的屬性
  - 可以拿它來做JS條件判斷，或CSS的條件判斷、選擇器
    ![截圖 2025-06-23 下午6 11 52](https://github.com/user-attachments/assets/1cc7e1e1-ae28-49f0-a820-5d2532a054b9)

  - 可拿來存組件的內部狀態
    <video src="https://github.com/user-attachments/assets/8614655d-aa9d-4b36-88a7-60af16d492c9" />
    
  - 格式為data-<英文字母>
      - 英文字母必須是小寫
      - 不能用xml開頭
      - 因為data attribute的名稱會被從kabeb case 轉為camel case，然後存到HTMLElement.dataset，所以不能包含大寫字母、「;」
        ```html
          <div id="myDiv" data-user-id="123" data-user-name="Alice"></div>
        ```    

        ```js
          const div = document.getElementById('myDiv');
          console.log(div.dataset.userId);   // "123"
          console.log(div.dataset.userName); // "Alice"
         ```           
- 了解CSS attr()[📗](https://www.amitmerchant.com/attr-function-types-css/)
  - 使用attr()可以取得HTML上的data atrribute的值，預設型別會是string
  - 透過type<型別名>可以定義取得的值的型別

6/22(S)

6/21(S)

6/20 🚲
- 讀Because of Winn-Dixie ~chapter 16 學英文
 - nothing more than
 - steal a look at

6/19 🚲
- 做side project

6/18 🚲
- 讀Because of Winn-Dixie ~chapter 14 學英文
  - ghost (不好的回憶)
  - for all you are worth

6/17
- 做side project

6/16
- 讀Because of Winn-Dixie ~chapter 12 學英文
 - I was to...
- 做side project

6/15(S)
- 讀Because of Winn-Dixie ~chapter 11 學英文

6/14(S)

6/13
- 做side project

6/12
- 讀Because of Winn-Dixie ~chapter 8 學英文
  - You bet.
  - I don't think I can.

6/11 🚲
- 讀Because of Winn-Dixie ~chapter 7 學英文
  - someone would most certainly…

6/10 🚲
- 讀Because of Winn-Dixie ~chapter 5 學英文
 - someone has a talent for something.

6/9
- 讀Because of Winn-Dixie ~chapter 3 學英文
 - I could tell that...
 - You know what?...
 - It's hard for me to think about...
 - I love something with all my heart.

6/8(S)

6/7(S)
- 了解為什麼需要mock [📗](https://www.youtube.com/watch?v=-VOfK5-FScI)

6/6 🚲
- 了解TS、vitest報錯"Cannot find module"的原因、解法 [📗](https://vitest.dev/guide/common-errors.html#cannot-find-module-relative-path)
  ```json
    // 告訴TS"@"代表相對於ts.config.json的哪個相對路徑
    // 沒設定的話TS會報錯"Cannot find module '@/components/Counter' or its corresponding type declarations."
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  ```

  ```js
  import { defineConfig } from 'vitest/config';
  import { resolve } from 'path';

  // https://vite.dev/config/
  export default defineConfig({
    // 已經透過vite.config.ts的resolve.alias自行告訴vite "@"代表的是哪個絕對路徑，所以不用安裝vite-tsconfig-paths
    // 沒設定的話執行，也沒安裝vite-tsconfig-paths的話，vitest會報錯"Failed to resolve import "@/components/<file name>" from "test/<file name>.test.tsx"."
    resolve: {
      alias: {
        // 務必要定義成絕對路徑
        '@': resolve(__dirname, './src'),
      },
    },
  });
  ```

6/5 🚲
- 初步了解vitest的mock功能[📗](https://vitest.dev/guide/mocking.html)
  - mock是指在編寫測試時，建立內部或外部package的假版本
  - 使用vitest提供的vi可以簡單地mock function、全域變數、第三方library、timer
  - mock function分為spy和mock
    - spy用於想知道某個function 是否被呼叫時
    - mock則是真的產生一個假的function
  - mock timer是而用於縮短測試的等待時間

6/4 🚲
- 初步了解vitest的snapshot功能 [📗](https://vitest.dev/guide/snapshot.html)
  - snapshot會將某個test的結果儲存為snapshot file，並在之後的測試中自動與之前的snapshot進行比較
    - 除了一般的檔案，也可以做成圖檔的snapshot
  - 何時使用snapshot
    - 測試大型資料結構或複雜輸出時(e.g.:整陀HTML或JSX)
    - 日後可以透過git history中的snapshot `查看產品UI、需求變動的歷史`
    - `常改動HTML 結構`的專案確認改動後排版是否看起來一樣，還是有細部的差異

6/3 🚲
- 了解vitest cli的test filtering功能 [📗](https://vitest.dev/guide/filtering.html)
  - 在`vitest`後面打上字串就會只執行檔名包含該字串的test 
  - 在`vitest`後面使用 -t 或 --testNamePattern在打上字串就會只執行特定名稱的test case
- 了解如何在mono repo幫不同類型、workspace的測試做設定 [📗](https://vitest.dev/guide/projects.html#configuration)
  - 不同類的test可以透過test.projects.extends來簡單設定
  - 不同workspace的test則可以建立共用的base config，再透過mergeConfig來達到extend的效果
    ```js
        // vitest.shared.js
        import { defineConfig } from 'vitest/config';
        import react from '@vitejs/plugin-react';

        export const baseConfig = defineConfig({
          plugins: [react()],
        })
    ```

    ```js
        import { defineConfig, mergeConfig } from 'vitest/config';
        import tailwindcss from 'tailwindcss';
        import { baseConfig } from '../../vitest.shared.js';
        import { resolve } from 'path';

        export default mergeConfig(baseConfig, defineConfig({
          plugins: [tailwindcss()],
          resolve: {
            alias: {
              '@': resolve(__dirname, './src'),
            },
          },
        }))
   ```

6/2
- 初步了解vitest
  - 在vite.config.js內設定test即可
    - 如果以TS撰寫unit test需要設定TS reference
      ```js
      // vite 2只要在vite.config.js內加入以下內容
      <reference types="vitest" />

      // vite >=3 則是修改tsconfig.json
      include: ['放測試檔案的資料夾路徑']
      ```
    - 如果vite.config.js中部分的設定只想讓跑unit test時才生效，可以透過`env.mode === 'test'`來判斷
  - 支援TS，不像Jest一樣需要設定Babel來轉譯TS才能執行unit test
  - 可以把unit test寫在跟組件同個檔案內
  - 當source code或unit test改變時，vite會自動重跑跟改動部分有關的unit test，以及和該unit test有關的unit test
 

6/1 🚲

5/30

5/29

5/28
- 看完[React Vite Testing Tutorial For Beginners - Vitest Testing Crash Course](https://www.youtube.com/watch?v=CxSL0knFxAs)
  - 作者建議儘量把UI和邏輯拆開，因為這樣既可以測`使用者進行互動時，UI的改變`，也可以`測邏輯`

5/27
- 看[React Vite Testing Tutorial For Beginners - Vitest Testing Crash Course](https://www.youtube.com/watch?v=CxSL0knFxAs) ~19:00

5/26
- 了解component test的核心概念 [📗](https://www.youtube.com/watch?v=OIpfWTThrK8)
  - component test的核心為「把待測物當成黑盒子，專注於測試interface」。只要interface維持一致，都能保證測試正常運行，才不會讓測試本身變得過於脆弱、難以維護
    - 只測試component的contract，而不測試元件內部的私有屬性和邏輯(實作)
    - component的contract通常指template、props、event等對外公開的interface
	![螢幕擷取畫面 2025-05-26 211452](https://github.com/user-attachments/assets/2990b5a5-254e-4918-99d3-065949d298a2)

  - component test可以分為2種
    <br/>
    <img src="https://github.com/user-attachments/assets/6138bf90-a0f6-4bfe-8061-569d4785767e" width="45%" />
    <img src="https://github.com/user-attachments/assets/e1e94f5c-7fa3-4218-b2b0-2025c25ee650" width="45%" />

    - integration test，把整個component當成一個黑盒子，包含其所有children component的行為與結果都是這個元件應該負責的部分
    - shallow test，只關心最外層component的行為與它直接使用的child component。如果某個行為來自於更深層的sub component，它就不是這個元件負責的範圍，所以測試時不會去理會它
	![螢幕擷取畫面 2025-05-26 211225](https://github.com/user-attachments/assets/c401b489-f070-4660-ae76-528576478d82)

5/25(S)
- 初步了解Vitest [📗](https://www.youtube.com/watch?v=5ddeTxyfgcE)
  - 不用額外設定Babel，就可以使用TS寫test
  - 當你修改測試檔並存檔時，它會幫你自動跑跟該測試，以及有關的所有測試，而不是像Jest會重跑所有測試
  - test suite可以直接寫在component同個檔案內

5/24(S)

5/23

5/22
- 了解MongoDB的aggregation [📗](https://www.mongodb.com/zh-cn/docs/manual/aggregation/)
  - aggregation處理多個document並傳回計算結果，可用於以下場景
    - 對分組資料執行操作，傳回單一結果
    - 將多個documnet中的值組合在一起
  - pipeline是由一個或多個處理document的stage組成，每個stage的output會被傳給下個stage
  - 常見的stage
    |stage|功能|SQL對應keyword|
    |---|---|---|
    |$match|篩選資料|WHERE|
    |$group|分組 + 統計運算|GROUP BY|
    |$project|控制回傳值顯示的欄位|SELECT|
    |$limit|控制回傳的筆數，常用搭配$skip使用|LIMIT|
    |$skip|跳過跳過前n個document，常用搭配$limit使用|OFFSET|
    |$sort|排序|ORDER BY|
- 了解[$match](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/match/)

5/21
- 閱讀[[Day 29] 一次弄懂 React hooks 的運作原理與設計思維（下）](https://ithelp.ithome.com.tw/articles/10308689)
  - 在 class component 的時代，有許多社群提出的 patterns 來`處理在component之間重用邏輯的問題`，主流的像是 higher order component 以及 render props
  - hook的出現是為了以更方便的方式解決上述問題，它讓 function component 能擁有狀態，且每次 render 夠不互相干擾
  - React用fiber node內的memorizeState來一層一層紀錄state是為了避免命名問題衝突
- 閱讀[[Day 30] 一次打破 React 常見的的學習門檻與觀念誤解：系列文總結以及完賽感言](https://ithelp.ithome.com.tw/articles/10308940)

5/20

5/19
- 閱讀[[Day 28] 一次弄懂 React hooks 的運作原理與設計思維（上）](https://ithelp.ithome.com.tw/articles/10308283)
  - component 在被呼叫時會產生一個對應的「狀態管理節點」，即 fiber node
  - 當reconciliation的流程開始時，reconciler 就會做以下幾件事
    1. 調度 component 的 render ，並將資料的改動更新到 fiber nodes 裡
    2. 將該次 render 出來的 新的 Virtual DOM Tree， 與前一次的進行比較，並將有差異的部分移交 renderer 處理真實的 DOM 更新
  - hook只能在component 的頂層調用，而不可以在條件式或迴圈裡調用，因為React用fiber node內的memorizeState來一層一層紀錄state的下一個順序的state是什麼(即其他文章常提到的用一個queue把state裝起來)，所以如果在條件式呼叫hook，就會導致state的紀錄不會對齊而出錯


5/18(S)
- 讀完[[Day 27] useCallback 與 useMemo 的正確使用時機](https://ithelp.ithome.com.tw/articles/10308018)

5/17(S)
- 閱讀[[Day 27] useCallback 與 useMemo 的正確使用時機](https://ithelp.ithome.com.tw/articles/10308018) ~useCallback

5/16

5/15
- 閱讀[[Day 26] Effects & cleanups 常見情境的設計技巧](https://ithelp.ithome.com.tw/articles/10307558)
  - 常見的 effects 設計問題
    - race condition
    - memory leak
  - 在effect內執行非同步動作，並使用其回傳的值時，如果沒有設置cleanup、宣告變數當作flag，不然可能第一次的response比較晚回來導致使用到舊的response的資料
    - ReactQuery之類的第三方套件已經幫忙處理掉了，也可以使用它 
  - 在effect內持續性的監聽，但是沒有設置cleanup來取消監聽的話，就可能在 component unmount 之後仍持續監聽，導致 memory leak
    - setTimeout、setInterval
    - 綁定event handler
      ```js
      window.addEventListener('scroll', () => {})
      ```
  - 在effect內不斷new instance也會浪費記憶體，所以最好把initialize 的code放到React 頂層 App component，以確保在整個網頁只會執行一次 

5/14
- 閱讀[[Day 25] Reusable state — React 18 的 useEffect 在 mount 時為何會執行兩次？](https://ithelp.ithome.com.tw/articles/10307083)
  - React 在 18 的 Strict mode 中添加了這個模擬「mount ⇒ unmount ⇒ mount」流程的行為。這是為了模擬多次 mount 的動作，來幫助開發者檢查 component 中的 effect 設計是否滿足這個彈性的要求

5/13
- 了解Leetcode 46. Permutations解法 [📗](https://blog.csdn.net/chencl1986/article/details/109293303) [📗](https://bclin.tw/2022/06/25/leetcode-46/)
  ```js
    const recursion = (nums: number[], res: number[][], permutation: number[], used:boolean[]) => {
        if(permutation.length === nums.length){
            res.push(permutation.slice());
            return;
        }
    
        for(let i = 0; i < nums.length; i++){
            if(used[i]){
                continue;
            }
    
            used[i] = true;
            permutation.push(nums[i]);
            
            recursion(nums, res, permutation, used);
    
            used[i] = false;
    
            permutation.pop();
        }
    }
    
    const permute = (nums: number[]) => {
        const res: number[][] = [];
        const permutation: number[] = [];
        const used = new Array(nums.length).fill(false);
    
        recursion(nums, res, permutation, used);
    
        return res;
    }
  ```

5/12
- 閱讀[[Day 24] useEffect dependencies 的經典錯誤用法](https://ithelp.ithome.com.tw/articles/10306703)
  - 誠實填寫dependencies。不然未來React官方如果改變了useEffect的實作，讓useEffect適度忘記dependencies的值，就可能會導致意想不到的錯誤
  - 當「y需要在x變動時+1」這類的情況發生時，可以用useRef記住x前一次的值，並和x當下的值比較，來判斷要不要幫y+1。而不是直接拿x當dependencies
  ```js
  // bad
  useEffect(() => {
    y += 1;
  }, [x])

  // good
  useEffect(() => {
    if (xRef.current !== x) {
      yRef.current += 1;
    }
    xRef.current = x;
  }, [x])
  ```

5/11(S)
- 閱讀[[Day 23] 保持資料流 — 不要欺騙 hooks 的 dependencies（下）](https://ithelp.ithome.com.tw/articles/10306185)
  - 除了使用useCallback把function包住來優化效能以外，也可以視情況把function直接宣告在useEffect內，或者宣告在component外

5/10(S)

5/9
- 閱讀[[Day 22] 保持資料流 — 不要欺騙 hooks 的 dependencies（上）](https://ithelp.ithome.com.tw/articles/10305701)

5/8
- 閱讀[[Day 21] useEffect 其實不是 function component 的生命週期 API](https://ithelp.ithome.com.tw/articles/10305220)
  - useEffect 的用途是「將原始資料同步到畫面以外的副作用」，而不是lifecycle hook
  - 在設計 effect 內的邏輯時，不應該考慮「這個 effect 會在哪幾次 render 時被執行」，而是即使每一次 render 時都執行這個 effect，其邏輯依然能正常運作。因為重點不是哪些 render 會執行這個 effect，而是這個 effect 最後的執行結果能夠「完整的同步」資料的變化就好
  - hooks 的 `dependencies 只是一種效能最佳化`，而非執行時機的保證。在未來 React 有可能會在某些時刻「忘記」dependencies 的舊值來釋放記憶體，因此如果拿dependencies當作執行時機的條件，可能會導致 effect 中的邏輯在非預期的情況下被執行

5/7

5/6
- 閱讀[[Day 20] 每一次 render 都有自己的 effects](https://ithelp.ithome.com.tw/articles/10304650)
  - React 用的是「整個框架本體是一個閉包」的設計，來記憶每個 component 的 hook 狀態
    - React用「閉包 + 指針」的設計來讓hook可以記憶狀態，也因此set function才能取得前一次的state值 (ex: setState((prev)=> prev + 1))
    - component 本身不是閉包，反而是 stateless 的 pure function
  - 由於閉包的特性，function所記得的props、state會是當次 render 時的狀態

- 閱讀[為什麼只能在最頂端層呼叫 Hook？從 useState 實作原理來回答](https://www.explainthis.io/zh-hant/swe/why-call-react-hook-top-level)
  - React 用的是「呼叫順序(index)」配對 hook，所以呼叫順序一亂，整個 state 就會亂掉，因此hook才只能在top-level呼叫

5/5
- 閱讀 [Scroll progress animations in CSS
](https://developer.mozilla.org/en-US/blog/scroll-progress-animations-in-css/)
- 了解更多Scroll-driven Animations的實際使用場景 [📗](https://medium.com/@aaabear320/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC%E7%AD%86%E8%A8%98-scroll-driven-animations-8b68242ad300)


5/4(S)
- 閱讀[[Day 18] Function component & class component 你可能不知道的關鍵區別](https://ithelp.ithome.com.tw/articles/10303533)
   - 在class component透過this.props取得props的值的話，由於this是mutable的，所以會拿到最新的結果，而不是某一個frame呼叫function時的props的值
   - class component 每次 re-render，React 會將新版的整包 props 以 mutate 的方式覆蓋進 this 當中取代舊版的 props，所以說this是 mutable
- [What is ‘this’ in React?](https://medium.com/byte-sized-react/what-is-this-in-react-25c62c31480)
- [[Day 19] 每一次 render 都有自己的 props、state 以及 event handlers](https://ithelp.ithome.com.tw/articles/10304009)
  - 在每一次的 render 之間的 props, state, event handlers 都是獨立、不互相影響的
  - 這也是為什麼當 state 中有物件型別值時，需要去保證資料是 immutable 的原因。當事件的處理中會使用到舊 render 中的資料時，這樣才能維持每一次 render 當中的 state 都保持獨立不互相影響
    
5/3(S)
- 閱讀[[Day 17] Immutable update 的 nested reference clone 誤解](https://ithelp.ithome.com.tw/articles/10303033)

5/2
- 了解TS的any和unknown [📗](https://medium.com/@s.chandrakethan9/this-is-how-much-typescript-you-need-to-know-as-a-react-developer-74947fc130a0)
  - any代表可以是任何型別，unknown則是我不知道型別
  - unknown的type check會更嚴格，不把type narrow down的話會報錯
  ```js
    const foo = (str: any) => {
      console.log(str[0]);
    }

    const bar = (str: unknown) => {
      // 'str' is of type 'unknown'.
      console.log(str[0]);
    }
  ```
- 了解TS的void、never差異 [📗](https://mariusschulz.com/blog/the-never-type-in-typescript)
  - function的回傳值若是void代表沒有回傳值，`never則代表永遠不會抵達執行的終點`(have no reachable end)
  ```js
    // void
    const foo = (str:string) => {
      console.log(str);
    }

    const foo2 = (str:string) => {
      const isOk = true;

      do{
        console.log(str);
      }while(isOk);
    }

    // never    
    const bar = (str:string)=> {
      throw new Error(str);
    }

    const bar2 = (str:string) => {
      do{
        console.log(str);
      }while(true)
    }
  ```
  - 用於變數時，never則代表沒有可能的型別(impossible type)
  ```js
    const foo = (value: string) => {
      if (typeof value === 'string') {
        console.log(value); // Type string
      } else {
        console.log(value); // Type never
      }
    }
  ```

  ```js
  const foo: any = 123;

  // Type '123' is not assignable to type 'never'
  const bar: never = 123;
  ```

5/1
- 了解[flex-basis](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-basis)
  - flex-basis 指定 flex 元素在主軸方向的預設大小 (但用 box-sizing 改變盒模型的話就除外)
    - 當flex-direction: row 時(預設)，主軸為x軸，對應的屬性是width
    - 當flex-direction: column 時，主軸為y軸，對應的屬性是height
    - 優先權: min-width = max-width > flex-basis(flex-basis: auto 除外) > width > content
  - 如果父層有設置flex，若子元素A設置width，當父層的width不夠時，所有需要shrink的width都會套到子元素A，所以子元素A會被擠壓變小
    - 幫子元素A設置`min-width`，可解決透過優先級解決這個問題 [✏️](https://codesandbox.io/p/devbox/try-new-css-property-tfrf9g?file=%2Fsrc%2Fpages%2FFlexBasis.vue%3A57%2C9)
    - 幫子元素A設置`flex-shrink: 0 !important`，強迫元素A不縮小也可解決這個問題








