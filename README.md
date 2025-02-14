2/16(S)

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
 

1/re
- 複習事件捕獲、事件冒泡 [📗](https://ithelp.ithome.com.tw/articles/10191970)
  - addEventListener的第三個參數用於設定事件補獲，或事件冒泡。預設為false，即事件冒泡
  - 點擊的element的父層會先執行事件捕獲，再執行事件冒泡
  - 點擊的目標element的事件捕獲、冒泡執行順序和程式碼寫的順序有關
- 看stand-up show學英文 [📘](https://www.youtube.com/watch?v=dI38GtWFihY)
  - cut the music off
  - I'd like a table for 3 people, please.
  - for real
    - I thought it was not your accent for real, but I was wrong.
