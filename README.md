3/30
- 了解 assertion function [📗](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions) [📗](https://www.learningtypescript.com/articles/branded-types#assertion-functions)
  - assertion function 跟 type predicate 一樣，是一種 type narrowing 的方式 [🖌️](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAKgFgJwtAvFAzAbgFDYMYD2AdgM7BQCWJ8SqUAFEQFxECuAtgEYQICUTUIpRKxEyKCgB8giSjRZcAekVRQkKAHNWAQwQATfMTJQAZgQISGzGsl4TphUgQA2EAHTOCG+gAMkeCAoANwg9AQASAG8iAF8fXhxsV3I2dksFbGUoQCijChNAf6NASONAYHNARg1AemTsPPoqGwhGDl5eSOwoU3MG9gTsGKUVAFpBoeGR0bHxzJVtEhIeYApiU1YiPHnibBNl1YWhPDgIPABrAElqMWhGFg5uPgFp2YRgESEqUVooFrbqoQBCOQxmq02qpEAQAO5QACiCAQBAQvn8gRCYSgUVibigx2AAHJngRyOg3PEgb1epMcoBMBMAMhGAHdSShV8Psjqc6p1uhsOqkEkA)
  - 因為 assertion function 會throw Error，所以只可全域使用，不能傳給.filter、三元運算子 [🖌️](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAKgFgJwtAvFAzAbgFDYPR5SiRQDmArgIYIAm2AxgPYB2AzsFAJavxKpQAKZgC5m5ALYAjCAgCUwqMy6tYiZFBQA+RRpRosuAlEqtWM4JxZQAZuWb0LLbLfuOl9OBHoBrAJI81aCFRCWk5BRMzBGAVJW5VPigAb2woLmshKABCPQxZFLS04ERGAHcoAFEEBEYEAQADJHoITgA3CBoFABIk5gBfADooX2AAcljGDnQB+tlUqD7sRYYWdmNqjSgAbQBGABoAJj30Y72AFgBdHBW2DiRWHc3qBAHrTgAbYBkBbl5kWRwTDYjHeEAG70YpAE9x2ANwQLW9wOT2qrw+XzqHi8fgCfDhCJBYIhUKRcKAA)。它比較適合拿來[檢查有異常的狀況](https://www.typescriptlang.org/play/?#code/C4TwDgpgBFCqDOEBOUC8UDeAoGBLAJgFxQAGArgLQAkG8wSuAdgOYC+JA3DlIwIYC2EYnQYsuMXswgB+YozL8ARsi6ssWAMYB7RnSjxeIABIQANqa1ooACny9gvQgmQBKNAD5SJ81oA0UGjsHADo+QXZ1ADMyRg1gXB0oADdeUwJ7CGcUazJEJGIAJQhtJHwAHhEmZn8YgGtGLQB3RncXYl54POB4KFzkKFwerMwcXEibAEI+pDdsGBhgAAskJqgAUSQVpGsAcmmBnpj8CEimCHwoLRR5cx2XcSg1bjHJ6elggigAHy+oKbz3mEIC45vMlitGutNlddvtFh0eJZPlceAIIHcHmonqYIMAoPwQMN0KCCIQ9hQAIwAJgAzDtfNwgcQdgApXiMaAAES06KwTwA9PyoIBMBMAMhGAHdTAJHGgGBzQCMGoB6ZKwKTSQUyeWsBKy93UBmMZgsGsJeXuQA)

3/29(S)

3/28(S)

3/27
- 了解TS的structural typing(duck typing) [📗](https://www.typescriptlang.org/play/?ssl=7&ssc=23&pln=7&pc=30#code/PTAEBUE8AcFMGUDGAnAltALqVBnUBDUeDZAV0Q1OXwBsIZYjIcNYBbAOlAEFQWyKVWqAwMAUCD7NWbUG1j4AdngwALfFgDuq2ItCIA9m2j40igOYiGOADT04SNJlAHFNSBLAZ8Aa1h5URQwDAkRDUiCRHTl2ACNYZDxXKMZROA4xTwhVXGwAvUMg6hYREMUjQOE0xhxpdltQbQTGSANSLPCaABN9ZAVWEU0Q6rxY0ixOnvKsfBwcVHM9NXZS0AVEVSyDZeQueFhGWAAPfGMaWAAucrZKmgBaNMDzTMkAMQNkNZOz2DtlnFSQ2wQQSADN8Ih-AQ+vojNBzqx3FkSEocKCEtRYudgQQ+CRyJRqHRqlIWOwLplAqxkODIaAAEK0OgAbzEoFAXVQp1g1IuoEUpDY8WQAG4xABfMRUsEQxjwaA6GGs9mc7m8-mC4ViyViBGgWJMvmMmh0AC8oGZHK58nVAEYAAygcVivU4BXNPnyxWMc2W1U2hJ8gBMjudmTd3tA5oNJrFMbNfHdfTFWQAkqDGox8F0eoFcSTtKgNniBISmZBYUF8IE8EyXKDkdF5EKEkkM8a6Eoel7mn8dHpUDMaDgQoglPrYFkAVhghPcfGXJ8I80MlKQTTZRBSPELWyrWrAxqW6K9+cLGo+QLj9rMnrKPE+eBtz6LfuA8g+bag3Yz+YL6AAGYnRTe8X3jOM63NUCU0kelYDHUgAXnOsugMKFplAdQADcs1AX81D7XRsAmJQMPiLJZnmRZYB6WdlhEZ9QCw0wuSxWAuAACQMTRYBw5A7DrAwM3o5thRwLZ2zrUxGBrVAulSZ8BMUHoR2I-Rxx3SiFkUGjV0kKAHBQdAsFyQxjBYiw1ghVQYmPHF6JJfBzGrZQMCydYbO2RVVj41BQQrZZUE+WAAEdSFoQdID0sBeFBCIKFQZJcnHAxYgAK3gky9AAKXwZjHGMghlLU0y4WkrosjzQh5huGhTFAcEcByVwuAAdUHTydNARDYDiuhjhREQ0EQHxoTaZTG0YExqDYHAKV1Hlen6WAOyjUAAAp-R5Q8r2FABKKMAD4Nr9a1ts+cU9pdRaUGWnsYXNTazvVXaEjsHrU0UDZ-D5WIDAMc4lAO01juVUA+kJPRToPD9uoBT7vrwAB+N9ztAAAqUB7Q4ACAE5QD5LbqWAiUU1ujQECTF9ydYDsxRplbIKWin7tgGCwAMhAjOcTRUBNAgTW4jbXuQA7Z1C8K6HWkW7D+gGFEUPbKqWaJpphhoxiwDDpc1N79X+wHFdAO5jp148layTmCp5vm6E5HAx2QWjojlw37OiUEgpKLTFnkIIsniBCkMHAByPA+IrMy2GSUEPlAXL8u5iYDHk1YcB8dBQBMOYniyNXZsafsUkgEOYQwnSaN0l4wHeYLvnhVJolMagS7wWPkAAUWssP1JNA0Rsw2Yoj6KbTFOWwsmYmhSF+YF5KOIrncYPrO2QFvjewDMraTq0ukUEO3MkHBSGgaAPiwe3Hc5Sz8-Ohplj0VpSEaNpukHnDSmVxBp9T3iEgrAwmBEpLBCGwXwjdl7xQwMAvAYCMDFhPvNAA2gzDs61bR7TsKgpk60gx7QALocHbl3DY611rxjsAAfUCPPKh8YcDA1BnuQoI5zgcBoAYcw5CmRXQlLwrIAA5EIrhGAVy6CodQGBoqgAAEo8ioEsaw0JUh9Apj0GgqA-AuHSplBoXYioVk5KCdEfQvr+AojCMy00aKNA6ikPg3JtEZQoGsMKEVRDg1IOcWsf0cKrj1AzORXRVqPSJjtXWosjonVRtSLBAMPh8gAER9C6Ikp0-DsH83NIEmidMxA5OCUzTJNB2agFapGeintEgzBzr7XQWgPg+DwOtZYFY-pqHfowMJosA7jHsQCQoPRUL+H3lgFpLsUJoRwKMzpuJDAcNFhkIAA) [📗](https://kacper0witas.medium.com/understand-duck-structural-typing-in-typescript-and-its-downsides-5665e60bf09c)
  - structural typing指的是只認type內的成員(只認形狀)，而不認type的名稱
    - 函數導向的語言通常是structural typing，物件導向的語言則會是nominal typing
  - 其優點是只要形狀相符就能使用，零耦合

    ```js
    // codes in a library
    type LibraryUser = { name: string; email: string };
    export const sendEmail = (user: LibraryUser) => {
      // some codes
    }

    // ------------------------
    import {sendEmail} from 'a-library';

    type AppUser = { name: string; email: string; age: number };

    const myUser: AppUser = {
      name: 'Jane Doe',
      email: 'foo@gmail.com',
      age:28
    }

    sendEmail(myUser);
    ```

  - 其缺點是**只認形狀，所以可能出現意圖錯誤操作**

    ```js
    type Width = number;
    type Height = number;

    type Square = {
      width: Width;
      height: Height;
    }

    const a:Square = {
      width: 30,
      height: 15,
    }

    const b:Square = {
      width: 10,
      height: 8,
    }

    const getSumOfWidth = (width1: Width, width2: Width) => width1 + width2;

    // 可以執行，但是意圖錯誤
    getSumOfWidth(a.width, b.height);
    ```

    - 透過[branded type處理](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAQgTgQwHYBMA8AVANLAfFAXigygDIoBvKAfWoCNFUAuWKAXwCgPRIoB1AJYpgACyiFYjdEgCuAWzoQ4OAOQB3IaJW4A3N3DQAEhAEBzEcAnxk0+YuVQVIk+eDa9HAPSeogLATAFK6Ap7qAB3qAMP8IAM5QgFfKgBTqgJgJgIcRHADGAPZIEZYMNhKYUBAAHsAQqFHWqGgySADWSGlqSDhZcAJIpri4ABQc4gBuCAA2MhAs1XUNSBwAlCwkBPgDw9CRxB480ADKAI4yCHDQRBS9UBrCIiyC53rizmYWLMb3wHqcqRlZUAhMO3sHEsdxGdRCwcpUrqJugBmAAM0ywJzurlBUjQT1c3QAjABWaYcN7pTLZH67faHSgnYEXKBg9AQkRYuEI24uB401HoizdAAceIJH0spggwE28gA8gAzekSLpUzGXTQiHBUgBMCvO00I+DlUAA1KdFSqPN4oIB75UAp3KAd-VADIRoUAYvKAejNAPCGgDR1QD0yYASqI4QpF4qliq6CAAdFScHQg0iLNMPEA)，這樣可以達成 type safety，又可以維持程式碼意圖明確

3/26

3/25
- 了解TS的 branded type [📗](https://www.learningtypescript.com/articles/branded-types)
  - branded type 是指透過附加一個`__brand`標記屬性，讓同樣底層型別的值在型別系統中變成不同型別，防止意外混用
    ```js
    type Width = number & { __brand: 'width' };
    type Height = number & { __brand: 'height' };

    type Square = {
      width: Width;
      height: Height;
    }

    const a:Square = {
      width: 30 as Width,
      height: 15 as Height,
    }

    const b:Square = {
      width: 10 as Width,
      height: 8 as Height,
    }

    const getSumOfWidth = (width1: Width, width2: Width) => width1 + width2;

    // 限制了兩個參數型別都必須是Width，所以傳入b.height會報錯
    getSumOfWidth(a.width, b.height);
    ```

  - 使用branded type會增加程式碼的複雜性。故簡單的場景還是用 [throw Error](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAExgNxsgpgCgIYBciYIAtgEZYBOANIuUSRdQJSIDeAsAFCKIzBEOcogC84xAAY2XXn0RQAFlTgB3YlnUBRKiqo4ARAGE8YMHCgp0mLPQCeiAF7U4AOgMsA3Dz4BfHz6IVFhQIFRIeIgA9PTe3P68PAA2IcRiiACMAEwAzHEplqTpALTZcYg8qBjYOGB0pCxAA)，代替 [branded type](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAcg9gOwFoQE5ygXiggrgWwCM0oAyKAbygH1rDUBDBAEwC4oAiMOAZwEtgfAG4QOUAL4BuALAAoOQHoFUQJgJgejMGPHmkGIoAM1wIAxroSLlgADlAWdqBAyMAUroZNnAO6mBXZMDq2oGLtQFIqgGH-AWDlANkdAYHNARg1AemS5J1M+PU1tVGAABV4BYQgACiEGABtcCHY8IjQASnYEnR4oHPzoPmr4ZDQMCjkoKD59KGy8gqxMbAAGUsp2jqhgAAt0AHccCHmAUVR0VEyAA1qC9gASCm2IcSgeKbhcXOYcOGAoYighgDoN0plZDvE5T-lZGLMoZjCPjMLIMIoEYioAA0d3YTRQ6FGbXeUFQEGAuFQCCgDCgykIb2+UDkuXROCwUAAjAAmADMb1Jt3wFJpb2JsiUUEAUUYqQAyES5AJHGgBC3QCOUYChMCIOEorJKklUvxBCJMvhXu05OLJZkEDDVZIgA) 會更好

3/24

3/23
- 了解如何設定AWS cli
    <img width="1278" height="285" alt="files in  aws" src="https://github.com/user-attachments/assets/708aa972-744a-4a49-a47a-428174f9b933" />
    
    <img width="932" height="530" alt="AWS access portal 1" src="https://github.com/user-attachments/assets/1e336e37-7720-4815-b874-d7b13a95b61d" />

    <img width="817" height="722" alt="AWS access portal 2" src="https://github.com/user-attachments/assets/6d6dc42d-55f6-4e01-95d0-496b60d44b9d" />

  - 綠蓋住的區塊是用`aws configure sso`產生，sso_start_url、sso_region的值可以在 AWS access portal > 角色的 access key > AWS IAM Identity Center credentials (Recommended)查看

  - 黃色蓋住區塊則可在 AWS access portal > 角色的 access key > Option 2: Add a profile to your AWS credentials file 查看

  - 因為我不想每次使用aws cli指令都要傳`--profile profile名稱`，且大多數時候都只用某個role，所以我把session跟profile的名稱都取為default。這樣這樣 [AWS CLI](https://docs.aws.amazon.com/zh_tw/cli/latest/userguide/getting-started-install.html) 就會自動使用這個 profile，不需要手動指定。完成後就下`aws sso login`，就可以下aws指令了
- VS Code extension [AWS Toolkit](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-toolkit-vscode&ssr=false#qna)
  - cmd+shift+P > AWS: Connect to AWS > profile:default，就可以使用 .aws/credentials 內default的憑證建立AWS連線。完成後就可以用AWS Toolkit做一些AWS的操作

3/22(S)

3/21(S)

3/20

3/19
- 閱讀 [The unknown Type in TypeScript](https://mariusschulz.com/blog/the-unknown-type-in-typescript)
  - any 允許型別可以是任何型別。unknown 常配合各種 type narrowing 的方式一起使用，這讓它既保留彈性，同時又比 any 更type safe
  - 若為 union type 時，unknown 會吸收所有非 any 的型別
    - 因為所有型別都可以賦值給型別為unknown的變數，也就是說 `type X = unknown | string` 中的 `string` 也在 `unknown` 範圍裡，所以TS compiler 就把 X 的型別簡化為 unknown
    - 只要 union type 中出現 any，整個 union type 就變成 any
- 了解never[📗](https://www.typescriptlang.org/play/?ssl=41&ssc=4&pln=41&pc=103#code/PTAEFUDsGtIewO6QFDJBG8mgJYGdQ5IBTQgM1ABcALOPUygTwAdiCaBDSwyAY1JzdeAGxy9oeADShGcAK5owvDpFBkckACagAjnMGkOoYXG5wKc+gTJwATrkoA6UAEluHXpQKjoh0HhwAI1FIAHNFKjgqakNIRioWYmcAdRjbWPiOYRMEaztQDgBbQJxQ-SZQAFpQOUxEFHR0vRx0gjxWXhx1XjxHVHQAQVBQuDhtYgAPIuZhUgR5YW1AgVUEWw5mZg1QgtAAKQBlAHkAOVBmDlt6W2dD04jNLiNlVV44QpXQQpV4zS6yYjpSDcGy2QoEFTaGikXjpLh2CLmaKkABWeCI50uATCalqnhwGPmkAA5NxYIhkf5qBtSEjoQ8nlVKawrhjlNlttEuLi+JQCao8LQ5Is+sg3pA8Nw0UQAApYwGgAC8oAAFNLIAdKLZtgAufxa7YASiVAD59scTo4LldiGr0RqDWFDQBuVDiyVfRgDXhvWrcZXquU22wqgAGAG9QAAiSBFYhRvVRgAidlMMQ4UdAAF9Qy7UIUvT75MDHLGPq6C97fSXiN8cMJXREXBRZHJQLQAG4KjGB+W2aSt0AvfzEBjU7iCdscdgxCLpShyWyqJiscgFOLSdHI1SaOBsT1V4tOVyUYkEZh0ALBYgRShRdQTaL4UAIQTUYbEEjanpMwJyCenhCwhbheeBXrMkRqDgEy3tQz6vjQNR1EgorulK9pBtcUDktgyp2kQmramEeqSkRoSGnqtQ4aoipmnclrWvQ+EOmReZikQHoFkc0K2IefpKqAvbBthWCQGGkYxnGCbRgcRRyMQwiZjmbFcTxfElmWxCNugAAqMSEIEKLEJ4nrcWk6lCCo8DcMsNT0Nofr1pSK6kNSeARMsn6gJoxnCJcxBQlEOmJAcsI4Mwx56c+w62ZYAWQZ+eCLje6CcNwAwyi4Q4cXIHxXE+MAFIE8jcNCLQJFsOJyMwlRkLYRCUDqqAuRA1wCZGmkkY6OxZq6aGeuA1wWQJQlYchYkRtGmnSVGsmFPJinZrmBQEINgIVowa28UWfqlnG2lgCJ9S4BCwxwqVozCNId5IT5VyUJCDhfHYpBwlCMT0E16DUJQlDMHgOogN82qWHgvDUMKABejhvIUwDBHAoTANClRUaJlQuZUGgY4kYPahFEQ-X9AMgAgZOOC5ePhZQflhI4dhI7uPTANSWjFXA0DAOkszTsQlTWWwyO42FEWVAAzJUAAMjg-YUwgAMQkAgqPjRjcA1S5-RgCcxBdrYWugAAQsZHBxaAwWsKF+PcElmx2F42U+WoOTrlkjABFIlK02UHChClYAkAF7BRLZHDXpB6TMK0n7cAgMSvGMpAmKEYhZMI8QvNZhMbKwkDOAAYvkkzTLM11wdYeJ8myVmmKA86LpATXsRK3AkHrABKxALkuBB4catGgOGyCgKA6DNk9ND1bkPCUuo93GBoN4j5PFJK6AACitj1SGUYDMICAcO70RT57bcKvXPdRnmvUG+Pg6dt2y76S5A7yCOAgTqdKr92aZ-6+gccxDvg+CoAgk5BQLG0H-KcmxPzOD0mwGEKh9T1mEKAZYEQLhgXipcYs2gfC0h4qADsWR5IAzdBxbgBYABqpDSDKj-p3buEpv4HVAAACQ4B2TkRgyCV35KAaBF9XjINivQPhaC45eR8lkbYEQELvmhEhKOAUxAPRKKICodJ9J7C4RwK21M66OQ+OuTQEQMpZXdLlQEM5uSFFKD9QRtcxGckpk3fqJDRCPEoMQLaAkVRxVsHqLaP9B7D1wBQAJ1xjRDxHiPYRdlAR7RMQAQkVMqKMJwOAnCjK6EeWZUAj0GEWWwfwcQ3SUS1PA7sfGFDLtFROmJELDj-uE76OdPzSEAeDL4XBwb7iUQklqSJGFdwbr0QpdcxlLkEbrQETDxmsOQDfCICCKqkB8uoSAgh+RtAej4rk7hEn2DcpBWyWD7K4AaGAP8pU0iGHSKAT88hQjvjYMoVcniuxgNULokhBiIovnuYERgERBwvFJMMOQlwVA+LHFwUU6BBo8J5PiQkcEenCIINAtOiACCDhuhwTQZj0BEr+FXWMaC3hOw0OcPy-ACDdPfBA4UUDnGkFAuBJIqzy4nUSRItQ+QVH0GBJyZYv0FSAm3l8NgeBfZsEkIiewIg6CclaPIWwDKF6+CgrMAg+QTDqwmeY4hgJ4gXmYMKS4iTBX2D-tIZ8N1ErJUOQUCIeAEI9OfJMaklg+RdmcOvRwoRHBl25HM2w5quDvgaXrAKiKwDsMBMQM864nmQFyqYtNPrTaShwF2fwnrqDXUjQUYlcjSWzIQIQCKAiKn6U-JmlU3xGC2R0sKcKAB+Q0qBG2FFAPnHICpYmgHbnQYgiqR7t1oLuHyWh6qQEnaAahBJZiUCXUmDg+BGCKoKc3D0ZAh22AADJcA0FkkxeFD2IEBHqQdN7bChJHR6wQPSVTXoQICGJ4SR7KHoAOo9jgx2fR-XEhJUZgNGFsHIEoKd4BytyaBv9pB72fpuNOsYid51ECanEsD0zVAQZnVhzQC61BSrkHB4guVEN4eQwBh9jgV1wDXbhvDUzmHRmY35KZQDPyBA8HBFQGY8lxPo6hpJm7t1sbw+B42HJzzJsgNsvAiHQObNNsIRqoHf2UNAAAfRzX6-NxAADCMRxB6mgcqD960dMcYbgZozeauzmeMtAUTBSVnoAAJpv1fNkD8RzYZbFmPYKV+Q5WMFceOGQGqq0RFs-YFqmd2XZUgHrHx2gNA3T-gm0AOs9ZXIwLsg2QxoHPnRB8GgnImV8tNneb4fJ2TpymYUOAXZtB1XeBEIwLVaj8lFC1QrgIXB4E7u1zrAlSKcgAD6zKK-NjNxQ7NNhbG-Q10ACh3IYIkW1BWI1jYmx1gKr82z0HhZQCIk5KvdVAEt3Kywbjm15c+ZYygzbgKFIsBbgJs6wNUNyaDoqTHvdzaQcFNd3BgVKMuKIgh8tRWsMQLgLrnxxW0EYEwE5VDF0KDMYgOpxTkv5FkHGrB3JAA)
  - never 代表永遠不會發生的分支
  - 當函式在某些情況下必定是異常、會throw error（而不是return value），把它標記成 never 是有用的。這讓TS型別系統能夠在靜態分析時理解：這個函式之後的程式碼是不可達的（unreachable），並正確縮窄後續的型別。
    ```js
    // 沒有回傳任何東西，所以回傳值型別是never
    const neverReturns = () => {
     // If it throws on the first line
     throw new Error("Always throws, never  returns");
    };

    // 因為neverReturns的回傳值是never，這暗示永遠不會執行到if之後的分支，如果真的執行到了就是有異常
    // 所以validateUser回傳值的型別會是boolean，
    const validateUser = (user: User) => {
     if (user) {
      return user.name !== "NaN";
    }

    // 如果把這行刪掉的話，TS會報錯 "Not all code paths return a value."，
    // 所以一定要return never 或 false，
    // 兩者差在前者暗示發生異常，後者只是普通的flow
    return neverReturns();
    };
    ```
   
  - union type 中出現 never 的話會被自動移除掉

3/18

3/17

3/16
- 了解const enum [📗](https://www.typescriptlang.org/docs/handbook/enums.html)
  - const enum被編譯後會變成值，而不是維持物件。普通enum編譯後仍然有物件存在
    ```js
    // 編譯前
    const enum Direction {
      Up,
      Down,
    }
    
    const d = Direction.Up;
    // -----------------------------
    // 編譯後enum直接被移除，d直接使用值，而不是從Direction查找
    const d = 0;
    ```

    ```js
    // 編譯前
    enum Direction {
      Up,
      Down,
    }

    // -----------------------------
    // 編譯後enum變成物件

    var Direction;
    (function (Direction) {
      Direction[Direction["Up"] = 0] = "Up";
      Direction[Direction["Down"] = 1] = "Down";
    })(Direction || (Direction = {}));

    const d = Direction.Up; // 仍然是物件存取
    ```
  - const enum優點是在runtime不用查找，所以效能較好。反之缺點是無法使用反查的功能
  - const enum的值一定要常數或者可以在compile time計算的值
    ```js
    // 以下的方式都不合法
    const x = 1;
    const foo = () => 0

    const enum Direction {
      Up = x,
      Down = foo(),
    }
    ```
- 要發布給別人用的 library，不應該 export const enum，因為使用者的編譯工具（Vite、Babel、esbuild）通常是逐檔編譯，無法跨檔案讀取，這會導致編譯失敗
  - 逐檔編譯是指編譯每個檔案時只看這個檔案本身，不去讀取其他檔案的內容。逐檔編譯速度快（可以平行處理、只重編有變動的檔案），但代價是無法使用需要「看別的檔案才能知道值」的功能，const enum 就是典型案例。
  - 相對於逐檔編譯，tsc 會先把所有檔案一起讀進來，建立完整的型別圖，才開始輸出，所以能做跨檔案的分析和替換。

3/15(S)

3/14(S)

3/13

3/12
- 閱讀[兩個世代的軟體開發碰撞: 大師 Martin Fowler vs. 大神 Peter Steinberger 的 AI Coding 觀點對比](https://blog.aihao.tw/2026/02/28/fowler-vs-steinberger/)

3/11

3/10

3/9

3/8(S)

3/7(S)

3/6

3/5

3/4
- 看[cloudflare worker是什麼？零基礎教程](https://www.youtube.com/watch?v=2BfZO_LT6jA)

3/3

3/2
- 閱讀[如何設計前端登入機制?](https://www.explainthis.io/zh-hant/e-plus/blog/frontend-login-design)
  - 驗證分為session-based、token-based
  - session-based有狀態，狀態由後端管理。組合為session + cookie
    - 步驟
      1. 登入成功後，後端建立session，並回傳session id給前端。session id 會放在 HttpOnly Cookie
      2. 打API時，瀏覽器會自動帶上存在 Cookie 裡的 session id 傳給後端
      3. 後端去DB找有無對應session id 的 session，有的話回 response 給前端
    - 缺點為有被 CSRF (跨站請求偽造) 的風險
      - 雖然可以透過後端在 header 設置 `SameSite` 處理這個問題，但部分老舊瀏覽器不支援 `SameSite`，所以仍有隱憂
  - token-based無狀態，為JWT token
  - 實務上會用混合模式，組合為access token + refresh token
    - 步驟
      1. 登入成功後，後端回傳 access toke (放localStorage 或 cookie) 和 refresh token (常放在 HttpOnly Cookie)
      2. 打API時，前端手動在 Header 加上 Authorization: Bearer <access_token>
      3. 後端拿到`Bearer <access_token>`後會先decode，再去對比header, payload, signature
      4. access token過期了，前端打取得refresh token的API，瀏覽器會自動帶上存在 HttpOnly Cookie 裡的 refresh token傳給後端
      5. 後端去DB找有無對應的refresh token有的話，回新的access token給前端
    - 有負載平衡系統的架構下，因為不同server都有同一把private key，因此都能對比signature的部分來判斷是不是自家發出的token
    - 此法可兼顧速度(decode access token，並對比是否合法很快)、安全(refresh token 存在 HttpOnly Cookie，不可被JS操作，因此不會受到XSS攻擊)
  - 如果使用RSC的話，access token 也只能放在 cookie (但不一定要 HttpOnly Cookie)
  - 如果前後端網址在不同的 domain
    - 那 HttpOnly Cookie 是無法被在前後端間傳接的，因此 refresh token 勢必無法只能放 localStorage 或 一般 cookie。如此就有被 XSS 的風險
    - 如果可以調整到「subdomain 不同，但同domain」，則只要設置 `Domain` 就可解決 [📙](https://www.threads.com/@chc_web_dev/post/C64DoDLhgyq)
    
3/1

2/28

2/27
- 閱讀[Day 11 - Next.js 13 App Router ：什麼時候適合使用 Server Components 或 Client Components？](https://ithelp.ithome.com.tw/articles/10316916)
  - RSC 的優點
    - 只在 RSC 中用到的程式碼、依賴， 在 server side 渲染完組件後，不會被傳回 client side，因此可以降低 client side 需下載的 JS 大小，加快頁面 initial loading (可提升FCP、LCP)
    - (如果是靜態渲染) Next 預設會在 build time 渲染頁面，並快取渲染結果，假如收到相同 request，就可以重複使用渲染好的靜態檔案，以減少重複渲染次數
    - API key, access token等敏感資訊可以藏在server，避免暴露到client side
  - RSC 的缺點
    - 無法使用browser API、React的hook、context，所以是靜態的，無法跟使用者互動
    - 因為無法用React context，所以(直到目前的Next.js 16) 無法使用 CSS-in-JS
    - RSC傳給React Client的props必須是可序列化的，所以不可以傳function, class給React Client

2/26

2/25
- 初步了解React Server Components [📗](https://ithelp.ithome.com.tw/articles/10316478)
  - RSC跟SSR無關，而是跟React Server有關
  - React Server 指的是渲染 RSC 的環境
    - 任務是跟後端API互動(就像Remix的loader function)，並生成 RSC，再將RSC以props的形式傳給React Client
    - 可以跑在build time，也可以跑在server
  - React Client 指的是接受與使用 React Server output 的環境
    - server 和瀏覽器上都可以運行。假如跑在瀏覽器上，主要任務會是操控 DOM；跑在 server 上則是產生初始的 HTML

2/24

2/23
- 閱讀[前端打包工具 (bundler) 是什麼? 為什麼要用?](https://www.notion.so/explainthisio/bundler-2b02d1d1de1880b986f9fef469470d44)
  - 在JS剛被完成的時候，並不支援模組化
    - 直到Node.js興起才有了CommonJS規範，後來又出了AMD、UMD等規範，直到2015年JS官方才正式將ESModule定為標準
    - ESModule推出以前，只能用script tag引入JS檔案，但這導致「全域變數污染」、「載入順序(依賴關係)」的問題
    - 就算真的人工妥善地管理變數、依賴關係，仍然有「單頁面需要發多個request才能把所需資源都拿回來」、「重複拿資源的問題」的問題
  - 以[純HTML、JS、CSS構成且未經打包的網站](https://tempura327.github.io/Apetment)為例
    - 從[source code](https://github.com/tempura327/Apetment/blob/master/index.html)、下方影片可以看出前2個問題
    - 影片可以看出後2個問題

      https://github.com/user-attachments/assets/a7bfb712-da1b-4b57-b17a-306d20d09fcb

2/17~2/22 過年休息

2/16
- 閱讀[前端建構工具 (build tool) 是什麼? 為什麼要用?](https://www.notion.so/explainthisio/build-tool-2942d1d1de1880b29d59ffe4d598e686#2942d1d1de1880daa24cf82c95793428)
  - 建構工具是裝了多種用於優化程式碼的工具的工具箱(e.g. vite)，而打包工具、編譯工具都只是其中的一種工具
    - 通常建構工具都能開箱即用，且曾寸進良好的開發體驗
    - 建構工具的config內設定plugin可啟用其他功能，例如 [vite-plugin-svgr](https://www.npmjs.com/package/vite-plugin-svgr) 是一種把svg轉換成React component的plugin
  - 打包工具 (e.g. ESbuild, Rolldown, Turbopack)
    - tree shaking，把沒用到的程式碼篩掉
    - code spliting，讓使用者每次進入頁面只載入需要的檔案
    - minify，把程式碼壓縮，以減少需要下載的檔案容量
  - 編譯工具 (e.g. Babel, SWC)
    - 轉譯（transpilation)，把.jsx, .vue, .svelte、.scsss等檔案轉換為瀏覽器可運行的.js, .css
  - Vite在開發環境做的是預打包(pre-bundle)、產品環境的才是真的打包
    - 預打包是指把CommonJS、UMD等的別種格式的JS轉成ESModule
    - 因為開發環境是預打包，所以HRM才會很快

2/15(S)
- 了解useEffect執行的時機 [📗](https://ithelp.ithome.com.tw/articles/10321575) [🔖](https://github.com/tempura327/learning-diary/blob/master/2025/README.md#58)
  - useEffect 會在每次 commit phase 後被執行(DOM繪製好以後) [📗](https://react.dev/reference/react/useEffect#parameters)
    - > your Effect will re-run after every commit of the component 
    - > If your Effect wasn’t caused by an interaction (like a click), React will generally let the browser paint the updated screen first before running your Effect.
  - React使用Object.is()來判斷useEffect、useLayoutEffect的dependecy是否有改變，有改變的話就執行callback
  
- 了解useLayoutEffect [📗](https://react.dev/reference/react/useLayoutEffect)
  - 在DOM繪製好以前就被執行
  - 使用useLayoutEffect做set state，會阻塞瀏覽器進行replaint，所以對效能有衝擊。官方不建議使用 
  - 使用useLayoutEffect做set state，會使得其餘所有的useEffect、useLayoutEffect馬上被執行

2/14(S)

2/13

2/12
- 了解後端專案的分層[📙](https://medium.com/@harshgharat663/understanding-handlers-services-repositories-middlewares-request-context-in-backend-2977539931d9)
  - 基於需求不同後端專案的分層設計都會有點不同
    - 所以有時候handler會改用controller，或者分層會多出mediator、middleware等層
    - 所以有時候會有雙層handler(HTTP handler + business handler)
  - request的lifecycle
    1. 前端發request，DNS解析得到ip後，打到server
    2. router對比路徑
    3. router分工給 HTTP handler
    4. HTTP handler叫Business handler處理request，business handler叫service處理完回給它，它再返回response給HTTP handler，HTTP handler再返回response給前端
  - handler的職責
    - request object內有parameter、body、headers之類的資料，HTTP handler會從request object裡取出parameters、body
    - HTTP handler把body裡的內容從字串轉成物件，並檢查前端該傳入的值是不是都有、都合法，或者把前端傳入的值做轉換
    - HTTP handler呼叫business handler，business handler叫service
  - Service的職責
    - Service裡裝的是純邏輯，它不會跟HTTP、資料庫有任何接觸
    - Service只加工組裡來自handler的資料、flow的安排、呼叫Repo
    - Repo的職責
  - 操作資料庫，並返回結果給Service


2/11
- 了解為什麼要幫GitHub Actions做快取 [📗](https://oldmo860617.medium.com/%E6%B7%BA%E8%AB%87-github-actions-workflows-%E7%9A%84-cache-%E6%A9%9F%E5%88%B6-f63db6f7929a)
  - 導入快取機制，可以達到沒有必要時就不用重複安裝依賴套件、重複執行專案的 build ，以此盡量減少 CI 的執行時間
    - 以前端而言，常用來快取 node_modules 或 build 結果
    - 可以使用官方提供的 [actions/cache@v6](https://github.com/actions/cache)


- 快取行為及限制
  - GitHub Actions 可以 access 與 restore 當前分支、base分支的快取 [📗](https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching#restrictions-for-accessing-a-cache)
  - (免費版)一個Repo中快取檔案的上限是10GB，超過容量、超過7天未被使用的快取會被自動刪除
  - 找快取的步驟
    1. 去找符合key的快取
    2. 找不到的話去找符合 key 的一部分的快取
    
    3. 再找不到的話再使用 restore-keys 去找快取
    4. (需自行設置條件)都找不到的話就執行 install 或 build
        ```
         - name: Cache node modules
           id: cache-npm
           uses: actions/cache@v4
           env:
             cache-name: cache-node-modules
           with:
             # npm cache files are stored in `~/.npm` on Linux/macOS
             path: ~/.npm
             key: ${{ runner.os }}-build-${{ env.cache-name }}-${{ hashFiles('**/package-lock.json') }}
             restore-keys: |
               ${{ runner.os }}-build-${{ env.cache-name }}-
               ${{ runner.os }}-build-
               ${{ runner.os }}-
               
         # 設置條件才會只在 cache miss 的情況下執行
         # 如果有用setup-node，且有設定cache，那就可直接把global package data放到node_modules，不然就要從npm registry下載
         - if: ${{ steps.cache-npm.outputs.cache-hit != 'true' }}
           name: List the state of node modules
           continue-on-error: true
           run: npm list
        ```

- [actions/cache@v6](https://github.com/actions/cache)
    - 用了的話，除了執行`restore cache step`之外，最後還會自動執行一個`post cache step`
    - 傳入
      - path，要存入快取的內容所在的路徑
      - key，用於唯一標識快取的key
      - restore-keys，cache-miss時使用的fallback key
    - 如果cache hit，會顯示`Cache restored from key: {key}`
    - 如果cache miss，會顯示`Cache not found for input keys: {key}, {restore-keys}`，且在`post cache step`會顯示`Cache saved with key: {key}`
    - 搭配[actions/setup-node@v6](https://github.com/actions/setup-node#caching-global-packages-data) 一起用可以達成best practice
      - setup-node負責cache global package data，cache負責cache node_modules
      - 如果執行`setup-node step`時cache hit，會顯示 `Cache restored from key: node-cache-{runner os}-{package manager}-{hash}`

2/10
- 了解transform: translate [📗](https://www.w3.org/TR/css-transforms-1/) [📗](https://ithelp.ithome.com.tw/articles/10362313)
  - translate 是用來達到位移效果的。它**只是視覺上的位移**，不改變元素在document flow中的真實位置 
  - 因為translate只移動視覺位置，所以實際上在document flow內的真實位置並沒改變，所以真實位置沒改變就不會觸發reflow，只會在compositing階段做視覺上的位移

- 了解Gecko rendering [📗](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Fundamentals)
  - Gecko是一個瀏覽器渲染引擎，它優化了對HTML、CSS、canvas的渲染。Gekco的優化減少了因為scroll之類事件產生的repaint
  - 簡單的場境會使用系統圖形合成器(system compositor)的專用硬體渲染，一些複雜的場景則會使用GPU渲染，以提升效能
    - 使用了animation、transform: translate 的話，視複雜度可能會由GPU渲染

2/9

2/8(S)

2/7(S)

2/6

2/5

2/4

2/3

2/2

2/1(S)

1/31(S)
- 了解為何position: absolute會導致崩塌
  - **建立stacking context跟跳脫document flow無關** [🔖](https://github.com/tempura327/learning_diary/tree/master?tab=readme-ov-file#16)
  - 先不提加上z-index來建立stacking context [🖌️](https://play.tailwindcss.com/lVy997dVWQ)
    - 只要[position: absolute](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position#absolute) 就會跳脫document flow，這就是導致崩塌的原因 
    - <img width="1908" height="752" alt="螢幕擷取畫面 2026-01-31 170042" src="https://github.com/user-attachments/assets/3c4f91b1-3e25-4ad6-8f3a-dd1257e1aa86" />

1/30
- 了解sticky [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position#sticky) [🖌️](https://play.tailwindcss.com/EE7BahkKVO)
  - sticky元素會建立stacking context [🔖](https://github.com/tempura327/learning_diary?tab=readme-ov-file#16)
  - 排的依據是外層最近的可滑動的**block** element [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#1125)
  - sticky不會因為外層元素使用position: absolute/relative + z-index被影響產生偏移，但是會被transform: translateY() 影響 [🖌️](https://play.tailwindcss.com/8a1jkEj5kD)
  - 導致sticky失效的原因
    - 外層元素有 overflow
    - 外層元素的高度沒有大於要sticky的元素
    - 沒有幫sticky元素設置top或bottom

1/29

1/28
- 了解為什麼DB會踩不到index [📙](https://medium.com/johnliu-%E7%9A%84%E8%BB%9F%E9%AB%94%E5%B7%A5%E7%A8%8B%E6%80%9D%E7%B6%AD/database-%E5%85%AB%E5%80%8B-index-%E7%B4%A2%E5%BC%95-%E7%84%A1%E6%B3%95%E7%94%9F%E6%95%88%E7%9A%84-sql-%E5%AF%AB%E6%B3%95-cdc7d2e72f51)
  - B tree是有階層結構的，必須一層一層往下走
    - 多個條件時，某個條件的欄位沒有設index
    - 複合式 index 使用順序錯誤
  - B tree裡的每個節點都是一個具體的key(正面表述)
    - 傳入負面表述的條件 (e.g. NOT, !=)
    - LIKE語句中%的位置在開頭 (e.g. '%abc', '%abc%')
  - B tree裡的每個節點存的是欄位原始值
    - 使用函數語句包裝作為條件的欄位 (e.g. UPPER(name))
    - 對欄位做運算 (e.g. 1+1)

1/27

1/26
- 了解function overload [📗](https://www.typescriptlang.org/docs/handbook/2/functions.html)
  - 有時候我們會需要把function定義成可以被以多個不同數量、型別的參數呼叫，或者回傳不同型別的值，此時就會需要用到function overload
    - 用function keyword宣告的function，使用一般的overload function即可
      - <img width="639" height="812" alt="overload signature" src="https://github.com/user-attachments/assets/e4cd09d0-dcec-413c-8e6a-590473da0816" />
    - arrow function不支援overload signature，所以必須使用call signature才可達到同樣的效果 [](https://blog.logrocket.com/implementing-function-overloading-typescript/)
  - 至少要有2個overload signature，且實作一定要兼容所有overload signature
  - 如果2個overload signature的參數數量都一樣，且回傳值型別一樣，那應該使用union type改寫成non-overloaded function [](https://aaronbos.dev/posts/function-overload-typescript)

1/25(S)

1/24(S)

1/23

1/22

1/21

1/20

1/19(S)
- 閱讀[資料庫索引 (database index) 是什麼? 如何選擇加在哪個欄位上?](https://www.notion.so/explainthisio/database-index-2cc2d1d1de188008a045c4b70e665c5c)

  - 建置index是為了讓搜尋的效率更好
    - 沒有特別設定index的狀況下，資料庫會掃過每一行，然後把符合條件的資料找出來，相對沒有效率。tree資料結構就是為了解決這個問題

  - B-tree
    - 它的每個節點比binary tree帶有比較多的鍵，雖然節點越多越佔空間，但是控制在一定數量下，不會帶來太多額外成本
    - 它減少了讀取磁碟的 I/O 所需時間，所以比起二元搜尋樹，是個讓搜尋能更快完成的資料結構

  - B+tree
    - B-tree的改良版，用於解決B-tree根據範圍搜尋的弱點
    - 在最底下的子節點外的節點都有重複出現
    - 分為內部節點 (internal nodes) 與葉節點 (leaf nodes)，內部節點只會作為指標 (pointer)，指向最終的葉節點，具體的值只會在葉節點
    - 因為內部節點通常容易快取，實際發生大量 I/O 的地方是葉節點，當這樣設計就能有效減少讀取磁碟，讓整體的速度更快

  - 為什麼不直接幫每個欄位都建index？
    - tree是一種用空間換時間的方式，且每次寫入資料也必須更新tree，如果建太多index會導致寫入變很慢

  - uuid當primary key是好主意嗎？
    - primary key本身就是一種index
    - uuid v6以下的版本因為uuid的值是隨機的hash
    - 如果拿hash當index的話，可能會導致寫入時更新tree更花時間

1/18(S)

1/17

1/16
- 閱讀[如何有效通過試用期、降低被 PIP 的風險](https://www.notion.so/explainthisio/PIP-27f2d1d1de18801b8281fd00028333f7)
  - 沒有做對的事
    - 「對的事」是指團隊、直屬主管對你的期待
    - 了解績效是如何決定的，這跟所謂的「對的事」有關
    - 在前期可跟直屬主管約談，頻率盡量做到一週能一次 ，以快速得到反饋並修正。待久了以後最好也維持三個月約談一次

  - 與團隊協作
    - 觀察在團隊中評價好的人。如果不知道誰評價好，可以直接問直屬主管，或者團隊成員
    - 先建立信任，再引入、推動新的計畫

  - 快速了解系統，並有產出 [如何快速上手程式碼庫](https://www.notion.so/explainthisio/2392d1d1de18800fb865f231313f3d9f) 
    - 不要花時間讀所有技術設計文件、source code。在選擇要讀的內容時，以最新的為主，藉此了解近期有的新設計或變動
    - 如果團隊有留下技術設計的文件（為什麼那麼設計、嘗試過但不採用的其他方案），閱讀那些文件了解設計概念後會比較好理解程式碼
    - 使用Deepwiki等AI協助理解程式碼
    - 
1/15

1/14

1/13

1/12

1/11(S)

1/10(S)

1/9
- 了解absolute、relative 移動的基準 [🖌](https://play.tailwindcss.com/vsR4F2speO) 

  https://github.com/user-attachments/assets/65e79d81-25e8-4972-ad7d-1ce77f509614

  內層的element會以外層element為基準一起移動

  https://github.com/user-attachments/assets/7c422e7b-87b3-4e12-957c-b9af4481a87d

  https://github.com/user-attachments/assets/de2309d7-0fda-4c33-a401-20b7149d0433

  如果是外層relative，內層absolute，或者反過來，都是內層的element會以外層element為基準一起移動

1/8

1/7

#### 1/6
- 了解stacking context [📗](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Stacking_context) [📗](https://ithelp.ithome.com.tw/articles/10217945) [🔖](https://github.com/tempura327/learning_diary/tree/master/2025#1125)
  - 元素預設會以 document flow 來排列，但當元素套用 position非static的屬性，會建立新的 stacking context，~~並跳脫document flow~~但**不一定會跳脫document flow**
    - 若脫離document flow，stacking context內的元素、屬性變動並不會觸發reflow
  - Stacking Context 是隔離的容器，子元素的 z-index 只在父容器的 stacking context 內有效
    - 同一個stacking context的元素才可立於同樣的基準點來比較z-index [🖌️](https://play.tailwindcss.com/3wHeONfZa7) [🖌️](https://codepen.io/GaryChu/pen/wvwQWjE)
  - 常見的建立stacking context的CSS
    ||position: fixed|postion: sticky|position: relative + z-index|position: absolute + z-index|opacity: 小於1|translate|flex + z-index|grid + z-index|
    |---|---|---|---|---|---|---|---|---|
    |建立stacking context|○|○|○|○|○|○|○|○|
    |跳脫document flow|○|×|×|○|×|×|×|×|

1/5
- 簡單了解Playwright Test Agents [📗](https://playwright.dev/docs/test-agents)
  - 整套由planner agent、generator agent、healer agent組成
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











