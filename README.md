12/10

12/9

12/8

12/7(S)
- 初步了解Signal [📗](https://medium.com/@LeeLuciano/%E6%88%91%E5%B0%8D-signals-%E7%9A%84%E7%A0%94%E7%A9%B6%E8%88%87%E8%A7%80%E5%AF%9F-%E5%BE%9E%E8%A3%9C%E4%B8%81%E5%88%B0%E8%A7%A3%E6%94%BE-e96e4329a77a) [📗](https://ithelp.ithome.com.tw/articles/10373437)
  - Signals 是一種顆粒度度很細的響應式狀態管理
  - 它追蹤變數與使用它的函式，或變數跟DOM node之間的依賴關係。當變數改變時，只會通知實際有使用該變數的區塊進行更新。這大幅地減少不必要的reconciliation，因此可提升效能 [🔖]()
  - 不需要比較整個virtual DOM tree來得到diff
  - 不需要執行整個function component
  - 不需要使用useCallback、useMemo之類來優化

12/6(S)

12/5

12/4

12/3
- 初步了解[Awilix](https://github.com/jeffijoe/awilix)
   - Awilix是一個的DI container library
   - 輕量，所以效能也會比較好，適合中小型專案
   - 自動注入依賴的功能
       - cradle 是一個 proxy，它會透過參數名稱自動解析依賴，幫開發者自動注入依賴到需要使用的class的constructor或者function的parameter，故可以減少手動配置
       - 如果需要的話也可以自行設定成手動注入
   - 自動管理instance的生命週期，支援singleton、 transient、 scoped等方式
       - 生命週期的自動管理是為了避免重複實例化，導致消耗太多記憶體
       - singleton(單例)，全域只有一個instance
       - transient(瞬態)，預設值。每次把註冊在容器裡的東西拿出來用時，都會建立一個全新的instance。會消耗較多記憶體，但可確保instance不會被交叉污染
       - scoped(範圍)，在特定的作用域(通常是一個 HTTP 請求)內共用同一個實例
   - 學習曲線較平滑

12/2
- 初步了解依賴注入（Dependency Injection, DI）的概念 [📙](https://medium.com/wenchin-rolls-around/%E6%B7%BA%E5%85%A5%E6%B7%BA%E5%87%BA-dependency-injection-ea672ba033ca)
  - DI是一種設計模式，也是降低耦合度的手段，其目的是讓class只專注自己的邏輯，不管依賴的實作細節
  - 優點
    - 集中管理依賴，統一由DI container注入，避免四處散落的全域變數
    - 降低耦合。傳入class的依賴只要照介面走，class就不必管其實作細節 [🖌️](https://www.typescriptlang.org/play/?#code/PTAEAsBdIBwZwFwgLYFMAmBLArsgdAMYD2ywA7qgHYHiaUC0ATkQDYtz0CGz2l6wAUgCiANgEAhAOwSAgsICsAgByKZi0ROni5QxUq0z66VDCrHqAT3p0AVqgKRMRBqk4jJAJgBGnAAwBmfwJOACgQukhURgAzTgJUUABJIRZ7SEZMYJYABRZsAHNQAG8Q0FBiSko0gAoASgRQADciTHQAbhCAXzCCFk44OFAAZSICAGtUSGLS0BgMxs5I0EZXdGcWC1m8-Ibk1IcMrNyCjpmKuHTsByJGapht3ZS0w84c7drpsrLMaNBqgEJ7gUPiUvl9IOBmGRQFVoUJGMxbgByIGFQBdDoAvL0APApI2odMHdMEzMoQzBwPCo0AAXi2Jxm3RmcDM2SIFFuIOJoFJ5NRhGcVQcdXxoG6DJAoEAZ9qAHXlANNygCN0kK9fqDAASnEwjAAIowLFFjoVMMh7qg0JRIIM9s9Mq99Z9yvyavUmi10HayudWKg8CwiPlqki1RrtbrGLaKgLIuh-rjhaKes4LhB1VqdXrttSYahoYGUyH9ULFQmpnBRhMpjTYcNS5NquBk8G08DTiXxpM8Ey+Cy2QWQuL6P2B4Oh8PwmaorF4kkngdrW8Cm77ZVHQ1mq0OgylQNhvZsCscw3Q+nDcbTeap-t0rPbaCwbNsF4WJllqt1ptUY8Ly85-lhWCYPfHwIZ9ODWSgNiTOAAHEeE7B5QC8IhPU4ShTlvUBxUAXYjAD+MwBQAMAQitAHh9QAYf8ACldAC+9QBpy0ABW1AAubQBTRUAQMjAGqI7DABC3QAl40AWgzOXdItGCuSAbjuODLRnI5tgAGgg6CiF4dB9QaBCkMoDk0JJWgeXTGlUV-W9uTwOsoJg+StOk4z9V0soGTQ8Nl2dVoFzBH4-n0wyZLk-VVLUsEPVSb1fX9IYdz3etU0PAoGghBJKUM0BOFAfJjNpfI8BjMJvLBfTeVswU8R4r5CVvQqGULShEyZAhd1QfcwttCss23SqQqDWrtlrUK80krl+NQPLzmLatIE1ewbkWDAM0rEZW0gaoKqqmrOqbMIWzLYbiEYMb0HbZlWSiIUgA)
      - 此即依賴抽象，不依賴具體
    - 容易測試。可以傳入mock物件，不用碰真的DB、API
    - 容易替換。換資料庫/服務只改 Container註冊時傳入的DB client，不用四處改其他class內用到 DB client的部分
    - DI container 自動組裝參數，不用手動 new 一堆物件、取出env並傳遞

12/1

11/30(S)

11/29(S)

11/28

11/27
- 了解web vitals [📗](https://www.youtube.com/watch?v=pTswmgVWSH8)
  - web vitals是Google 提出的網頁效能與使用者體驗核心指標，這些指標會影響 SEO 排名，以及使用者留存 
  - 指標中有三個最重要的被稱作core web vitals，分別為LCP、INP、CLS

    | 指標 | 問題原因 | 改善方式 |
    |------|----------|-----------|
    | **LCP** | - 過大的圖片等資源<br>- DOM 過度肥大<br>- 使用距離使用者較遠的 CDN | - 壓縮圖片、縮小 asset<br>- 精簡 DOM、避免未顯示元素掛入 DOM<br>- 使用地區接近的 CDN 節點 |
    | **INP** | - DOM 過肥造成 reflow / repaint 費時<br>- 巨量 DOM 造成互動後渲染時間變久<br>- Virtual DOM 也無法避免瀏覽器層渲染成本 | - 攤平、精簡 HTML<br>- 減少不必要的 DOM<br>- 檢查並優化 function 的 self time |
    | **CLS** | - 元素大小不固定（圖片、廣告等）導致 layout shift | - 為圖片/廣告設置 min-height<br>- 或使用 aspect-ratio 預留空間<br>- 使用 visual regression test 找出位移問題 |

  - Google有一個叫做[CrUX](https://developer.chrome.com/docs/crux?hl=zh-tw)的使用者體驗報告，它會收集使用者使用Chrome瀏覽網頁時的資料，並以此來當作baseline，並判斷網頁的效能指標如何

- 了解甚麼是DOMContentLoaded 、load、unload [📗](https://www.explainthis.io/zh-hant/swe/fe-DOMContentLoaded-load-beforeunload-unload-difference)
  - DOMContentLoaded (DCL) 是當 DOM 建構完成後會觸發的事件。當 HTML 載入、解析完後就會觸發。可以幫助開發者偵測何時可執行 JavaScript
  - load 是在 HTML 載入、解析完，CSS 、圖片等資源也都載入好後，才會被觸發
    - load 必定是在 DOMContentLoaded 之後被觸發
  - unload是在離開或關閉網頁後，才會被觸發。通常會是用來埋資料分析使用者確切是在何時離開了網頁 

11/26
- 練習Leetcode 56. Merge Intervals解法 [🖌️](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAWwKYCcDmqAUMxQYBuAhgDYDOAXImCMgEYYDaAumwJQ12MvuuIA3gChEYxBAQUoidKgqIAvImb5C6UpWYAGVqwDcw0eOBx0OMqhkwliAIz7ENgDxOCxchQB0lsJigAFo4wANQhHCLiURJSMsj4tmoeWjDsuobR4pJg0igkAB6J7hqequx2BkaZYtm5zAAOckQAsvgANIiNqC0FAspyFMwDPqh+gYgAtPaVxpkA9HOIgGe6gC4KgLOJgFGugDD-gAJGgKdygFFGXS34gNvGgAhG8WCz0TDAOFeIrsetSABkb3mFAHzKL-gRG7VWTyIbyEZjAKTaa2ZhXDovXqGIHVbKwOioDLVAC+KLEeMQC0QgGfldbbfZHJrNAoXZAFAl3B4FRDfTpU5kfFAJZx-dn5QHAqIDMHeXz+KFTCqw-5gDp0-IzQVZBDokCYgm4glEwBJNptdntAC9ugFLjQAVxoAmBMA3coE4b1EAUAI4OHteWsDhYsSaoVWEDoJADQzY5G1OCWHxwTAPDDYR3MOxtAAsrDaOjaFVdbsJi2YKcQiYEwmDobI4cjWFw2bjieT8baAFY9BwM0SKx166wC1IQ6gwxG0GWY3GAMxJ5gAJjaADYRwAOVO6ZN2Wup6cNptZ2OTmdzkeL5d6IA)

 ```js
 function merge(intervals: number[][]): number[][] {
    const res = [intervals[0]];
     for(let i = 1; i < intervals.length; i++){
        const min = intervals[i][0];
        const max = intervals[i][1];
         const [prevMin, prevMax] = res[res.length - 1];
         // 左側重疊，所以把prevMin換成min
        if(min < prevMin && max >= prevMin){
            res[res.length - 1] = [min, prevMax];
             continue;
        }
       
        // 右側重疊，所以把prevMax換成max
        if(max > prevMax && min <= prevMax){
            res[res.length - 1] = [prevMin, max];
             continue;
        }
         // 沒重疊，所以直接推進去
        res.push([min,max]);
    }
     return res;
 };
  console.log(merge([[1,4],[0,1]])); // [[0, 4]]
 console.log(merge([[1,4],[4,5]])); // [[1, 5]]
 console.log(merge([[1,3],[2,6],[8,10],[15,18]])); // [[1,6],[8,10],[15,18]]
 ```

11/25
- 了解block element、inline element在flow layout的排列 [📗](https://www.joshwcomeau.com/css/understanding-layout-algorithms/#inline-magic-space-5)
  - 預設block element由上到下垂直排列，inline element則水平由左到右排列，空間不足時則會wrap
  - block element會參與block formatting context，inline element則參與inline formatting context
  - 相鄰的block elements之間會有margin collapsing的現象。當發生時會以margin較大的那方為主 [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Block_and_inline_layout#margin_collapsing)
  - 文字之間如果行距太小會導致難以閱讀，而文字屬於inline element，所以inline element被設計成預設有一點些空格
    - 若使用Tailwind則不會有這個現象，因為Tailwind用CSS把img變成block element [🖌️](https://play.tailwindcss.com/KbwJGDRWKZ?file=css)

11/24

11/23(S)

11/22(S)

11/21

11/13~11/20

11/12

11/11

11/10

11/9(S)
- 了解css layout modes [📗](https://www.joshwcomeau.com/css/understanding-layout-algorithms/) [📗](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Introduction#normal_layout_flow) [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_display/Flow_layout)
  - layout model可分為6種
    - flow layout
      - 預設值，又稱normal document flow、normal flow
      - 唯一有block element、inline element概念的layout
    - flexbox layout
      - display: flex 會建立flex formatting context，套用這個屬性的element的children會參與FFC，所以會變成用flexbox layout
      - 套用display: flex的inline element會被變成block element，但其children並不會變成用flexbox layout
    - grid layout
    - float
    - positioned
      - 在各種layout model中優先序最高
      - 透過position、float可以讓元素跳出flow，不再參與normal flow，而是獨自排列
      - 套用position: relative的元素是個特例，使用positioned layout，但仍然會參與flexbox layout、grid layout
    - table

11/8(S)

11/7

11/6

11/5

11/4

11/3

11/2(S)
- 了解CSS的box model [📗](https://www.explainthis.io/zh-hant/swe/css-box-model) [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model)
  - box model是元素的組成結構，由內容、內距、邊框與外距組成，分為content-box、border-box，前者為目前各大瀏覽器的預設值
  - content-box只算內容寬高，border-box則包含內距與邊框在內
  - 例子 [content-box與border-box](https://play.tailwindcss.com/tH582q5uC5)

   <img width="1434" height="573" alt="compare content-box and border-box" src="https://github.com/user-attachments/assets/49c25c83-4a82-4d48-8693-5770c0502eb5" />

   <img width="1026" height="513" alt="tailwind default - border box" src="https://github.com/user-attachments/assets/0d4171da-944f-46ce-85a3-fc9d8a05a1b9" />

11/1(S)

10/31

10/30

10/29

10/28
- 了解CSS的display type [📗](https://developer.mozilla.org/zh-TW/docs/Web/CSS/box-sizing)
  - display type是描述element再畫面上怎麼排列，分為block box與inline box
  - block、inline是控制外部的排列(outer display type)，決定元素在 in flow 下如何排列(即元素本身參與的是何種 formatting context)

   ||block|inline|
   |----|----|----|
   |換行|會|不會|
   |width、height|有效|無效|
   |margin|有效|垂直方向無效|
   |padding|有效|有效，但垂直方向的padding不會推開上下的元素，因此可能出現重疊|
   |border|有效|有效，但垂直方向的border不會推開上下的元素，因此可能出現重疊|
   |預設寬度|跟其父層一樣|自身內容的寬度|

  - 例子 [block box](https://play.tailwindcss.com/520DrTXgmX)、[inline box](https://play.tailwindcss.com/7QBhlcz7tg)
   <img width="1439" height="588" alt="compare block and inline" src="https://github.com/user-attachments/assets/e10c037e-298d-4398-9342-b77ffd8657d1" />
  在這兩個例子中都有放hr tag，仔細看的話會發現只有inline box的例子中「width不生效」、「分隔線底下的兩個元素跟分隔線有重疊」

   <img width="1440" height="590" alt="add m-2 and compare 2 inline examples" src="https://github.com/user-attachments/assets/0a54ac9a-5885-4fe5-8b9a-5cf906e556ae" />
 試試看幫inline例子中的hr下的兩個元素加上`m-2`，會發現垂直方向的margin沒生效，所以仍然和分隔線重疊

  - 例子 [用css把block改為inline](https://play.tailwindcss.com/Gwa0oXRGX2)
   <img width="1436" height="574" alt="compare span inline and css inline" src="https://github.com/user-attachments/assets/fe5ad3fd-0894-41aa-bca1-f763f72d81c5" />


 - flex與grid
    - flex與grid是控制內部的排列(inner display type)，與其底下的子元素排列有關


10/27

10/26(S)
- 想以下題目的解法[🖌](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAwghgGwMYDECuA7JUC8UAUcAXBmgLYBGEATlADRQUnlXUCUuAfFKZTQFD8A9EKjAAFgEsAzlBlQA9gGthopAozTgUJGmrUQuAgDNMSIvGTosHHNwDeqqM+oRgejAQB0PsHGpwZNLMfNQA2gC6tg5Ozs7qmtphxpLUWgAK-oEMPl6uGVlBEUZ+AUEA3LFxCVpiCsCIMAqY2nj5wJll0nkQACZoSBD4plgMKWkdhWyVVS5uHt6+WUQ8LDSR0VCOInG7Ndr5JVk9-YPDZgzA9Y3NGMDTgju7c+7UnvmVT3EAvlW-O79+PsdHoDEZzlgVpZUGZNo54hparp9JI+uDcv4AObBVahDZcLb8PaI7SSDAYGjonwUgAewBWvFY+LshOeUFcr08yIMEKQbHwGOo2Jy1IgdIeu2+M12O0Abq6AaojAJLxgAQjKBgaiSMiSYCSABuEEAEP+AaPlAEGaOkRCgQEC8CAUmMAgAyAK8DAKtKisA0eqASH-AEJmgBh-wDv6oAZCPZfQGECJcTJFOoXl1iDQEAA8sZwXDw8TNJbrbbMfgAORIRAIKCxhDxpO5hhY6QS54chZVk6h3k15y-XaRmheK4AZWAGowmJTBPhzxqmZtdrzBYQRZ7fbJmIrUCrLbidbeUF7-ZzDdcpyGIz5q7bcTTwc5cnJNEqrel54W3NRvUqUsEwLgvV64OIjJoDCYv7sMO4brp4cBQAA1IwL5viSy6fgAKgA7goRjciAhCfg8QIWlaE47ohKH4AAzPyAAsbDTFAOwAOxOGOeHZphvTIQoJF0BR+AAKyUeU1GiAAjAATPRuFZpOH4sURpH4JxPFUTsgC-8YABUqADIZUDCbBiRQGQaAIDqYAIIYeD4DSISsAwIAMmsQEsiOoFQDSUAAFRQCAME4dpun6ZIhkgKxaGghh3kGUZDw7Ax4k5iFvlGaxJHkbx-EaSJEVifh+AxX58XERx-LyXxOwAGwAAyPKIgAkpoAznqAMZpgDoSj6gBi8oAsHKAPfKgD+8oAFK4AFLdoA5oqAF96xgIHAwD2sNo0ALJwGAWm1BNwDADQngmf41ArJgSgYAoSEYMyMQItp+REFo26REYkR3sYCjUPgVqkkYJV8ZIUAADzLvoNoQAOEjPRBEFsCOh1IqC33AAAkktZBGGtYSSBEd7OJIxj4KAkAKMm3Jg5DEDQzg+NQLmp0LrmgNnnM3RgGg0jiPgWN3DjZBsGeJ7OGeyN06DDNQ5eWhwFgEAY1AACC+hwIYABkEsgvo2NQ19P3iFA3AlWTbL5F4VM0wKPgLUtbyc7L3O45RLPhoCLwLB8-CAsCFJaKLATGVAYThq7uxhLmcAVrmFC5hEdBnp7SBLp7vQ+xA-sMGEnvGD7i4B4T4j+xE4ap6nokZoxk568t+D28Ajvi6bTiAKGxgByCcRgBLnoADsqAF+KOpkILaDAHN2jGG4SDiJNChIEo4JkL3SjC+k4NEOk1AKFq0gQK9xMDpwqaWxuE9TzI1oBGc7txBSSFQKv09DPg+SWvqS-PDPwAIZqzfAPg+BsHYQO1hA0in0MuaN7fpM3s83x0MREqQDmaSjYIHXYg8+4j3BmnZmgIdgd2AF3Hufd84QD3gfde98T4IDPsBL4l9r5N2aHfB+T9ZjBjfrgj+kD+5fxIT-P4HEgGqycN8SiXZxDfWwa-VMXxIoZXyOFUQ7DypQEQcgoeaCMGT0PjwqheC7JVEITfEh99H6cG2KIXYOD9R5l0WiEs8ZGFfH-gJFhzMAQcIkNw4+vD8HaPNFnKKdjqyfBEWwIAA)

```js
type CalcFunc = (a:number , b:number) => number

const curry = (func: CalcFunc) => {
  // TODO
};

const add = (a:number, b:number) => {
  return a + b;
}

const addTwo = curry(add);

console.log(addTwo(3)(4)); // 7
console.log(addTwo(3,4)(5)); // 12

const multiply = (x:number, y: number) => {
  return x * y;
}

const multiplyTwo = curry(multiply);
console.log(multiplyTwo(3)(4));
```

```js
const flattern = (arr: unknown[]) => {
 // TODO
}

const nestArray = [
  [
    ['a','b'],
    ['c', ['d','e'], [['f','g'], 'h']]
  ]
]

console.log(flattern(nestArray)) // ["a", "b", "c", "d", "e", "f", "g", "h"] 
```

```js
// 超過3秒印出hello world，反之印出 resolve value

const fetchMock = (mockAPI:Promise<string>) => {
 // TODO
}

// 超過3秒印出timeout

fetchMock(new Promise((resolve) => {
  setTimeout(()=>{
    resolve('resolved value');
  },4000)
})).then((res) => {
  console.log(res);
})

fetchMock(new Promise((resolve) => {
  setTimeout(()=>{
    resolve('resolved value');
  },1000)
})).then((res) => {
  console.log(res);
})
```

10/25(S)

10/24

10/23

10/22

10/21

10/20

10/19

10/18

10/17

10/16

10/15

10/14

10/13
- 了解setPointerCapture()
  - e.currentTarget.setPointerCapture 用於捕獲pointer event (pointermove、pointerup等，是同時支援滑鼠、觸動板操作的事件)
  - 當調用 setPointerCapture(e.pointerId) 後，即使滑鼠移出元素邊界，該元素仍會持續接收所有後續的pointer event，直到發生pointerup或呼叫 releasePointerCapture()才會移除綁定關係 [📗](https://zh.javascript.info/pointer-events#zhi-zhen-bu-huo)
  - 優點是簡化事件處理邏輯，不需要在 document 或 window 層級監聽事件
  - 常用於處理拖曳、繪圖等需要持續追蹤滑鼠位置的互動場景、處理多點觸控時的指標隔離 [📗](https://medium.com/geekculture/building-a-simple-colour-picker-in-react-from-scratch-8ef0d3f4e9cc)


10/12(S)
- 重新了解peer dependency [📗](https://docs.npmjs.com/cli/v10/configuring-npm/package-json#peerdependencies) [📗](https://nodejs.org/en/blog/npm/peer-dependencies)
   - peer dependency用於標示該plugin(package)需要某個版本的某個package，並且要求使用該plugin的repo安裝符合版本的指定package，以解決package重複安裝的問題
     ```text
         // 如果react-router-dom跟react-hook-form都需要react，但他們都沒把react放在自己的peerDependencies裡面，而是放在dependencies，就會重複安裝
         ├── myProject
         │   └── node_modules
         │       ├── react
         │       ├── react-router-dom
         │       │   └── node_modules
         │       │       └── react
         │       └── react-hook-form
         │       │   └── node_modules
         │       │       └── react

         // 如果有正確設定peer dependency，就可避免react-router-dom跟react-hook-form都需要react時，兩邊重複安裝react
         ├── myProject
         │   └── node_modules
         │       ├── react
         │       ├── react-router-dom
         │       └── react-hook-form
     ```
   - 舉例來說react-router-dom的peer dependency有`"react: >=18"`，那如果要使用react-router-dom就必須在專案的dependency寫`"react": "^18.0.0"`，以便安裝react 18+
     - 如果硬是不安裝react 18+，接下來發生的事會根據專案使用的套件管理工具而不同
       ||npm|yarn|pnpm|
       |---|---|---|---|
       |是否自動安裝peer dependency|7+會自動安裝|不分版本只會跳出警告訊息，但不會安裝|自動安裝|
       |版本衝突時|不安裝|---|安裝，但會警告|
       |備注|||可自行設定[strictPeerDependencies](https://pnpm.io/next/settings#strictpeerdependencies)，在版本衝突時不安裝|
   - 曾經有人在 yarn的 issue中提出[要求實作自動安裝 peer dependency的功能](https://github.com/yarnpkg/yarn/issues/1503#issuecomment-950095392)，有許多人都深感贊同，但[直到目前yarn 4都沒有這個功能](https://github.com/yarnpkg/berry/discussions/6666#discussioncomment-11972498)，頂多只能在`yarn add`加上使用 [--peer](https://yarnpkg.com/cli/add#details)來安裝peer dependency


10/11(S)
- 學習一些新的好用的 CSS 屬性 [📗](https://medium.com/@onix_react/new-css-features-you-should-know-958ed1d34464)
   - @scope [📗](https://liruifengv.com/posts/css-scope/)
     - 限定 CSS 規則的作用範圍，解決了過往需要CSS module、CSS in JS才能解決的樣式外洩問題

   - content-visibility [📗](https://web.dev/blog/css-content-visibility-baseline)
     - element不在可視範圍內(viewport)，就不渲染
     - 已證實 `content-visibility: auto` 在很長的頁面可縮短render時間，因此可以優化INP、FCP [📗](https://www.cnblogs.com/coco1s/p/16373817.html)  [🔖](https://github.com/tempura327/learning_diary/blob/master/README.md#923)
     - 然而它有個小缺點，會讓scroll bar拉動時產生飄動感，不過只要用contain-intrinsic-size設定明確的height(100vh不算是明確的值) 就可解決這個問題
    - aspect-ratio
     - 控制圖片、影片顯示的比例，如此一來就不需要手動設定寬高、遮罩



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

##### 9/23
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
  - CLS (Cumulative Layout Shift)，衡量頁面在載入過程中「版面是否會跳動」 的指標
    - 圖片沒設定寬高、廣告插入導致版面跳動，這些都是CLS不佳的情況
	
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
















