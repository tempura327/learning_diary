1/12(S)

1/11(S)

1/10

1/9

1/8

1/7

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
- 看stand-up show學英文 [📘](https://www.youtube.com/watch?v=dI38GtWFihY)
  - cut the music off
  - I'd like a table for 3 people, please.
  - for real
    - I thought it was not your accent for real, but I was wrong.
