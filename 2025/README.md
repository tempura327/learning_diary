12/31

12/30

12/29

12/28(S)

12/27(S)

12/26

12/25

12/24

12/23

12/22
- 初步了解oklch [📗](https://javascript.plainenglish.io/the-tiny-css-upgrade-that-solves-big-design-system-headaches-3d933675bf76)
  - 色彩空間(color space)是一套規格，定義怎麼用三軸數字座標表現顏色
  - 色域(gamut)是顯示器能夠產生的顏色範圍
    - 目前大多的螢幕是sRGB，Mac有部分型號是P3
  - oklch系統是新的色彩系統，由L(亮度) C(色度，越高則黑白含量越少，該色越飽滿) H(色相，顏色所在的角度)
  - 解決了以往hsl在亮度上的問題 (人類體感的亮度+-N%跟實際上的亮度+-N%不一樣，且不同顏色+-N%時體感上的增減也會不同)，讓顏色調整更符合人眼感知 [🖌](https://codesandbox.io/p/sandbox/try-oklch-4lw9xl)
  - oklch比起sRGBrgb有更廣的色域 [📗](https://tailwindcss.com/blog/tailwindcss-v4#modernized-p3-color-palette) [📗](https://dev.to/matfrana/the-mystery-of-tailwind-colors-v4-hjh)，顏色的表現力會更好
     - 但是如果螢幕是sRGB的一樣只能表達出人眼看到的35%
  - 透過l加上calc()可簡單做到亮度反轉，進而做出dark mode

12/21(S)

12/20(S)

12/19

12/18

12/17

12/16

12/15

12/14(S)

12/13(S)

12/12

12/11

12/10

12/9

12/8

12/7(S)
- 初步了解Signal [📗](https://medium.com/@LeeLuciano/%E6%88%91%E5%B0%8D-signals-%E7%9A%84%E7%A0%94%E7%A9%B6%E8%88%87%E8%A7%80%E5%AF%9F-%E5%BE%9E%E8%A3%9C%E4%B8%81%E5%88%B0%E8%A7%A3%E6%94%BE-e96e4329a77a) [📗](https://ithelp.ithome.com.tw/articles/10373437)
  - Signals 是一種顆粒度度很細的響應式狀態管理
  - 它追蹤變數與使用它的函式，或變數跟DOM node之間的依賴關係。當變數改變時，只會通知實際有使用該變數的區塊進行更新。這大幅地減少不必要的reconciliation，因此可提升效能  [🔖](https://github.com/tempura327/learning-diary/blob/master/2025/README.md#410)
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

#### 11/25
- 了解block element、inline element在flow layout的排列 [📗](https://www.joshwcomeau.com/css/understanding-layout-algorithms/#inline-magic-space-5) [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#119)
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

#### 11/9(S)
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
     - 已證實 `content-visibility: auto` 在很長的頁面可縮短render時間，因此可以優化INP、FCP [📗](https://www.cnblogs.com/coco1s/p/16373817.html)  [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#923)
     - 然而它有個小缺點，會讓scroll bar拉動時產生飄動感，不過只要用contain-intrinsic-size設定明確的height(100vh不算是明確的值) 就可解決這個問題
    - aspect-ratio
     - 控制圖片、影片顯示的比例，如此一來就不需要手動設定寬高、遮罩

#### 10/10
- 了解如何透過改HTML、CSS優化效能 [📗](https://developer.chrome.com/docs/lighthouse/performance/dom-size?utm_source=lighthouse&utm_medium=devtools&hl=zh-tw) [📗](https://yaron-galperin.medium.com/memory-matters-understanding-heap-snapshots-in-javascript-with-chrome-devtools-53abc33ef9df) 
  - 做分頁，不要把所有內容塞在一份HTML、CSS裡 [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#923)
    - DOM、CSSOM 太肥大的話，瀏覽器會需要花更多時間做reflow、repaint
  - 善用打包工具做minify
    - 縮小檔案的大小，以減少瀏覽器下載時間
  - 把DOM element 攤平 [📗](https://play.tailwindcss.com/frGPbi9PDL)
     <img width="1907" height="342" alt="螢幕擷取畫面 2025-09-09 212640" src="https://github.com/user-attachments/assets/68872db1-96e5-465f-a466-d116785b4c66" />
     <img width="1908" height="434" alt="螢幕擷取畫面 2025-09-09 221021" src="https://github.com/user-attachments/assets/59900e2e-81bd-4a65-9e09-d4396e222440" />
     以上圖中的兩個例子，都是左側效能會比較好
    - 看不到，或者變看不到的DOM element 不要掛到DOM上
      - infinite scroll
      - content-visibility + contain-intrinsic-size
  - HTML 用串流的方式傳 [📓](https://app.notion.com/p/explainthisio/critical-rendering-path-0edfc6c614334ec7b15284770d6092bd?source=copy_link#87ab7a3c39ae40e28741b856f769e589)
    - 因為 HTML 可以被逐步解析 (incrementally parsed)，所以不用一次傳整份，而是切成不同的小部分，然後以串流的方式傳到客戶端
  - 使用atom css，或者BEM，避免效能問題雪上加霜
  - CSS 放在文件最上方最上方
    - 瀏覽器在解析 HTML 時，遇到會阻擋渲染的 CSS，就會跳去先處理 CSS，然後再回去處理 HTML
    - 如果 CSS 不設計為阻塞渲染，在 CSSOM 建構完後，又有新的樣式變更，會讓畫面樣式跳來跳去，導致使用體驗很差。JavaScript 也是基於這個原因，而設計為阻塞渲染
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
- 了解瀏覽器渲染網頁的流程 [📓](https://app.notion.com/p/explainthisio/critical-rendering-path-0edfc6c614334ec7b15284770d6092bd)
   1. 下載HTML
   2. 下載CSS
   3. 解析HTML，產生DOM tree、解析CSS，產生CSSOM tree
   4. 將DOM tree跟CSSOM tree結合，產生render tree
   5. layout (reflow)，計算每個node的幾何資訊 (位置、大小) [🔖](https://github.com/tempura327/learning_diary/blob/master/2024/README.md#1121)
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

#### 5/8
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

#### 4/10
- 閱讀[[Day 11] React 畫面更新的核心機制（下）：Reconciliation](https://ithelp.ithome.com.tw/articles/10298053)
  - 當呼叫 setState 後，React 會先以 Object.is() 來檢查新傳入的 state 是否與舊的不同，如果相同的畫面不用更新，反之則產生新的Virtual DOM Tree，用於比較、更新畫面
    - 基本型別的值，Object.is()判斷值是否相同的，是的話則為true
    - 物件型別的值，Object.is()判斷reference是否相同的，是的話則為true
  - 「產生新的virtual DOM，將新產生的 Virtual DOM Tree 並與舊的進行比較，再更新DOM Tree」的流程，在 React 中被稱為 Reconciliation
  - state 所屬的父組件進行 re-render，會引起其子組件re-render，並傳入新的 props

#### 4/9
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



