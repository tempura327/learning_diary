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
