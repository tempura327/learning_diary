1/11(S)

1/10(S)

1/9

1/8

1/7

1/6
- 了解stacking context [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Stacking_context) [📗](https://ithelp.ithome.com.tw/articles/10217945)
  - 元素預設會以 document flow 來排列，但當元素套用 position非static的屬性，會建立新的 stacking context，並跳脫document flow
    - 因為脫離document flow，所以stacking context內的元素、屬性變動並不會觸發reflow
  - Stacking Context 是隔離的容器，子元素的 z-index 只在父容器的 stacking context 內有效
    - 同一個stacking context的元素才可立於同樣的基準點來比較z-index [🖌️](https://play.tailwindcss.com/3wHeONfZa7) [🖌️](https://codepen.io/GaryChu/pen/wvwQWjE)
  - 常見的建立stacking context的CSS
    - position: fixed、postion: sticky
    - position: relative + z-index、position: absolute + z-index
    - opacity: 小於1
    - translate: transform
    - flex + z-index、grid + z-index

1/5
- 簡單了解Playwright Test Agents [📗](https://playwright.dev/docs/test-agents)
  - 整套由planner agent、genetator agent、healer agent組成
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



