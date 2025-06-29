7/6(S)

7/5(S)

7/4

7/3

7/2

7/1

6/30

6/29(S)
- 了解Go的變數宣告 [📗](https://go.dev/tour/basics/10)
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
- 了解Go的具名回傳、多重回傳 [📗](https://go.dev/tour/basics/7)
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
- 試著import pkg.go.dev上的套件、local module並使用 [📗](https://go.dev/doc/tutorial/create-module) [📗](https://go.dev/doc/tutorial/call-module-code)
  - 一個 .go 檔內只能有一個`package main`，因為每個 .go 檔案只能屬於一個套件
  - 同一個資料夾下的 .go 檔，都必須是同一個 package
  - 只有 `package main` 是整個程式的entry，因此只有`package main` 才能被 `go run` 或 `go build`
- 讀Because of Winn-Dixie ~chapter 22 學英文
  - crepe paper (皺紋紙)
  - shimmery (金蔥狀的閃亮)

6/24
- 安裝Go，並用Go寫一個Hello world [📗](https://go.dev/doc/tutorial/getting-started)

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
