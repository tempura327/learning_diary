5/18(S)

5/17(S)

5/16

5/15

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
