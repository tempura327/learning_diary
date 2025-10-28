

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

4/30

4/29

4/28

- 閱讀[[Day 15] 維持 React 資料流可靠性的核心關鍵：Immutable state](https://ithelp.ithome.com.tw/articles/10301603)
  - React 會純粹用 Object.is() 去判斷reference是否相同來斷定資料是否改變，
    ```js
    // 如果傳遞內容完全一樣，但reference不同的物件，React必會re-render

    const [data, setData] = useState({ name: 'Tempura' });

    return (
        <div>
            <h1>{data.name}</h1>

            {/* 按了會重渲染 */}
            <button onClick={() => {setData({ name: 'Tempura' })}}>
                set name to Tempura
            </button>

            {/* 按了會不會重渲染 */}
            <button onClick={() => {
                setData(data);
            }}>
                set name to same Tempura
            </button>
            <button onClick={() => {
                data.name = 'Jasmine';
                setData(data);
            }}>
                set name to same Jasmine
            </button>
        </div>
    )
    ```
- 閱讀[[Day 16] Immutable update 物件與陣列的基本功](https://ithelp.ithome.com.tw/articles/10302252)

4/27(S)

4/26(S)

4/25
- 練習類Leetcode 8. Second Largest Element in an Array
    ```js
    const findSecondBiggestNum = (arr:number[]): number => {
        let biggestNum = 0;
        let res = 0;

        for(let i = 0; i < arr.length; i++){
            if(arr[i] > biggestNum){
                res = biggestNum;
                biggestNum = arr[i];

            }else if(arr[i] < biggestNum && arr[i] > res){
                res = arr[i];
            }
        }

        return res;
    }

    console.log(findSecondBiggestNum([1, 3, 4, 5, 0, 2])) //4
    console.log(findSecondBiggestNum([1, 0, -1, -2])) // 0
    console.log(findSecondBiggestNum([20, 20, 10, 8, 20])) // 10
    ```

4/24

4/23
- 練習Leetcode 3. Longest Substring Without Repeating Characters
  ```js
    function lengthOfLongestSubstring(s: string): number {
        let n = 0;
        let arr = [];
    
        for(let i = 0; i < s.length; i++) {
            const targetIndex = arr.findIndex((ele)=> ele === s[i]);

  	    // 目前指到的字符已存在於arr，其index為targetIndex，所以要把arr從頭到targetIndex砍掉
  	    // 砍掉前要記錄目前的長度
            if(targetIndex > -1){
                n = Math.max(arr.length, n);
    
                arr = [...arr.slice(targetIndex+1, arr.length)];
            }
    
            arr.push(s[i]);
        }

  	// 比較最後的arr長度跟最後一次砍掉重複部分時紀錄的長度，較大的就是字串s中不重複的最長長度
        return Math.max(arr.length, n);
    };
  ```

4/22
- 閱讀[[Day 14] 以 functional updater 來呼叫 setState](https://ithelp.ithome.com.tw/articles/10300743)
- 練習Leetcode 20. Valid Parentheses
    ```js
    const map = {
        '(' :')',
        '{' :'}',
        '[' :']',
    };

    const keys = Object.keys(map);

    function isValid(s: string): boolean {
        const stringLength = s.length;

        if(stringLength % 2 === 1){
            return false;
        }

        const arr = [];

        for(let i = 0; i < stringLength; i++){
            const isLeftPart = keys.includes(s[i]);

    	    // 如果是左括弧，就無腦push
            if(isLeftPart){
                arr.push(s[i]);
                continue;
            }

	    // 如果目前指到的符號等於「arr內最後一個符號對應的右括弧」，就把arr內最後一個符號(跟他一對的左括弧)從arr踢出
            if(s[i] === map[arr[arr.length - 1]]){
                arr.pop();
                continue;
            }

	    // 如果目前指到的符號不是左括弧，且也不等於「arr內最後一個符號對應的右括弧」，那就代表出現不成對的狀況了，直接return false
            return false;
        }

	// 如果迴圈跑完後arr為空，代表所有符號皆成對
        return arr.length === 0;
    };
    ```

4/21
- 閱讀[[Day 12] 如何在子 component 裡觸發更新父 component 的資料](https://ithelp.ithome.com.tw/articles/10299348)
  - 當component的state的setState作為props傳給其子component A後，若在子component A內呼叫setState，該 state 原本所屬的 component 會被 re-render，進而使得底下的所有子component A、B、C都re-render (產生新的virtual DOM)
- 閱讀 [[Day 13] 深入理解 batch update](https://ithelp.ithome.com.tw/articles/10300091) [🔖](https://github.com/tempura327/learning-diary/blob/master/2024/README.md#1218) [🔖](https://github.com/tempura327/learning-diary/blob/master/2024/README.md#1227)
  - 即使不同 state 的 setState 交叉連續呼叫也會支援自動 batching
  - React 18 之前的版本，batch update 其實只會在同步事件中才會自動支援。如果在同步事件中去多次呼叫 setState 的話，仍會多次觸發 re-render

4/20(S)

4/19(S)
- 閱讀 [軟體工程師的修煉與成長 (5) — 1:1該談什麼才能讓職涯起飛](https://readwise.io/reader/shared/01gsa0ypxcayenh9pm5zv9j8hx/)
  - 直球對決問對方對自己的回饋、想前往下一個職級的需要做的事、想做某些事，請對方幫忙注意機會
  - 主管的好壞在於他們對於幫助團隊裡每個人的職涯成長有多用心

4/18
- 閱讀 [What’s new in React 19](https://react.dev/blog/2024/12/05/react-19)
  - React 19的`action`指的是`處理非同步的動作的function`
  - 更簡單的管理call api的狀態
    - useTransition
      - 回傳的第一個值是代表pending狀態，第二個值是接受async callback的function
    - useActionState
      - 直接接受一個async callback，回傳error、pending狀態、action function
      - 前身是react dom的useFormState
    - optimisticName
      - 樂觀更新結果到UI，失敗時也會自動rollback
  - 簡單讀取promise resolve的值、context值
    - use
  - server component
    - 在server上執行，所以只有SSR可以用
    - 用於先在server上把資料撈出來放進HTML讓使用者可以快速看到第一幕，類似pre-render
    - 因為在server上執行，所以沒有辦法像瀏覽器執行JS，也就不能做一些互動效果、state管理
  - component內可以放meta tag (ex: title, meta, link)
    - 以後可以不使用react-helmet的Helmet包裹meta tag，或者用自己用JS插入title到head tag了

4/17
- 了解如何在TS+React+Vite的專案設置alias [📗](https://notes.boshkuo.com/docs/Vite/vite-problem2)
```
pnpm path
pnpm i @types/node -D
```

```
// tsconfig.app.json加上

compilerOptions: {
  // …略

  /* Path Aliases */
  "baseUrl": ".",
    "paths": {
   “@/*”: ["src/*"]
  }
}
```

```js
// vite.config.ts改alias路徑

resolve: {
  alias: {
    '@: path.resolve('./src'),
  }
}
```

4/16

4/15

4/14

4/13(S)

4/12(S)

4/11
- 初步了解pnpm，以及其運作方式 [📗](https://www.youtube.com/watch?v=DKulVqlQYa8)

4/10
- 閱讀[[Day 11] React 畫面更新的核心機制（下）：Reconciliation](https://ithelp.ithome.com.tw/articles/10298053)
  - 當呼叫 setState 後，React 會先以 Object.is() 來檢查新傳入的 state 是否與舊的不同，如果相同的畫面不用更新，反之則產生新的Virtual DOM Tree，用於比較、更新畫面
    - 基本型別的值，Object.is()判斷值是否相同的，是的話則為true
    - 物件型別的值，Object.is()判斷reference是否相同的，是的話則為true
  - 「將新產生的 Virtual DOM Tree 並與舊的進行比較，再更新DOM Tree」的流程，在 React 中被稱為 Reconciliation
  - state 所屬的父組件進行 re-render，會引起其子組件re-render，並傳入新的 props

4/9
- 閱讀[[Day 10] React 畫面更新的核心機制（上）：一律重繪渲染策略](https://ithelp.ithome.com.tw/articles/10298007)
  - 在 React 中在講「渲染」，通常都是指 Virtual DOM elements（React elements）的產生
  - React 以 Virtual DOM 來進行一律重繪，React會比較新舊 Virtual DOM，然後只更新有變化的部分對應的DOM
    - 使用Virtual DOM重繪的策略可以避免掉DOM重繪帶來的巨大效能衝擊
  - Virtual DOM的重繪範圍是以component為單位。當呼叫setState時，React只會重繪該 state 所屬的 component 以及其後裔component

4/8
- 閱讀[[Day 08] JSX 的重要特性與規則以及其背後緣由](https://ithelp.ithome.com.tw/articles/10296741)
  - 一段 JSX 就是呼叫一次 React.createElement()，所以JSX 的第一層只能有一個節點
  - transpiler (ex: Babel) 無法直接在 JSX 裡以標籤的語法定義來分辨tag name是想表達字串內容還是一個函式名稱(function component)，所以會用tag name首字母大小寫來判斷
 
  ```js
     // 首字小寫，判斷是一個對應真實 DOM 的 element type
     const hello = <div className="text-blue-300">hello world</div>;
     // 相當於 createElement('div', {className: 'text-blue-300'}, 'hello world');

     // 首字母大寫，判斷是一個 function component
     const helloWorld = <HelloWorld className="text-blue-300" />;
     // 相當於 createElement(HelloWorld, {className: 'text-blue-300'});
  ``` 

- 閱讀[[Day 09] 單向資料流 & DOM 渲染策略](https://ithelp.ithome.com.tw/articles/10296750)
  - 單向資料流的核心概念是「畫面是資料延伸的結果」，且這個過程是單向且不可逆的
    - Vue雖然是雙向綁定，但也是單向資料流
  - 在真正的產品中實作單向資料流的時候，會面開發上的臨心智負擔、效能衝擊兩種問題，但使用前端框架就可以避掉兩個問題

4/7
- 閱讀[[Day 06] Render React elements](https://ithelp.ithome.com.tw/articles/10295277)
  - reconciler
    - 管理、產生virtual DOM tree
    - 負責產生新的 Virtual DOM Tree，再比較新舊Virtual DOM Tree比較，並將兩者差異告知 Renderer
    - 以上步驟稱 Reconciliation
  - renderer
    - 將 reconciler 所產生virtual DOM Tree，在目標環境（ex: 瀏覽器）中轉換並產生對應DOM Tree
    - 用於瀏覽器環境的 React renderer 為 react-dom 
    ```js
      import ReactDOM from 'react-dom/client';
      // 使用.render()可以呼叫renderer產生DOM
      ReactDOM.createRoot(document.getElementById('root')!).render(
        <React.StrictMode>
          <Root />
        </React.StrictMode>,
      );
    ```  
    - 不建議去`手動操作 DOM element`，因為這有可能`會導致 Virtual DOM Tree 與對應的真實的 DOM Tree 不一致`，進而引發一些意外的問題

- 閱讀[[Day 07] JSX 根本就不是在 JavaScript 中寫 HTML](https://ithelp.ithome.com.tw/articles/10296066)
  - React使用Babel定義如何將JSX轉換成React.createElement()，所以JSX才能順利在瀏覽器上被變成virtual DOM，再產生出DOM

4/6(S)
- 閱讀[[Day 05] 建構一切 UI 的最基本單位 — React element](https://ithelp.ithome.com.tw/articles/10294538)
  - ReactElement是一種type為object的資料，用於描述DOM element。它也是 virtual DOM 的一部分，相當於virtual DOM element
    - `ReactElement` 從概念上來說就像是在`表達「某一刻當下的畫面結構」`，因此一旦被`建立之後`就永遠`不能修改`
  - ReactElement經過React轉換過後會產生對應的DOM element
  - ReactNode則是任何可以由 React 渲染的東西。ReactElement是它的子集

4/5(S)
- 閱讀[[Day 04] DOM 與 Virtual DOM](https://ithelp.ithome.com.tw/articles/10293802)
  - DOM (DOM tree)是樹狀資料結構，它和瀏覽器的畫面渲染引擎綁定，因此操作 DOM element就會連動更新畫面繪製
  - virtual DOM(virtual DOM tree)也是樹狀結構資料，它`定義整個畫面結構`，但是因為`沒跟渲染引擎綁定`，所以操作virtual DOM的成本較低

4/4

4/3
- 了解新的CSS屬性 position: anchor + anchor-offset 屬性 [📗](https://medium.com/@arnoldgunter/69ce290ac95e)
  - 2025年4月的現在支援度還很差
  - 可以用純CSS做出tooltip的效果 [✏️](https://codesandbox.io/p/devbox/tfrf9g?file=%2Fsrc%2Fcomponents%2FTooltip.vue%3A3%2C5)

4/2
- 讀完[How React Compiler Performs on Real Code](https://adevnadia.medium.com/how-react-compiler-performs-on-real-code-5241110febc5#197d)
- 調查如何在mono repo使用VSCode extension [i18n-ally](https://github.com/lokalise/i18n-ally)
  - https://github.com/lokalise/i18n-ally/issues/1246
  - https://github.com/lokalise/i18n-ally/issues/997

4/1
- 了解新的CSS field-sizing: content 屬性 [📗](https://levelup.gitconnected.com/the-new-css-field-sizing-property-just-solved-one-of-the-hardest-problems-in-styling-aa6eb7352440)
  - 試用看看 [✏️](https://codesandbox.io/p/devbox/tfrf9g?file=%2Fsrc%2Fcomponents%2FTooltip.vue%3A12%2C10)
- 閱讀[How React Compiler Performs on Real Code](https://adevnadia.medium.com/how-react-compiler-performs-on-real-code-5241110febc5#197d) ~Interactions performance and React Compiler
  - 作者實測發現「用useMemo、useCallback把所有非基本型別的值包起來會更讓performance變差」並不是真的

3/31

3/30(S)
- 閱讀[How React Compiler Performs on Real Code](https://adevnadia.medium.com/how-react-compiler-performs-on-real-code-5241110febc5#197d) ~React Compiler on the real app

3/29(S)
- 閱讀[深入理解 package-lock.json 的用途與適用情境](https://blog.miniasp.com/post/2025/03/26/In-depth-understanding-of-the-purpose-and-applicable-scenarios-of-package-lockjson#google_vignette)
  - 如果package-lock.json不存在
    - 使用`npm i`會根據package.json內的套件範圍安裝範圍內的最新版，並產生package-lock.json
    - 無法使用`npm ci`
  - 如果package-lock.json存在
    - 使用`npm i`會根據 package-lock.json內的詳細版本安裝
    - 使用`npm ci`會根據 package-lock.json內的詳細版本安裝，但如果package-lock.json內的版本超過package.json內的版本還是會報錯
- 閱讀Improvements in React 19 [ref as a prop](https://react.dev/blog/2024/12/05/react-19#improvements-in-react-19)
  - React19會廢棄fowardRef，以後傳遞ref給子組件只要項一般的prop那就好
- 閱讀[How React Compiler Performs on Real Code](https://adevnadia.medium.com/how-react-compiler-performs-on-real-code-5241110febc5#197d) ~React Compiler 🚀 to the rescue
  - 變數值若非基本型別，傳給子組件的話，每次重渲染之後因為reference改變，所以就會被React判斷子組件也要重渲染
  - 使用useCallback、useMemo可以部份減緩這個問題，因為React會在遇到memoizing props時會停下re-render，先去component chain查詢值是否真的有變，真的有變才re-render
    - 但它們並不是萬能的，因為performance開銷不小，所以只有在計算邏輯複雜時才建議使用 (後續實測結果看4/1)

3/28

3/27
- 練習Leetcode 2033. Minimum Operations to Make a Uni-Value Grid
```js
function minOperations(grid: number[][], x: number): number {
  const nums = grid.flat().sort((a, b) => a - b);
  
  const isEvenLength = nums.length % 2 === 0;
  const middleIndex = Math.floor(nums.length / 2);
  // 通常讓大家往中間數(middleNumeber)移動總移動距離會最少
  const middleNumbers = nums.slice(middleIndex, middleIndex+ (isEvenLength ? 2 : 1));

  const results = middleNumbers.map((m) => {
     // 查看middleNumeber和其他的數字差多少，再除以x就是移動的次數
     // 舉例來說4和10差6，若x為2，則移動3次
    const res = nums.reduce((acc, curr) => {
      const difference = Math.abs(curr-m) / x;

      return {
        total: acc.total + difference,
        // 如果某個數字跟middleNumber差的值無法被x整除，意味著永遠沒辦法移動到那個數字
        // 只要有一個不能被整除，就可以直接return false
        isOk: acc.isOk && Number.isInteger(difference)
      }
    }, {
      total:0,
      isOk: true
    })

    return res.isOk? res.total : -1;
  })

  return Math.min(...results);
};
```

3/26
- 練習LeetCode 412. Fizz Buzz
```js
function fizzBuzz(n: number): string[] {
    const res = Array.from({length: n}, (_, i)=>{
        const num = i + 1;
        const is3Divisor = num % 3 < 1;
        const is5Divisor = num % 5 < 1;

        let str = '';

        if(is3Divisor){
            str += 'Fizz';
        }

        if(is5Divisor){
            str += 'Buzz';
        }

        return str || `${num}`;
    })

    return res;
};
```

3/25
- 了解cursor相關的CSS屬性 [📗](https://www.w3schools.com/cssref/pr_class_cursor.php)
  - ![螢幕擷取畫面 2025-03-25 215920](https://github.com/user-attachments/assets/058539a8-fe1a-468e-9d50-53e86d09e01b)
- 練習在canvas上製作resize功能 [✏️](https://codesandbox.io/p/sandbox/try-canvas-2-vz4pcm?file=%2Fsrc%2Fcomponents%2FResize.tsx%3A24%2C6-24%2C7)

3/24
- 讀MDN measureText()的內容 [📗](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/measureText)
  - text預設的baseline是alphabetic，是有點偏上的擺放。設為top，才會跟其他形狀的擺放規則一樣
  - 練習使用measureText、設置textBaseline [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FImage.tsx%3A195%2C11-195%2C23)
- 閱讀[5 個段落寫出理想 Cover Letter](https://www.cake.me/resources/write-a-cover-letter-in-5-paragraphs)

3/23(S)
- 讀MDN createPattern()的內容 [📗](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/createPattern)
  - createPattern + fillStyle可做出拼貼、切裁圖案的效果
  - 練習使用createPattern + fillStyle做拼貼、切裁圖案 [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FImage.tsx)

3/22(S)
- 讀MDN clip()切裁圖案的內容 [📗](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/clip)
  - clip()用於切裁圖案
  - 練習在canvas上畫文字、圖片、切裁圖片 [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FImage.tsx%3A53%2C29)

3/21
- 完成canvas drag練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-2-vz4pcm?file=%2Fsrc%2Fcomponents%2FDrag.tsx%3A122%2C38)

3/20
- 讀MDN的在canvas上放文字、圖 相關內容 [📗](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage)
- 讀MDN的translate、rotate 相關內容 [📗](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/translate)
  - rotate可以拿來做旋轉功能
- 繼續做canvas drag練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-2-vz4pcm?file=%2Fsrc%2Fcomponents%2FDrag.tsx%3A122%2C38)

3/19
- 看canvas 的drag and drop 教學 [📗](https://www.youtube.com/watch?v=7PYvx8u_9Sk)
  - 進行練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-2-vz4pcm?file=%2Fsrc%2Fcomponents%2FDrag.tsx%3A122%2C38)

3/18
- 讀MDN 的arcTo()、eclipse()相關內容 [📗](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/ellipse)
  - 照著做曲線、橢圓的練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FLine.tsx%3A31%2C17)

3/17
- 讀完MDN的canvas教學 Drawing shapes with canvas [📗](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)
  - 照著做line、circle練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FLine.tsx%3A31%2C17)

3/13~3/16(S)
澎湖旅遊

3/12
- 了解用JS取得上一頁網址的方法
	- document.referrer [📗](https://medium.com/@tariibaba/javascript-get-last-page-url-dc47a2ca5087)
		- document.referrer只有在點擊link時才能生效，但如果a tag上有`rel="noreferrer"`，即便是點擊連結進入網站的，其值一樣會是空字串
		```
		const lastPageUrl = document.referrer;
		```
	- 出於安全和隱私原因，window.history 允許跳轉頁面，但不允許存取session內的 URL [📗](https://stackoverflow.com/questions/3528324/how-to-get-the-previous-url-in-javascript)
		- `history.back() + return location.href`會先跳回上一頁再回傳網址不適用於只想取得上一頁網址的場景

- 讀Svelte教學 ~Basic SvelteClasses and styles [📗](https://svelte.dev/tutorial/svelte/classes)
	- 了解如何根據條件切換class、style
	```
	<button class="font-bold {isActive? 'bg-blue-300' : ''}">
		Try
	</button>

	// 官方文件沒寫，但實際試過有效
	<button class="font-bold" class:bg-blue-300={isActive}>
		Try
	</button>
	```
	- 了解如何用`:global`讓parent component內撰寫的style也能套用到child component

3/11
- 讀完MDN的canvas教學 Basic usage of canvas [📗](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage)
  - canvas的預設大小為300px × 150px，透過HTML width、height 屬性可以調整大小
    - 不要同時用HTML跟CSS調整canvas大小，當兩者比例不同時會導致canvas扭曲
  - canvas可以有有一或多個渲染環境(rendering context)，渲染環境又分為2D跟3D
  - 照著做rect練習 [✏️](https://codesandbox.io/p/sandbox/try-canvas-1-dt3338?file=%2Fsrc%2Fcomponents%2FLine.tsx%3A31%2C17)


3/10
- 學在Svelte component的props定義class的方法 [V5](https://svelte.dev/docs/svelte/$props#Renaming-props) [V4](https://stackoverflow.com/questions/75896304/add-class-to-svelte-component)
- 學在Svelte component內 export function [📗](https://svelte.dev/docs/svelte/legacy-export-let#Component-exports)

3/9(S)

3/8(S)

3/7
- 了解發生push時發生`error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400`的原因
  - 原因是push的檔案超過緩衝區大小，或者是網路訊號不好，最簡單的解法是拆開分成幾次push
  - push時 git 不會一個一個檔案即時送出，而是把多個檔案或變更合併到一個git物件，並放進緩衝區，再送到server
  - http.postBuffer是緩衝區的大小，http.postBuffer 預設值通常是 1048576  Byte (=1MB) [📗](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httppostBuffer) [📗](https://git-scm.com/docs/gitfaq#Documentation/gitfaq.txt-WhatdoescodehttppostBuffercodereallydo)
  - 把http.postBuffer調大送給server的git物件也會變更大，所以調越大的話會導致push越慢 [📗](https://learn.microsoft.com/en-us/azure/devops/repos/git/rpc-failures-http-postbuffer?view=azure-devops)
    - 基於push會變慢，所以並不推薦修改http.postBuffer的值
  - 如果把http.postBuffer[調到超過server能接受的上限，那push還是會失敗](https://blog.miniasp.com/post/2014/09/07/Handle-large-Git-repository-on-Visual-Studio-Online)
  - server接受的檔案大小可以調整，但需要有權限，且不建議這麼做 [📗](https://docs.gitlab.com/topics/git/troubleshooting_git/#increase-the-post-buffer-size-in-git)
  - 檔案本身的大小不等於git物件的大小，因為git演算法會把檔案壓縮後變成git物件
  - `git config --get http.postBuffer` 可查看postBuffer大小，若無回傳值則代表為預設值

3/6
- 學習如何在Svelte專案設置default route [📗](https://svelte.dev/docs/kit/advanced-routing)
- 看standup show學英文 [📘](https://www.youtube.com/watch?v=0t8QCW78oDE)
  - That's messed up
    - A: That guy let his dog poop in front my door. He didn't even  clean it, he just left.
    - B: That's messed up.
  - tick someone off
    - I definitely get road rage. Once I start driving, a lot of things start to tick me off.

3/5
- 閱讀[橡果學院貼文](https://www.threads.net/@the.acorn.academy/post/DGxeAzZyZo5?xmt=AQGzXXUj_EAErEbaUiXTyZXJwqQ60Txv2xp8qNroyVQ1GJQ)
```
To即將要畢業找美商or海外工作的各位：
過去三天，我提供了幾大重點給大家，
給大家技巧上的建議還有心理建設，
前天講了履歷，昨天講Coffee Chat，
今天講英文面試，
明天會短暫回歸輕鬆小故事
這篇會專攻大家都適用的英文面試觀念，
會稍微籠統一點，
但我相信至少有一項會讓你覺得耳目一新
不要把這篇當作我的Google面試分享，
要看谷歌面試的話，去留言區看之前文章
-不管大家說什麼架構最棒，
其實來來去去都差不多，反正就是：
1-2句話講你的任務，
1-2句話講為什麼這件事很困難，
3-4句話講解決過程，1-2句話講結論，
1-2句話講你學到什麼，或是未來如何調整
（要詳細！看留言示範）
-只要有5個故事可以說，
基本上可以面對任何問題，
剩下的就是隨機應變去小調整，
我個人認為大家可以去查一下P&G八大問，
這八題都能回答的話，就完全沒問題了，
同一個故事可以回答好幾題
-儘量不要拿到面試了才準備，
尤其對我們英文非母語者來說，
要練到嘴巴腦袋都習慣英文，
是需要不少時間的，我之前還在上班的時候，
甚至會沒事去面試，練練手感

-如果你的英文程度在多益700以上的話，
英文面試強烈建議大家寫稿，
我知道大家都說，寫稿會限制你的發揮，
但最大原因是因為你寫了稿，
但沒有真的花很多時間把他變熟，
或是沒有人真的陪你練過，
自我介紹+五個故事，共六篇稿，
用AI三天一篇綽綽有餘，先不論完美不完美，
兩個禮拜就可以搞定
-大部分的外商其實對英文口說程度，
沒有真的很高的要求，
但如果是海外求職就真的要很好了，
除非能靠硬實力碾壓別人，但即使這樣，
很容易進去之後遇到天花板，
所以英文口說要加油，
我知道聽起來有點在販賣焦慮，
但某種程度上確實是，
要不然我就不會離開谷歌創業了，
對嚮往國際生活風格的人來說，
英文口說是硬需求
-英文口說要練到高低起伏的訣竅，
就是儘量讓你的句子短一點，每一個逗號都暫停，
每一個重點動詞、比較級形容詞、數字都加重音

什麼叫詳細，舉例：
不只要說
we created content that increase conversion rate
而且還要回答
what content, why this content, how did you come up with this content
又或者：
We believe that A is the better investment choice because they have lower risk.
還可以再加一點細節
A is the better investment choice because of their higher free cash flow, which can be a contingency if an event raises energy cost.
```

- 了解如何使用dev tool查看CSS animation [📗](https://developer.chrome.com/docs/devtools/css/animations?hl=zh-tw)


3/4
- 學到新的繪製半透明形狀，但不影響子元素的方法
  ```html
      <!-- 使用Tailwind的作法 -->
      <div id="parent" class="w-48 h-48 relative before:absolute before:top-0 before:left-0 before:content-[''] before:w-full before:h-full before:bg-blue-300 before:opacity-50">
          <p>child element</p>
      </div>
  ```

    相當於以下的手寫CSS

  ```css
      #parent {
          width: 12rem;
          height: 12rem;
          position: relative;
      }

      #parent::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background-color: #93c5fd; /* Tailwind 的 bg-blue-300 */
          opacity: 50%;
      }
  ```

- 閱讀 [忙不是藉口，開不好 One-on-One 就是主管的問題](https://medium.com/@stevenyeh/%E5%BF%99%E4%B8%8D%E6%98%AF%E8%97%89%E5%8F%A3-%E9%96%8B%E4%B8%8D%E5%A5%BD-one-on-one-%E5%B0%B1%E6%98%AF%E4%B8%BB%E7%AE%A1%E7%9A%84%E5%95%8F%E9%A1%8C-bae77b0f466e)

3/3
- 了解IndexedDB [📗](https://developer.chrome.com/docs/apps/offline_storage)
    - 針對indexedDB的操作是非同步的
    - indexedDB的容量配額會根據瀏覽器有差異，當超過容量配額時先刪除哪些資料的標準也不同
        - `超過容量配額`時刪除資料的動作稱作`資料驅離`，localStorage、sessionStorage也有這個機制
    - 無痕模式下indexedDB容量配額會比較低
    - Safari是目前唯一有實作主動驅離資料的瀏覽器
        - [主動資料驅離](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria#proactive_eviction)是指超過一定時間沒有操作網站的話，就把IndexedDB資料清除
- 了解如何用dev tool查看及變更 indexedDB 資料 [📗](https://developer.chrome.com/docs/devtools/storage/indexeddb?hl=zh-tw)

3/2(S)

3/1(S)

2/28
- 讀Svelte教學 ~Basic Svelte/Events/Spreading events [📗](https://svelte.dev/tutorial/svelte/spreading-events)
- 讀Svelte教學 ~Basic SvelteBindingsTextarea inputs [📗](https://svelte.dev/tutorial/svelte/textarea-inputs)
    - 當對select使用`bind:value`時要小心。當綁定初始化後，Svelte會自動將select的預設值設為option的第一個項目，而不是一直維持與之綁定的state的值

2/27
- 了解如何使用Svelte `bind:this` 取得DOM element [📗](https://svelte.dev/tutorial/svelte/bind-this)

2/26
試著在Svelte+Vite專案設定Graphql codegen

1. 安裝以下codegen套件
```
    // 用於GraphQL codegen產出type、schema
    "@graphql-codegen/typescript-graphql-request"
    "@graphql-codegen/cli"
    "@graphql-codegen/introspection"
    "@graphql-codegen/typescript-apollo-client-helpers"
    "@graphql-codegen/typescript-resolvers"
    "@parcel/watcher"

    // 用於fetch，且有plugin可以在codegen時產出document
    "graphql-request"

    // graphql-request的依賴
    "graphql-tag"
    "graphql"
```


2. 設定codegen config
   
  [設定檔可以用多種格式撰寫](https://the-guild.dev/graphql/codegen/docs/config-reference/codegen-config)
  ```ts
  // codegen.ts

  import { type CodegenConfig } from '@graphql-codegen/cli';

  const config: CodegenConfig = {
    schema: '你的GraphQL endpoint',
    documents: ['src/**/*.(svelte|ts|graphql)'],
    ignoreNoDocuments: true,
    // 每次執行codegen都把舊的檔案覆蓋
    overwrite: true,
    // 開啟watch模式，只要document有變動就會跑codegen
    watch: true,
    generates: {
      // codegen產出的type、document存放的位置
      './src/generated/graphql.ts': {
        plugins: [
          'typescript',
          'typescript-operations',
          '@graphql-codegen/typescript-graphql-request',
          'typescript-apollo-client-helpers',
          'typescript-resolvers',
        ],
      },
      // codegen產出的schema存放的位置
      './src/generated/graphql.schema.json': {
        plugins: ['introspection'],
      },
    },
  };

  export default config;
  ```

3. 在package.json新增script
  ```
  "scripts": {
      "dev": "yarn codegen & vite dev",
      "codegen": "graphql-codegen",
    },
  ```

4. 根據需求建立GraphQLClient集中管理headers之類的設定
  ```ts
  const apiClient = new GraphQLClient('你的GraphQL endpoint', {
    // 因為token可能會動態改變，所以headers需要定義為function
    headers: () => {
        const token = localStorage.getItem('key的名稱');

        return {
          // GraphQL的不論是query或mutation，method都是POST
          method: 'POST',
          authorization: `Bearer ${token}`,
        }
    },
      // 因為graphql-request沒有狀態管理功能，所以需要使用middleware和Svelte store製作API狀態管理
    requestMiddleware: async (request) => {
      apiStateManagementStore.set({
        isLoading: true,
      });
      return request;
    },
    responseMiddleware: async (response) => {
      if (response instanceof ClientError || response instanceof Error || response.errors) {
        apiStateManagementStore.set({
          isError: true,
        });
      }

      apiStateManagementStore.set({
        isLoading: false,
      });
    },
  });

  export default apiClient
  ```

2/25
- 閱讀 [Things only senior React engineers know](https://medium.com/@meric.emmanuel/things-only-senior-react-engineers-know-618d81154cb6)
  - 可以不用useEffect就不要用，尤其是在useEffect的callback中操作和UI有關的邏輯，因為會提高出現bug的風險
  - 當key prop的值改變時，會直接把整個element unmount，並mount一個新的element到DOM
  - 組件的children型別應該設為ReactNode，這樣才不會過度限縮彈性
    - ReactNode包含所有可以被渲染的東西，string、number、boolean、undefined、null、\<p>text<\/p>
    - ReactElement 則只有\<p>text<\/p>

2/24

2/23(S)

2/22(S)

2/21
- 學習一些更禮貌地說英文方式 [📘](https://www.youtube.com/watch?v=rQN4-l5AXE0)

|分類||例句|
| --- | --- | ---|
|請求|I was hoping you...|I was hoping you could help me.|
|請求|I don't suppose..., could you?|I don't suppose you could lend me a hand, could you?|
|表達意見| Aren't you kind of...| Aren't you kind of young to be getting marry?|
|討論|someone seems to...| You seem to have made a mistake here.|
|拒絕|I'm not sure I'll be able to...| I'm not sure I'll be able to make it to the meeting.|
|拒絕|It's looking unlikely that...|It's looking unlikely that we'll finish on time.|

2/20
- 學習一些更禮貌地說英文方式

|分類||例句|
| --- | --- | ---|
|請求 |I was wondering if... |I was wondering if you could do me a favor. |
|請求|Could I please ... | Could I please have your name? |
|請求|Do you mind if I...| Do you mind if I sit here? |
|請求|Would it be possible to...| Would it be possible to reschedule the meeting?|
|其他|By any chance| Are you, by any chance, available this weekend?|

2/19
- 在Svelte專案試用[shadcn-svelte](https://www.shadcn-svelte.com/)
  - Svelte的生態圈真的是比起React實在是小太多，簡直像是孤兒
  - 了解到新的選library的方式。可以看repo的最後一次commit時間距離當下多久
    - 如果是一個很新的repo最好在1~2個月以內
    - 已經算成熟的(ex: ajv)則半年左右都在允許範圍
    - 超成熟的(ex: lodash)則超過一年也行

2/18
- 讀Svelte教學 ~Basic Svelte/Logic/Await blocks [📗]([https://svelte.dev/tutorial/svelte/spread-props](https://svelte.dev/tutorial/svelte/await-blocks))
- 了解如何在AWS上設置一個純前端專案
  - S3
    - bucket
  - Cloudfront
    - distribution
      - error page
      - behavior
    - function
- 試著使用Github Actions做PR merge後自動部署到S3 bucket的dev folder

2/17
- 了解如何在Svelte專案設置formatOnSave功能 [📗](https://hoishing.medium.com/auto-format-svelte-in-vs-code-c0208c2010c9) [📗](https://github.com/sveltejs/prettier-plugin-svelte?tab=readme-ov-file)

2/16(S)
- 了解如何用Svelte store實作API狀態管理 [📗](https://www.youtube.com/watch?v=umnSLfR_VkM)
  - writable
  - readable
- 了解AbortController
  - 用於取消request  

2/15(S)

2/14
- 讀Svelte教學 ~Basic Svelte/Props/Spread props [📗](https://svelte.dev/tutorial/svelte/spread-props)

2/13
- 了解如何使用docker部署網站
  - 撰寫Dockerfile

  - 執行build image，並幫它打tag
    ```
    # -t 是tag的意思，用於幫image命名
    # image name 後方是指Dockerfile所在的目錄，.代表當前的目錄
    docker build --tag my-app .
    ```

    以上指令相當於以下多個指令
    ```
    docker build .
    docker image ls
    docker tag <image id> my-app
    ```

  - 把image 推到image儲存庫
    ```
    docker image push myrepo/my-app:latest
    ```
  - 在server上把image拉下來，並把它初始化變成一個容器(執行容器)
    ```
    docker image pull myrepo/my-app:latest
    ```

    ```
    # -d 是detach的意思，讓container在背景執行，不會佔用終端機
    # -p 是port的意思，將server的port 80連接container的port 3000
    # --name 後方是container的名字，可以省略
    # myrepo/my-app 是image的名字，即在步驟2中打的名稱
    docker container run -d -p 80:3000 --name hello123 myrepo/my-app
    ```

  - (optional) 根據需求在當下正在執行的container 設定環境變數
    ```
    # -e 是environment的意思，用於設定環境變數
    docker container run -e MY_ENV=production -e PORT=3000 myrepo/my-app
    ```
    之所以不直接在build image時就直接把環境變數包進去是因為這樣該image就跟特定環境綁定了，不能在多個環境複用

- 初步了解AWS的ECR服務
    - AWS的ECR是image的儲存庫，相當於私有的Docker Hub，Github也有提供私有image儲存庫的服務
    - 可和其他AWS 服務整合

2/12
- 看Docker快速入門教學[📗](https://www.youtube.com/watch?v=1wfgS31LcgQ&list=PLVVMQF8vWNCLsTAWVvGRyQP0ajj0Rx1--&index=2&t=20s)
  - 建立image的方式有2種
    - `docker build`
      - 用dockerfile是用於建立image
    - docker commit
      - 將image初始化成container，進行修改後再建立成另一個image
- 了解docker指令
  - docker指令有分新舊版，雖然舊版仍能使用，但推薦使用新的
  - 查看image
    ```
    # 本機所有的image
    # 舊版
    docker images
    # 新版
    docker image ls

    # 本機某個image
    docker images <image name>
    ```
  - 查看所有的container
    <img width="1017" alt="截圖 2025-02-11 下午6 15 35" src="https://github.com/user-attachments/assets/0cd9ac9f-837a-476c-89ed-e49150c4e40c" />
    ```
    # 舊版
    docker ps -a
    # 新版
    docker container ls
    ```
  - 移除image
    ```
    # 舊版
    docker rmi <image name>
    # 新版
    docker image rm <image name>
    ```
  - 移除container
    - image每次執行後就會產生一個container，如果用完不需要了可以把這些container刪掉
    ```
    # 舊版
    docker rm <container id或name>
    # 新版
    docker container rm <container id或name>
    ```

2/11
- 試試看在Windows11[安裝HyperV](https://www.youtube.com/watch?v=ExZIQj-DvI8)或WSL
  - 在Windows使用docker會需要它
  - 可以透過[官方文件](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-hyper-v?pivots=windows)內指示，使用shell command安裝
  - 可以照[影片](https://www.youtube.com/watch?v=ExZIQj-DvI8)的指示，來建立bat檔安裝
    <img width="739" alt="截圖 2025-02-10 下午6 02 33" src="https://github.com/user-attachments/assets/e7a047f8-72ee-4f20-baa1-6b7a858c704a" />
- 試試看在Windows11[安裝](https://docs.docker.com/desktop/setup/install/windows-install/)、啟動docker
  ![螢幕擷取畫面 2025-02-11 221118](https://github.com/user-attachments/assets/35d0e04f-947b-484a-a86a-e4bd1a79bf67)
  `啟動之後發現電腦效能太差，會導致風扇狂轉，所以刪除了，之後docekr的東西都只用Mac試`

2/10
- 試試看在Mac[安裝](https://docs.docker.com/desktop/setup/install/mac-install/)、啟動docker [📗](https://medium.com/%E5%AE%B8-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98/mac-%E5%AE%89%E8%A3%9D-docker-%E5%8F%8A%E6%93%8D%E4%BD%9C%E6%8C%87%E4%BB%A4-6a9cfaa55979)
  - 安裝好桌面版之後，只要點兩下圖示就可以啟動docker
- 了解docker指令
  - 下載image
    - 指令
      ```
      # 舊版
      docker pull <image name>
      # 新版
      docker image pull <image_name>
      ```
      如果pull image時省略repo名，則預設會從Docker Hub拉取image
      如果是要從AWS ECR拉取image，則要在image名稱前加上ECR的網址還有repo名稱

    - docker應用程式下載
      <img width="1266" alt="截圖 2025-02-10 下午6 07 02" src="https://github.com/user-attachments/assets/4820d1f7-53e1-4d58-849c-0491c40febfb" />
      <img width="979" alt="截圖 2025-02-10 下午6 07 16" src="https://github.com/user-attachments/assets/6645bc53-3bff-4dba-8552-8e30e777f943" />
  - 搜尋想要使用的image
    - 指令
      ```
      docker search <image name>
      ```
    - 到[DockerHub](https://hub.docker.com/)搜尋
  - 執行image以產生container
    ```
    # 舊版
    docker run <image name>
    # 新版
    docker container run <image name>
    ```
2/9(S)
- 初步了解Docker [📗](https://www.youtube.com/watch?v=ZKdlglAxr7g)
  - Docker是一種實現容器化的工具
    - 容器化是指把應用程式跟它的依賴打包到一個獨立的環境。這個獨立的環境就是容器(container)
      - container初始狀態是映像檔(image)，透過指令執行image就會變成container
    - K8S是另一個目前主流的容器化工具
  - container具有一致性，可攜性、隔離性
    - 基於隔離性，容器內內只能放一種應用程式
 

2/8(S)

2/7
- 學習用於描述衝動行為、人的詞彙、片語 [📘](https://dictionaryblog.cambridge.org/2025/02/05/reckless-and-impulsive-acting-without-enough-thought/)
  - with no thought for something
    - He bought a expensive camera, with no thought for his financial condition.
  - hotheaded
  - [rash](https://www.thesaurus.com/browse/rash)
    - It was rash of him to buy such a expensive camera.
    - I think it was a bit rash of them to get married when they'd only known each other for a few weeks. (marry in haste, repent at leisure)
  - rush [headlong](https://www.thesaurus.com/browse/headlong) into something
    - She rushed headlong into marriage without really getting to know her partner.

2/6
- 了解React-Redux的connect function [📗](https://react-redux.js.org/api/connect)
  - connect function用於`連接class component和Redux的store`
  - connect接收mapStateToProps, mapDispatchToProps等參數，並回傳一個HOC(接受component並回傳component的function)
    - connect的內部有一段code可以取得store的值，再把store傳入mapStateToProps取得需要的某個屬性存入變數，再把變數當作props傳給傳入的component，這樣component就能和store連接起來了 [🖌](https://codesandbox.io/p/sandbox/redux-zombie-child-component-problem-5h34q5?file=%2Fsrc%2FHOC%2Fconnect.js%3A5%2C37-5%2C42)

2/5
- 聽Johnny Stimson的You can do it 學英文 [📘](https://www.youtube.com/watch?v=L2ADdk3w-rg&list=RDMM&index=4)
  - put your heart into something/put your heart and soul into something (全心投入)
  - brush someting off (拍掉、刷掉)
    - I brushed the dirt off my shoes.
  - It is a part of life. (表達某件事情是人生中不可避免的經歷，無論是好是壞。通常用來安慰別人，或者表達一種對人生的理解)
    - Failure is a part of life.

2/4
- 了解mapStateToProps [📗](https://www.dhiwise.com/post/mapstatetoprops-or-useselector-a-quick-comparison)
  - mapStateToProps是配合Redux使用的一種function，它是connect component的一部分，用於取得store
    - mapStateToProps會把整個store中的某個屬性當作props往下傳，而useSelector則是訂閱store的部分屬性，所以後者re-render次數會較少，故效能較好
  - 最早推出是為了`配合class component使用`，已經成為一種古早味設計模式
    - function component出了以後，Redux也推出功能類似的useSelector來搭配它
    - `不要跟function component一起用，會導致zombie child component`

2/3
- 了解stacking context [📗](https://ithelp.ithome.com.tw/articles/10217945)
  - stacking context是指使用positioned box建立的環境堆疊，可以透過以下CSS屬性建立
    ```css
    position: fixed;
    
    position: sticky;
    
    position: relative;
    z-index:100;

    position: absolute;
    z-index:100;

    transform: translate(100px, 100ox);

    /* 只要小於1就可以 */
    opacity: 0.9;
    ```
  - stacking context內的元素不會觸發[reflow](https://github.com/tempura327/learning-diary/blob/master/2024/README.md#1121)
  - 位於不同stacking context的元素間不會互相比較z-index

- n8n[📗](https://github.com/n8n-io/n8n)

1/29~2/2
過年休息

1/28
- 閱讀[選工作前，先了解該公司怎麼做事故檢討](https://www.explainthis.io/zh-hant/career/how-companies-handle-incident-reviews)
  - `不指責人的事故檢討很重要`
    - 若事故檢討的方式是找戰犯，當問題發生時，犯錯的那個人或團隊，很可能會試圖掩蓋問題，這對於解決問題反而是不利的
- 閱讀[選一間冷靜的公司](https://www.explainthis.io/zh-hant/career/calm-company)
  - 冷靜的公司
    - 平緩地成長、有穩定的收益
    - 自由、彈性、平靜的工作環境
    - 對於決策深思熟慮
  - 喪心病狂的公司
    - `收益不好，導致需要不斷的資金注入`，且基本面不佳，難以改善
    - 明示、暗示地威脅、施壓，使員工感到壓力、焦慮
    - `員工`常常在吸收負面情緒，導致下班後感到`筋疲力盡`
    - `時程不合理`，只能靠不斷加班完成
    
- 閱讀[21 項給軟體工程師的職涯提醒](https://www.explainthis.io/zh-hant/career/21-career-tips-for-software-engineers)

1/25~1/27
嘉義旅遊、達康表演、吉伊卡哇燈會

1/24
- 用Zustand做TodoList練習 [🖌](https://codesandbox.io/p/sandbox/try-zustand-and-chakaraui-1-dn5qkv?file=%2Fsrc%2FApp.tsx%3A21%2C16)

1/23
- 聽Johnny Stimson - Flower練英文
  - the end of the edge of sky (形容很遠的地方、遠在天邊)
    - My wife divorced me, then moved to Canada from Taiwan. I feel like she's on the edge of the sky.
  - get something out of my thoughts (將某事物從短期的思緒中移除)
    - I need to focus on work, but I can't get my vacation out of my thoughts.
  - get something out of my mind (將某事物從長期的思緒、記憶中移除)
    - My wife divorced me, and then moved to Canada. I know she won't come back to me. It's time to get her out of my mind.

1/22
- 了解Zustand的useSelector
  - Zustand跟Redux一樣都建議使用useSelector來只取出需要的部分，以減少因為store變動而造成的re-render
  - 可以把處理重複邏輯包進去useSelector

1/21
返鄉，休息一天

1/20
- 了解Zustand和Vanilla Zustand的差異
  - 它們的關係就像React Redux和Redux，前者能直接用於React，後者是整個library的核心，可以獨立於框架之外使用
  - `Zustand`的create`回傳`可直接跟store互動的`hook`，而`Vanilla Zustand`的createStore則`回傳`值則是store `instance`

1/19(S)
- 了解如何使用Zustand的create function [📗](https://www.youtube.com/watch?v=Nru6yGYivvg)

1/18(S)
- 學英文
  - As the saying goes
  - puts in an appearance (出現一下下)
    - I didn't really want to go to the party, but I thought I'd better put in an appearance.
  - on the scene (去有事情發生的地方)
    - Firefighters were on the scene within minutes.

1/17
- 了解Zustand的基本用法 [📗](https://www.youtube.com/watch?v=Nru6yGYivvg)

##### 1/16
- 了解Zombie Child Problem [📗](https://medium.com/@adithyaviswam/can-the-context-api-result-in-the-zombie-children-issue-a00d52af8c8)
  - zombie child component是指「是一個應該被銷毀但暫時沒有被銷毀的子元件」
    - zombie child component可能會嘗試讀取store中不存在的資料，可能會引起memory leak、不一致的UI、錯誤的資料更新等問題
  - 這個問題和React中的父、子component的生命週期執行順序有關
      ```
      Parent initialized
      Parent rendered for first time
      Child initialized
      Child rendered for the first time
      Child componentDidMount (useEffect is invoked)
      Parent componentDidMount (useEffect is invoked)
      Child componentDidUpdate (useEffect is invoked)
      Parent componentDidUpdate (useEffect is invoked)
      ```
      
      ![_- visual selection](https://github.com/user-attachments/assets/b5dcda4e-209c-44c8-87fd-1fba90aa7c0c)

1/15
- color: light-dark(); [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/light-dark)
  - 簡單切換dark mode、light mode顏色的方式
    ```css
    .light {
      /* forces light color-scheme */
      color-scheme: light;
    }
    .dark {
      /* forces dark color-scheme */
      color-scheme: dark;
    }

    code {
      color: light-dark(var(--light-code), var(--dark-code));
    }
    ```
  - paint-order: stroke fill markers; [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/paint-order)
    - 調整text-stroke、text-fill的執行順序以畫出不同的文字效果
      - 先stroke，後fill文字效果看起來會較細。反之則較粗
      - 再搭配text-shadow的話可以產生立體效果 [📗](https://codepen.io/web-dot-dev/pen/dyxryKE)

1/14
- 看stand-up show學英文 [📘]([https://www.youtube.com/watch?v=dI38GtWFihY](https://www.youtube.com/watch?v=0t8QCW78oDE))
  - free-range (放牧)
  - don't trust somebody
    - What he said was complete nonsense. Don't listen to him.
  - Don't get me wrong.
    - Don't get me wrong, I really enjoy helping out, but I can't handle this all on my own.
  - I'm all about...
    - I'm all about exploring new cuisines when I travel.
  - public shaming (公開羞辱)
  - check out (結帳)
  

1/13
- 初步了解Zustand
  - 為了簡化使用context、Redux時，會出現的複雜的狀態管理而生的狀態管理library
    - 試圖解決Zombie Child Problem、React Concurrency、Context Loss
  - 採用Flux
    - Redux也是採用Flux。它的目標是`將資料與View去做分離`，好處是`讓狀態更好維護`、變化變得較好追蹤
  - immutable state
    - 跟Redux一樣，因為它們都採用Flux
  - `不需要用context provider`把整個app包起來
    - 因此可以避免zombie child component的問題
- 學英文
  - toiletries (盥洗用品)
  - throw the baby out with the bathwater (把有價值的東西不小心跟不重要的東西一起丟掉)
    - I know the wallpaper is ugly, but this is a lovely house. We can always redecorate.

1/12(S)
- 了解JS自訂事件、compsition event
  - new一個Event instance，然後綁到element上，再用.dispatchEvent就可以手動觸發
  - composition event 是指 compositionstart 、 compositionend ，以及 compositionupdate 

1/11(S)
- 了解HTTP cache機制 [📗](https://web.dev/articles/http-cache?hl=zh-tw)
 - 瀏覽器送出的所有 HTTP request會先轉送至瀏覽器快取，檢查是否有可用的有效快取。如果比對結果相符，系統就會用瀏覽器快取中當response，進而提高載入速度
  - HTTP 快取的行為是由request header和response header的組合一起控管


1/10
- 聽AI分享會 [📚](https://ai-hurry-up.zeabur.app/1)
  - [HuggingFace](https://huggingface.co/)
    - 放了很多AI模型的網站，部分可免費用
  - [Napkin AI](https://www.napkin.ai/)
    - 根據文字畫圖表、關係圖的AI

1/9
- 讀The ultimate guide to cache-busting for React production applications，了解瀏覽器 cache機制 [📗](https://maxtsh.medium.com/the-ultimate-guide-to-cache-busting-for-react-production-applications-d583e4248f02)
  - 瀏覽器`用檔名`是否一致`辨別是否能直接用瀏覽器的快取`，還是要跟server拿，並存入瀏覽器快取
  - 使用vite之類的bundler工具執行`build後`，會得到chunk file，名稱為`[name].[hash].js`，且每次build，只要`code有任何改變hash就會變`
    - 以此避免server上的資源內容已經改變，卻一直使用瀏覽器快取。這種技術被稱為cache-busting
  - build後還會產生`mapper file`，名稱通常為index.[hash].js or bundles.[hash].js，裡面會記錄哪個頁面需要哪個載入哪個chunk
  - 如果response header內沒有Cache-Control: no-cache，瀏覽器會先解析 HTML檢查所需的資源，並根據檔名去瀏覽器快取找是否有可用的快取
  - 如果deploy的當下有使用者剛好在網站上
    - 在A頁，那麼因為在deploy以前他就在線上，所以已經拿到mapper file1，已經在A頁，所以A頁需要的chunk也已經載入了，所以A頁就不會crash
    - 從A頁跳到B頁，因為deploy前沒進去過B頁，所以沒載入B需要的chunk、瀏覽器快取內也沒這些chunk，這時就只能根據mapper file1去跟server拿資源，但是這時早就被更新成新的資源了，所以找不到mapper file1內指出需要的chunk，於是就會出現`chunk error`
  - 使用以下標籤可強迫瀏覽器不要把index.html存到快取，這樣就不會一直拿到舊的mapper file
    ```html
    <meta http-equiv=’cache-control’ content=”no-cache, no-store, must-revalidate”>
    <meta http-equiv=’expires’ content=’0'>
    <meta http-equiv=’pragma’ content=’no-cache’>
    ```

1/8
- 了解HTTP cache機制 [📗](https://www.youtube.com/watch?v=1Ahl3ah3UBU)
  - 瀏覽器快取內存的資源是否過期是以[Cache-Control]([https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control))做判斷
    - Cache-Control在request header和response header出現時可設定的指令會有些微不同
      - 但兩者都可以設定`max-age=<秒數>`、`no-cache`(不要使用瀏覽器快取，永遠去跟server拿)、`no-store`
  - 當瀏覽器快取過期時，`304代表`client端有去問server資源是否有更新，server回`資源沒變，可以繼續用瀏覽器的快取`
    - 向server詢問資源是否過期時會用request header、response header中的屬性對比判斷
      - [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match)和[E-Tag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag)
      - [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since)和[Last-Modified](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified)

1/7
- 讀React的生命週期 [📗](https://www.explainthis.io/zh-hant/swe/react-lifecycle)
  - class component才有lifecycle，分為mount, update, unmount三個階段，各個階段有不同的lifecycle method可用
  - funtion component只能用hook模擬生命週期

1/6
- 學TanStack query
  - `usePrefetchQuery`用於使用者很常要看的資料，在某個事件發生時已經猜到使用者要看資料了，就先撈起來放，可以減少使用者等待時間，以此提升UX
  - `invalidateQueries`用於把撈回來的資料標記為stale，這樣就會自動再重撈，常用於建立、更新完後，重撈資料
- 了解object和Map的差異 [📗](https://www.explainthis.io/zh-hant/swe/map-vs-object)
  - Map可簡單地迭代、知道有幾個key、key可以是任何型別 

1/5(S)
- 了解JSON Server的用法
- 認識[MistCSS](https://github.com/typicode/mistcss)

1/4(S)
- 學TanStack query [📗](https://www.youtube.com/watch?v=I-qGvLln-pg)
  - 了解如何用useMutation實作樂觀更新、悲觀恢復

1/3
- 學TanStack query [📗](https://tanstack.com/query/v4/docs/framework/react/reference/useQuery) 
  - 了解refetchInterval、retry、retryDelay、refetchOnWindowFocus、refetchOnReconnect等useQuery常用的設定
    ```
    const {data} = useQuery({
      queryKey: ['todo'],
      queryFn: async() => {
        // get是一個包裝過的axios function，實作可以忽略
        return await get('/todos');
      },
      // 每10分鐘refetch
      refetchInterval: 60_000 * 10,

      // 失敗時重撈2次，預設為3次
      retry: 2,

      // 每次間隔5秒
      retryDelay: 5_000,

      // 重別的視窗切回來時refetch，預設為true
      refetchOnWindowFocus: true,

      // 斷網後恢復連線時refetch，預設為true
      refetchOnReconnect: true
    })
    ```
- 了解甚麼是`樂觀更新`、`悲觀恢復`
  - 樂觀更新，不等response回來，直接當作更新成功，並把資料顯示在畫面上，以此提升UX。通常用於低風險的動作，且會和悲觀恢復一起用
  - 悲觀恢復，request失敗時，把資料恢復到操作之前的正確狀態

1/2
- 學TanStack query (React Query) [📗](https://www.youtube.com/watch?v=7MDI54nlEbc)
  - 管理data、fetch狀態、處理cache的library
  - useQury需要一個unique key、回傳promise的function，useMutation則只需要回傳promise的function
  - query有status和fetchStatus兩種狀態，前者和data的狀態有關，後者和request的狀態有關
  - mutation只有status，它和request的狀態有關
- 學英文
  - make something a breeze
    - Using this app makes travel planning a breeze. (使用這個APP讓旅遊規劃變得超簡單)
    - You won't have any problems with the test. It’s an absolute breeze.
  - rule of thumb
    - According to my rule of thumb, it will take about 40 minutes to get to Taipei Train Station from here if we take the subway. (根據我的經驗，從這裡搭捷運去台北車站要花40分鐘)
 

1/1
- 複習事件捕獲、事件冒泡 [📗](https://ithelp.ithome.com.tw/articles/10191970)
  - addEventListener的第三個參數用於設定事件補獲，或事件冒泡。預設為false，即事件冒泡
  - 點擊的element的父層會先執行事件捕獲，再執行事件冒泡
  - 點擊的目標element的事件捕獲、冒泡執行順序和程式碼寫的順序有關
- 看stand-up show學英文 [📘](https://www.youtube.com/watch?v=dI38GtWFihY)
  - cut the music off
  - I'd like a table for 3 people, please.
  - for real
    - I thought it was not your accent for real, but I was wrong.


