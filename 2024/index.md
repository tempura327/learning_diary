12/8(S)

12/6~7
北埔旅遊

12/5

12/4
- 學英文
  - It's up to you ... (取決於你)
- 讀完Redux Essential 3，並照著做一個小練習 [🖌](https://codesandbox.io/p/sandbox/epic-hill-3sryps)

12/3
- 讀完Redux Essential 2
- 讀Redux Essential 3 ~Showing the Posts List

12/2
- 讀Redux Essential 2 ~Defining Pre-Typed React-Redux Hooks
  - 了解如何用slice，以及它如何集中管理action、reducer，並產出產出actoion creator
  - `reducer一定是pure function，且它不做非同步的事`
    - slice的reducers中的code看起來是mutable，可以這麼做是因為createSlice使用的Immer會自己幫你copy state，意味著reducer收到的state並不是原本的那份，所以不會造成side effect
  - thunk是一個function，接收dispatch、getState，可以處理非同步
    - 一樣可以再包一層變成thunk creator，或者用createAsyncThunk
  - 透過useSelector可以讓組件得到store當下的state，進而取得某個屬性的值

12/1(S)

----------
11/30(S)

11/29
- 聽Chains練英文
- 讀Redux Essential 2 ~Redux Slices
  - 了解如何使用Redux dev tool

11/28
- 讀完Redux Essential 1
  - action是物件，描述要用哪個reducer、傳甚麼paylod給reducer
  - reducer是一個function，它會取得當下的state的copy，然後根據action.playload去計算新的state，並return出去讓store自己更新state
    - 之所以copy是因為要保持immutable，來減少side effect
  - dispatch是一個function，把action送去給reducer
  - store，儲存global state的地方
  - 了解如何用action creator減少重複手寫action

11/27
- 聽一篇BBC 6mins English
- 讀Redux Essential 1 ~State Management
  - 了解Redux的核心精神，immutable(pure)

11/26
- 看React紀錄片~45min

11/25
- React
  - 複習controlled component、uncontrolled component的優缺點 [📗](https://medium.com/starbugs/%E4%BB%80%E9%BA%BC-%E5%85%83%E4%BB%B6%E7%AB%9F%E7%84%B6%E4%B9%9F%E6%9C%89%E5%88%86%E5%8F%AF%E6%8E%A7%E5%88%B6%E8%88%87%E4%B8%8D%E5%8F%AF%E6%8E%A7%E5%88%B6-%E6%8E%A2%E8%A8%8E-react-controlled-%E4%BB%A5%E5%8F%8A-uncontrolled-component-d6b8285d8939)

11/24(S)

11/23(S)
- 學習安慰人的英文句子[📘](https://dictionaryblog.cambridge.org/2024/11/06/nobody-blames-you-phrases-for-offering-reassurance/)
  - It wasn't your fault.
  - Nobody's perfect.
  - Nobody blames you.
  - We'll be cheering you on.

11/22
- 了解甚麼是UMD

11/21
- 了解甚麼是reflow、replant [📗](https://dev.to/gopal1996/understanding-reflow-and-repaint-in-the-browser-1jbg)
- 了解操作DOM對效能的影響

11/20
- Svelte [📗](https://ithelp.ithome.com.tw/articles/10350711)
  - 了解其優點
    - 無virtual DOM
    - 因為不以Svelte作為執行環境，所以只要裝在devDependecies就好，bundle size小
    - 使用SvelteKit可以做出SSR效果
- React
  - 了解React專案的tsconfig的compileOptions.jsx [📗](https://www.totaltypescript.com/react-refers-to-a-umd-global)

11/19
- CSS
  - 了解display:none和visibility:hidden差異
    - 前者不占位，後者占位
- 看React紀錄片~35min

11/11~11/18
日本旅遊

11/10(S)

11/9(S)

11/8
- 看策略模式影片[📗](https://www.youtube.com/watch?v=IkG_KuMpQRM)

11/7

11/6
- 學片語
- Vivus.js [📗](https://maxwellito.github.io/vivus/)
- CSS
  - stroke-dasharray, stroke-dashoffset

11/5
- 聽Lemon tree練英文

11/4
- 聽Lemon tree練英文
  - all that I can see is ...
  - hang around
  - nothing ever happes
