10/2

10/1
- 閱讀[1-1 為什麼你的 AI 代理總是越做越笨? 如何解決這問題?](https://app.notion.com/p/explainthisio/1-1-AI-32e2d1d1de1881a09964c280f2232174)
  - **上下文窗口(context window)** 是 AI 能同時處理與記憶的最大資料量，相當其**短期工作記憶**
    - 佔用太多 context window 的 token，會導致上下文腐敗(context rot)，這就是輸出品質下降的原因
    - AI 已知的通用知識，不需要再重複解釋。重複解釋會浪費 token
    - 不同的任務，不應該混在同一個 context window，應該要`/new`開新的
    - 使用`/status`主動檢查 context window 佔用比例，達到70~80%時，可用`/compact`壓縮 context，讓 AI 總結談話內容，然後再開新的 context window 繼續
  - AGENTS.md 和 CLAUDE.md 是給 AI 看的 README.md
    - 每個專案最多只會各有一個
    - 雖然它們很有用，但不建議把所有規範都放進去。只有那些每次 AI 代理運作時都必然會用到，且永遠不可違反的規則，才適合放在裡面。通常裡面會寫 repo 的架構、convention、
    - 在其加入指示，以要求 AI 精簡輸出。要求 AI 在 plan mode 時盡可能精簡輸出，甚至在不影響理解的前提下捨棄部分語法規範。這樣可以有效降低每次互動在 context window 中佔用的 token
  - [SKILL.md](https://agentskills.io/home) 是給 AI 看的詳細步驟、參考的資料說明書
    - 一個極完整的 skill 由 SKILL.md、script、reference、assets 組成
    - SKILL.md 由 metadata (name、description)、instruction 組成，instruction 用於告訴agent每個步驟做啥、做到哪裡記得停下來檢查甚麼、寫code時候的best practice、參考資料
    - 一開始只會載入 metadata，之後 AI 會根據 description 判斷是否載入 skill 的其他部分，因此可以節省占用 context window 的 token
  - 「如果刪掉所有 skill，這條規則(對這個專案)還應該存在嗎？」 如果是，那條規則應該放在 AGENT.md，而不是SKILL.md。因此說「真理放AGENT.md，依照狀況不同的放SKILL.md」

9/30

9/29

9/28

9/27

9/26
- 閱讀[為什麼在 AI 代理時代，越來越多設計系統選擇 StyleX](https://app.notion.com/p/explainthisio/AI-StyleX-3de2d1d1de188070a987e3f00193c72a)
  - 對 AI 來說閱讀 StyleX 跟 Tailwind 的 code 所需時間幾乎無異
  - StyleX 有 type-safe 的功能，可避免 AI 產生幻覺
    - 如果使用 Tailwind 的話，雖然原生沒有驗證 class 的功能，但還是可以利用 [eslint-plugin-tailwindcss](https://github.com/francoismassart/eslint-plugin-tailwindcss) 做檢查，以避免幻覺
    - 以上兩點搭配起來 StyleX 會更適合極大量導入 AI 的團隊。反之則還是 Tailwind 的開發體驗對人類會比較好
9/25

9/24

9/23

9/22
- 閱讀[淺談 Atomic CSS 的發展背景與 Tailwind CSS](https://blog.huli.tw/2022/05/23/atomic-css-and-tailwind-css/)
  - atomic CSS 要解決的是「一旦 CSS 規則跟 context 有關，在大型專案中維護就會變得困難」的問題
  - 優點
    - class name 變得與 context 無關，scope 也變小，因此更好維護也更好改動
    - CSS 大小是線性成長的，重複的規則都會用到同一個 class name，因此檔案大小大幅降低
    - 容易可以支援 LTR 跟 RTL 的文字排列方式
- 閱讀[StyleX 是什麼? 解決了什麼問題? 適用在什麼場景?](https://www.explainthis.io/zh-hant/swe/stylex-intro)
  - [StyleX](https://stylexjs.com/docs/learn/thinking-in-stylex) 是 CSS library。跟 styled-component 一樣屬於 CSS in JS，但是效能更好。
  - styleX 解決就近管理(co-location)、套用樣式分辨難易度(deterministic resolution) 的問題
  - 優點
    - 讓 style 放在組件旁邊 (co-location)，以方便管理
        ```jsx
            import * as stylex from '@stylexjs/stylex';

            <!-- MyComponent 的 style 就放在它旁邊 -->
            const styles = stylex.create({
              foo: {
                color: 'red',
                backgroundColor: 'blue',
              },
              bar: {
                padding: '4px 8px',
                margin: '4px'
              },
            });

            function MyComponent({ style }) {
              return <div {...stylex.props(styles.foo, styles.bar, style)} />;
            }
        ```
    
    - 解決當有多個同屬性的class name套用於一個元素時，無法一眼看出哪個 style 會被套用的問題 (deterministic resolution)
        ```html
        <!-- blue放在red後面不代表文字真的會是藍色 -->
        <!-- 必須去讀css檔，看哪個 class 優先序比較高，才能知道 -->
        <span class="red blue">title<span>
        ```
    - 透過 styleX API 建立的樣式會被編譯成 atomic CSS，故能重複使用這些class
        前項編譯結果
        ```css
        .x1e2nbdu {
            color: red;
        }
        .x1t391ir {
            background-color: blue;
        }
        .x139fjs {
            padding: 4px 8px;
        }
        .x1q9fjk {
            margin: 4px;
        }
        ```

    - 自動去重
        假設建立兩個都是控制文字變紅色的樣式，最後只會編譯出一個class [🖌](https://stylexjs.com/playground?input=N4IgggDhB0AuDOAPEAuEBLAthA9gJ1gAIAqQgQ3kPlgE8AbAU0UIDM8dNCAdEAAWvpMAVvAD0Axoh4BuLgDssuAoQAyOAOY5W7Tj2ii1mmfMX4iwQgGMcdfJQC%2B2jtxD7YOANYM58aBKbGcvKixMTyJIQA6gx01pgMhO6JABYJAMq0jAAahBB0ZDTq7ACucgAmAIThYXIRAKJl6ESwqVY4ZQlk5VQMCf6UxRBlZLAJ6D6wXbB0NNDVhHWIEAx4WN5EAO5NyYme3pRdZSkM8QPw4%2Bq7Xj5%2BmUxwvvNpyWR4CS0JAKoASiq7bXR8gAjfAjBL4HrdJhkbCMShJHAfPCPWrEUTycKELHYnFtCZUO7wACMhAAvATBIhoJY3mCABTATG45msHA4FCERm1Fk86y2PAcgDkbzKgoANEyedj7JKefYAJSyILcqWsUqWWDoHC1ACyNAAwhxcHJ1kS6fLObKpW9YMU8LUADyNABunOg7v8VIg7Ag8Dp-SJ0BYbPl9gAfHrDdhtaaHaIXWGlaqsTLlcm8dQKXCAExkrP3GkMelc9NY4Psy0q0t8-BCkXiq1yxu4hVK5s4ljqzXawiRo0xuSwbPmyulwg2u2Ol1uj13L0%2Bv39bNBkPhvvRk2D7NxhNJ5Op%2BRMJREDosMjFOhETtyDVa2qQCAjkvjhi2%2B2EOmSp3oZ1hq0O9djVNUQ-yrLEAINftNyHECv3jH9QKxRV5FTEAxRAdxrl8T0HlQDBo2UUgKHzZg2GcHh%2BDnERxDnQJDyWMwMyIGtkTzHDT3GBhDQmP1nyBdQOR4Oh0HUZJYAAWmGPAPDpABiFgAHZFMUsVCFkolsw0jT5R4CVuVGRBYEEkBhNEiSpJk2SAAYbNU%2BSWBYHS0MxSxXjKAAhASXFMsTJNeSyHMClg7KJIFQqJRzdJctz3PwDoBW8kTfIsuk8HUIE6Sswgsqy0RCCJAAWABSeVVLSjLswAVkqwgqpqurCDywqSqcvSsU1aYGGMnzzP8ulkngOg6WzAA2EbVMqgAOIrVJGwNptKwgBqG0aFNUybivWokWqi7l4GKIEOsYbqkt66TUvSzLsuuvKRsqkqysuhrnuqxrCAUqyduc7lhOoE6zL887yqunK3oUkaHvHJ7Xpemq8sm7MvrawggWKWB3DkAAVJgjMSgGUvs4K1JsqzWsxVH0e1AAFVZMFeGh-uSvrluGsaJum2b5shlnsw%2B1SFMR-mFKR8m0YxtIGGscp6cZs6ZJ57Ns1m4X2e5wbhsV9aVfehaybkVt5DQkBDBwB5kDQUxCPIShviLDUnF0EBaQ1QJLaIIjKE9B2XEoylqM9OiTQY5RT3PS81RvbtahNhl80IewOQsfwAH4ORwjJBCyDO4Xji1nylzN0COckhI0HBxJBOgykDrEJ3fT8qwdeBnXUK1gHdW5KWgb0cF9f1CWgdhEVU-xQytZ10AYDZYsQUkeFBkaCoKwgCoAZkqngrXYRg5-w1uQCtV50DIcTgRiXfs4YLJN6rRDcSdBgWHgO-mQdYSTVeABxPAyEadZ20IEXUkwAAAGAASYARd7DiTICA1MqpEBEl3gVKy0BJrVSKjfBB2Zd4KQKtAIkq9tpYKlDQJBPAiHQAUkSAAnJgg%2BYFcQ0BwTwSqNC0E0NXvQ5sL8WRN3cBAQgOAHLwFfLvT6PACS90NPyXesk6iVQAGI0MUYoyR1Be4AHkIBkEsE0Gg4jJGwUYTifhvchEiLETwIkNl6FSIgDI-Acjqr6gKnUVeRjeGmNEO-IseBv6-0noOLx2I36cS-j-P%2Bg4AFANARAqBFc4EAMQcg5cWluEmOxIgFhIA7rQFXrzDJqoyG70qiNaAVkFLTRITyZhu9V7sNXhtIpLIQmmI0YI4RT8rEgAkSAexji8ByMUfqAAIko0Z6iBHaN0fowx-TjGqjMZ0yxsBd42L6QMmwTieCyX1Io7Mk1RkFU8c2OMviImBPWCEncj9n7-h0S0ZsZRd46mzDQyaBCrIkkVgpfJY1LDLgaSSSq0ARr5VXhUhStU-mTQaflUFo1l6r0he8yq4lCH5JhmkgqGLykFUmpNGFaD0HiSXtAFB0KRrLg%2BfqIk1V8nwqXoGQ5VK-kjSqSvEaqD3lEsxTQ8FKDQUouhZ86huYGnsIUqvFeFSpqEAacuJe10mmQoKhyywgZCoyuXFZeVy47oyvwQUwV0BKoyvKZNKyBU6BgoUuwwlq9LAEPpQQgq7DswFOgLyrFFKCW2oFvgmhgYFKVSDaNKh6DoA0PJZNV1Ar5rqujfatB4No0CujVZcFgZvmQs4XyiplCCVmsVtGuF%2BU5V-MqlZSF5qao5sORWqycKS3lLDZNSwY0sXgu5VC3MhDlxhvBZ881y9FZKqJCNcSwaKnKsxWUqdrqFKhoVbW81ZL8E2WhWw6N1LxIbTBTQhSAAtTAq98EfVXhimhqCs1EksAVXV5qFXlMKjVR9cqZU0OXJ6mVNizWVPygLfJuKJ0KXEqCyaNCMWQqzVO95FLV6LtBdKqd68KUjSJdmfBcLcWYcLeCqqFKiQYpsvkyapH8lZpgwa9e4lsyoLDeBokI7qriXQ4QijtD8m0PEtS6NLGMU4boBitB3HV41ssOJKjm7KokbBVZdhNjcUCfwfShSInE35MOaJ9BxrH3Sc4ZCoky76OBhve%2Bxlk1nTSetbaglV6CHgwfXmxd5Tvk1TjVQokJGTPepofWyp3r16EFBYQgqx6am4hYOgQEwCQF2iGrJeJZRoFkHlEkzJsAf4%2BGDHgTAu9stdEGvSXmRLbOVWzE5K0iz76POSM815EnQVZv7earFnbyljRoflIj1DoUfVTdC2hkK8FGs%2BRy2qBVAwopI3yv5hUKO82jfVT5ND1vsbbQU1dCmluBjDflfbmG%2BOvqaaFtBzbSPueo5B6VInQVHvg2apegLb0osIPiteH3a3DZw8Ov51rcyfOmwNgHpLNIEJ7X84NuKfPLntRR9hZTQNlO85VfUDHEUseJXdYbDG-VcfmppULkLqXDeFYVKT%2BLJ21QU%2BijSFSSSvrunitBit8qMdDbauT6Lns9ZzSi0Tzb8FyfA2a89TamlC7DZYP5BV11y-BgighXHIVEJ%2BcZteGKHtHo%2B6gx94H8dNP7YvSHjmNJTd1T5-KSaOU0MiwwnkMW4ugMS3JFL0CgQZfgSyIruX8AFZ4H7kroxhqcoq1VqLWJaumPq41ngOpbM08OaCzD1n2OoOpZVSwnyrLE9T1VfK5TFbL3-Sx3M2GwUkkxRykknymk1TVfz0FS9cyIpCxDkzbfgs1Qe6vaFWUfOzt8xSthyuiHZjJfkld%2BDeYkZpSZj7FLqP4qzUvlBi79cjR61ZKfk7mPkfEuyq9anYeoIafRqhT3wZzaodhvjVD5cYthdBofAXYf1-PZRhjFGJMgYxWtgUptozobq%2BgLPqKNoRjWtPtGuzrQi3mtnAZNOUpwgpJYLvkPtaiSLPkevRrepVr1hwvRgDjKiOjGg-h8vlOwmNJPv%2BgVNCiit6tapRvQTbhUtStdIchSj1nmmPmvN6nyvNKGs6FwRpNnqzpNHgt-pdn-hyshjxpPtNsvvThTpPqCpViSLvuwkeqXk5rQWruCrWpOuxuRvVCBlei1pyi3gZpYUSh6rrllGru9vtv3kvnJrKnNIQEjjKrBgLAqhUuzsDiNBamCpNpOk5tXqgvmnQGXpVNupGvep6itnyrWo%2Bgqn3tClwWGhKhkSvDVIPiGtQlPp4RDmvFepigjFhmtqSh6rQu9GapVmZuwYIdpr-uoawUPgUhRiOmkRga%2BuqoZj5vRsuHGpPvDl-l1hyrpp6trnKmoSrlekRuppRpUvbjqOtmWqXqGuwavHQO1mvBRpVmaiIdQZIckPLhhjQiIQXpVMkGSi3gpM6INuqjQugUXqPkSpathlNmCpIbVPrpkfgphsNjys2pwVEdBmqq4V6ueuUefhpCIW2tSlJv%2BqgUvoVPBiMYvF4d6rxuhpyrUa-rBuzrvkkeguipClapPl6vToGBvpfkUT%2Bt%2BlPjGtBjhuBuUgLEflQnRoUZfsgbiqimxl1oVFPvLuUSyvTgQh8sUbyVQrgZiuquUfKaARShtDZsEVQrcfRpVDZiMYQsejqEQkCX4fSj%2BrcV6jWkSCoNhkGhtC%2Bh6gjHcZQtQjQnQMWjesxtajsRBjcRigzkeskDCWvHQE0lqYQF5oppVAAF5GlhpqnLzLreY0LJBcEHEiEsYCF3FplNKxmVbqHJ4RpZ4AASj6%2BCj62YzqAs-Oo2veVmPxaeEKbORKXqcapB3BEZBChe3G4phBLGDBIx-OaSfxmZK6jh7mNhaC72cmqai6VaIhsKhCUmYqdZcK5RcucBpJ7mNODO6KZBY6ZqABdqEqWpGewWyKp5rquG2U9GE2AxqKCM7GwOUuDqS8068pk%2BSJ65YK5Rwq0GSRPO9G%2BKpKkGyB-pFSnC%2B6bO-5eaQBnyCMkJI69KN5EOkhNUr6MpDSoR-a%2B5EGBh8AaZ-5jGrBxahy8%2BxFaB3GWaMqjhs%2B1CS%2BY00KFxWe-xh2WK9aThWxhaEqWqlBfmNabetaMazoQlEWmApGAJz%2BhaRIyQwG564hPJ4F68uKam9KeBXyZ%2BBCcRQF3q6KE5JG-Ri6amY075mk-5xqoaplvG-6P%2BN5mZZSDBUKixthOJZlD%2B7hhllGoa9aOGAqGK4xY6xelUDuzYzudAu8lgdobwg4gyUejUvCcYzc6gd8yE%2BsGIN42omY-QbEc41ItIoez4Q8uMz4WILEssgMlkPmRIdkLAlUtVtVesKYekBscgIA9gQAA)
        ```jsx
            import * as stylex from '@stylexjs/stylex';

            const styles1 = stylex.create({
              foo: {
                color: 'red',
              }
            });

            function MyComponent1({ style }) {
              return <div {...stylex.props(styles1.foo, style)} />;
            }

            const styles2 = stylex.create({
              foo: {
                color: 'red',
              }
            });

            function MyComponent2({ style }) {
              return <div {...stylex.props(styles2.foo, style)} />;
            }
        ```

        編譯結果
        ```css
        .x1e2nbdu {
            color: red;
        }
        ```


    - type-safe API，可限制組件的 props 只接受控制某些樣式的屬性 (e.g. 只接受color、background-color)，或者限制 spacing 必須為某些數字

9/21

9/20

9/19

9/18

9/17

9/16

9/15

9/14

9/13

9/12

9/11

9/10

9/9

9/8

9/7

9/6

9/5

9/4

9/3

9/2

9/1
- 練習Leetcode 704. Binary Search [🖌️](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAZwKYEMBOEAWAKMEAW2QC5FCiAjVTAbQF0AaRKLAc1SnMpswEoexPogDeAKERTEAGy6zUwKIgC8iAAwBuSdLnLMMdjmVrKyAHRyw7KDkQBaRAEZtOqQHccMOYjxyliAA8agZGUPxibtJSEAjIykQwACZJPmr+ygDUiACy6LbmwDJwcJh4eKHGDgpKEQD0iABM-K7R0TDAvmZ0iSlyDKoqamyYnOGRbZOImFwgmEi9qajaU4gAvuJR7Z0ExMg9yUsDgawcXBESq9EZqoiLPtkuW9JriKgyaBNXUpUmd4c+RxPVYbaIbKIzKBzJD2J5rVyxMDIOBySxwdh4NBYXB4OiwpjqJgAZiYAFYmABOJhORrMCn8fjiRHI1HFDFY7D4PFOAnEsmU5jNRnMlGoNHsjCc3E8xrE5hOBmbIA)
  ```js
  function search(nums: number[], target: number): number {
      let left = 0;
      let right = nums.length - 1;
  
      while (left <= right) {
        const middle = left + Math.floor((right - left) / 2);
  
        if (nums[middle] === target) {
            return middle;
        }

        if (nums[middle] < target) {
            left = middle + 1;
        } else {
            right = middle - 1;
        }
      }
  
      return -1;
  };
  ```
