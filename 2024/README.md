12/31

12/30

12/29(S)

12/28(S)
- 學用really表示強調、委婉否定 [📘](https://ell.stackexchange.com/questions/241452/i-dont-really-vs-i-really-dont)
    - I really don't...
        - I really don't like swimming. (強調)
    - I don't really...
        - I don't really like swimming. (委婉)
    

#### 12/27
- 讀完理解React的setState到底是同步還是非同步(下) [📗](https://ithelp.ithome.com.tw/articles/10257994)
  - React 18(含)以後所有的setState都會是非同步的
  - React 17(含)以前，一般的呼叫方式是非同步的；非正規的方式則是同步(e.g. event listener綁handler)
- 讀完Redux Essentials 5

12/26

12/25
- 學用英文表達禮貌否決 [📘](https://tw.blog.voicetube.com/archives/64676/?mtc=campaign_managertoday_blog_20190423&utm_source=managertoday&utm_campaign=64676&utm_medium=blog&ref=20180423)
    - I see your point, but...
    - That's one way we can go, but what about...

12/24
- 讀Redux Essentials 5 ~Typing createAsyncThunk
    - 跟useSelector、useDispatch一樣，.withTypes()也可以幫createAsyncThunk做預先型別定義 [📗](https://redux.js.org/usage/usage-with-typescript)
      ```js
        import { createAsyncThunk } from '@reduxjs/toolkit'

        import type { RootState, AppDispatch } from './store'

        export const createAppAsyncThunk = createAsyncThunk.withTypes<{
          state: RootState
          dispatch: AppDispatch
        }>()
      ```

12/23

12/22(S)

12/21(S)
- 讀Redux Essentials 5 ~Writing Async Thunks
    - action creator回傳action物件，而thunk action creator回傳thunk function(或稱thunk)
    - thunk function內會用dispatch來送action，action會先讓middleware處理過，再送給store，再送給reducer
    - thunk function內常會用3個dispatch，分別為「把狀態切為loading」、「把狀態切為success」、「把狀態切為failed」
        - 使用createAsyncThunk可以簡化，因為它會自動產生thunk function，去呼叫dispatch送action，並做好error handling(區分request和dispatch的錯誤)

12/20

12/19

#### 12/18
- 讀完理解React的setState到底是同步還是非同步(上) [📗](https://ithelp.ithome.com.tw/articles/10257993)
    - setState的batching機制，讓setState是非同步的。每次呼叫setState並不會馬上去更新state，而是先排到queue，之後再一次更新state，減少state變更導致的re-render
    - 若子組件的prop來自父組件的state，為了讓它們的值永遠一致，所以props的更新也會是非同步的

12/17
- 讀完Redux Essentials 7
    - 了解如何用RTK Query來做mutation
- 讀Redux Essentials 5 ~Thunks and Async Logic [📗](https://redux.js.org/tutorials/essentials/part-5-async-logic#middleware-and-redux-data-flow)
    - `Redux`本身並`不處理非同步`的邏輯，因為其核心概念是一切都要pure，而非同步並非pure。非同步只發生在store之外，因此`需要透過middleware做額外的處理`，thunk就是最常見的middleware
    - middleware會用額外的邏輯處理dispatch送來的action。當中的邏輯可以是非同步，也可以是同步的


12/16
- 讀完RTK Query Quick Start [📗](https://redux-toolkit.js.org/tutorials/rtk-query)
    - RTK Query是一個撈資料、快取資料的lib，旨在取代createAsyncThunk 與 createSlice構成的用於撈資料的繁雜的code
    - 不過由於它依賴於Redux，且現在Redux的使用者不如Zustand多，所以使用者並不如React query、Axios多
    - 使用`createApi`可為`單一個url建立API slice`(內含query hook)，fetchBaseQuery則是redux/toolkit封裝過的fetch
    - 把建立好的API slice加入store的reducer，並為它設定store的middleware。`middleware`用於`管理快取`生命週期和到期時間
        - 有了middleware，RTK query就能在多個組件同時打某支API取相同資源時，自動省去重複的requst

12/15(S)

12/14(S)

12/13
- 學新的委婉說不喜歡某事物的句子[📘](https://www.youtube.com/watch?v=LfMySVL5ikM)
    - It's not my thing.
        - Alcohol is not my thing. 
    - It's not my favorite.
    - I don't particularly enjoy...
        - I don't particularly enjoy jogging.
    - I'm not (really) into...
        - I'm not really into drumstick.
- 學英文
    - grab a coffee
        - Let's grab some coffee.
        - Do you wanna grab a coffee with me tomorrow?

12/12
- 了解box-sizing: border-box和content-box的差異
    ```
    width: 30px; height: 30px; padding: 9px; border: 1px;
    ```
    前者扣掉padding、border內容區域會縮小成10×10，整個大小則維持30×30

    後者內容區域則不會縮小，整個大小則成50×50

12/11

12/10
- 讀API Reference/createApi ~ baseQuery、endpoints、reducerPath，其餘部分等用到時再查閱  [📗](https://redux-toolkit.js.org/rtk-query/api/createApi)
  - createApi是RTK Query的核心function，它會回傳API slice、action creator、用於query的hook ，其中前兩者是createApi呼叫createSlice幫它產生的
- 讀完API Reference/Generated API Slices/API Slice Overview  [📗](https://redux-toolkit.js.org/rtk-query/api/created-api/overview)
  - API slice是個物件，內含封裝fetch和cache的邏輯的reducer、管理cached data的生命週期、和訂閱的middle ware，以及其他可以跟endpoint互動的function
  - 為了效能最好整個網站只用一個crateApi，但如果endpoint真的不同，仍然可以用多個createApi，只是要記得定義reducerPath 作為unique key

12/9
- 學英文
  - crash course (速成班)
  - Someone should have ... (表達悔恨、責備)
    - I should have known he was a cheater. (我早該知道他是個騙子)
    - I shouldn't have left home without locking the door. (我不應該沒鎖門就離開家)
- 讀完Redux Essentials 4
  - 每個component都該只取取需要的資料就好
  - 使用extraReducers讓reducer可監聽其他slice的reducer
  - reducers和extractReducers的差異，前者會幫我們產生新的action物件，後者則不會，而是處理其他slice的action

12/8(S)

12/6~7
北埔旅遊

12/5
- 讀完Redux Essentials 3
- 讀Redux Essentials 4 ~Adding a Users Slice
  - 傳遞prepare function給slice底下的reducer，以此自定義action creator

12/4
- 學英文
  - It's up to you ... (取決於你)
- 讀完Redux Essential 3，並照著做一個小練習 [🖌](https://codesandbox.io/p/sandbox/epic-hill-3sryps)

12/3
- 讀完Redux Essentials 2
- 讀Redux Essentials 3 ~Showing the Posts List

12/2
- 讀Redux Essentials 2 ~Defining Pre-Typed React-Redux Hooks
  - 了解如何用slice，以及它如何集中管理action、reducer，並產出產出action creator
  - `reducer一定是pure function，且它不做非同步的事`
    - slice的reducers中的code看起來是mutable，可以這麼做是因為createSlice使用的Immer會自己幫你copy state，意味著reducer收到的state並不是原本的那份，所以不會造成side effect
  - thunk是一個function，接收dispatch、getState，可以處理非同步
    - 一樣可以再包一層變成thunk creator，或者用createAsyncThunk
  - 透過useSelector可以讓組件得到store當下的state，進而取得某個屬性的值

12/1(S)


11/30(S)

11/29
- 聽Chains練英文
- 讀Redux Essentials 2 ~Redux Slices
  - 了解如何使用Redux dev tool

11/28
- 讀完Redux Essentials 1
  - action是物件，描述要用哪個reducer、傳甚麼paylod給reducer
  - reducer是一個function，它會取得當下的state的copy，然後根據action.playload去計算新的state，並return出去讓store自己更新state
    - 之所以copy是因為要保持immutable，來減少side effect
  - dispatch是一個function，把action送去給reducer
  - store，儲存global state的地方
  - 了解如何用action creator減少重複手寫action

11/27
- 聽一篇BBC 6mins English
- 讀Redux Essentials 1 ~State Management
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

##### 11/21
- 了解甚麼是reflow、repaint [📓](https://app.notion.com/p/explainthisio/Reflow-Repaint-f1c663ad54324a6a933f75ab0b68a9b0) [📗](https://dev.to/gopal1996/understanding-reflow-and-repaint-in-the-browser-1jbg) [📗](https://ithelp.ithome.com.tw/articles/10217427)
    - reflow是重新計算畫面上的element的位置
        - 由root element開始往下計算元素的位置，越深的話計算會越久
        - reflow完必定會再次replaint
        - 變更margin、padding、display、border、font-size等和layout有關的CSS屬性會觸發
        - 以JS新增、刪除、更新DOM上node會觸發
            - 如果必須插入多個新的element到DOM上時可以`批次新增，減少reflow次數，以此效能上的開銷`
              ```
                const items = [1,2,3,4].map((i) => {
                    const span = document.createElement('span');
                    span.innerText = i;
    
                    return span;
                });

                const container = document.querySelector('.container');

                container.append(...items);
              ```
    - replaint則是外觀改變時重新渲染
        - color、visibility、outline...等只會觸發repaint
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
  - hang around (閒逛)
  - nothing ever happes
    - Every time I buy a lottery ticket, nothing ever happens — I have never won.
