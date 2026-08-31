8/31
- 練習練習Leetcode 3. Longest Substring Without Repeating Characters [🖌️](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAGwKZgOZQBYHlgAyCGqAzlAMogBG5ATjJgBSkBci9jGAlO2CAFtqqOogDeAKESIICcojBwoqRAF4FqAO6IKqKE24BuKSj0dkcTQEkwAE1QAPNYgAMx6WiiIBAQwcF0LGxnNwkTYDhRJk9EGBDDWMQAHg4AOjRMHASYAGoc7nETaWlZMHkIEDpRdQADABIxUgBtGABdAF8a4yLizWwYNEQmRWVU7B9SJgqq7gLJYoXikdRU+09UFibSC2s7R1ajHsXzSxt7Jxz1AEZ3Rfaw4+XUn1tbTbbD499-QJxnAFkfDhUt8mN8AplsAAaRIAWhOu3OiByiCun0Q9xMdD0lSQ4N+2GM7UMQA)
 ```js
  function lengthOfLongestSubstring(s: string): number {
    // 有紀錄的最大長度，作為最後返回的答案
    let maxLength = 0;

    // 紀錄，用於檢查當下指到的元素是否重複
    const note = new Set();
    // 指著不重複的子字串的左側， 會跑得比右側的index慢
    let slowIndex = 0;

    // i為右側index
    for (let i = 0; i < s.length; i++) {
      const curr = `${s[i]}`;

      // 如果note內找到curr，就並把slowIndex往右推一格，與此同時也要更新note，所以刪掉note內跟slowIndex指到的元素相同的元素
      // 如果推了後發現curr還在note內，就繼續重複相同動作，直到curr不再出現在note內(此時兩個指標會在同個位置)
      while (note.has(curr)) {
        // set內的元素沒有順序性，所以才用s取得實際上跟curr一樣的元素，並以此刪掉note內重複的元素
        note.delete(s[slowIndex]);
        slowIndex += 1;
      }

      // 如果note內找不到curr，那直接把curr新增到note
      note.add(s[i]);

      // 每一輪都要檢查「兩個指標當前的長度」有無比maxLength大，如果有的話更新上去
      maxLength = Math.max(maxLength, i - slowIndex + 1);
    }

    return maxLength;
  };
 ```

8/30
- 練習Leetcode 53. Maximum Subarray解法 [🖌️](https://www.typescriptlang.org/play/?#code/PTAEDMFcDsGMBcCWB7aoC2BDAHgZUgEYCCATiZgJ4AU0k6AzgFyi3oECmJA2gLoCUzVhxKgA3gCgQoadKmA8-UTQAJu2ygAjIGjUwNOagW-jAx3KAYf8ACRoFO5QEGagHPMANu2gBzeAAtA9GbrDgYoTAjDqBYOUCLsYAv8YAQ6oaAL26ApcaAz7GADEqAAOaAMfqAIW4k7PCQJNCSYDIQyCRUtvCgiKAAvBoA3MWgADwsdPQAdLYOzlWIANQdfBJSOTmwqPTIts3I9lQABoilACSiiAC+kwA0rPR8Wf05UlaAbq6A0HKA4MbRiYAepoDq2oAFSoBQcoBuioCySoAAcoDQCpeA5JqAPaaHJ5eGW9tZGBAPCGgGcVQDqIc83hcXIBjazOAMBiHANAaXEQPFAHXqDHRoAAtOpMQA+HH0dH8XrZQE5dYUspk+nYuklfEaHgVRHbRZc0A8voyQbQYajazjKgAcnx0plstlEpWZMVUrlqulEs2AukKTSGVAAFlMM5GlhsFRGhb1nxOVJFpzxOIoHAkKgMDh8MQyJRUQxBHRhLwBDjhGJxNJCqAUvQGXSAAwcsOgCPwdjoAAOMbR8ft0nAeQKqWq5XU7VqZOadkcTnaXR6iekQvoRVg6RE5RZCfroBT6YZhuNpqoLbIWO7qbTiuHJGtDpyyKoPYzxPKUbr2ykjZG7DGE0mKTT1kwsHYkfY0fgyFA80Xyxn2yjDMXnJyPOkPMTOvSaCjnLtDvEm6iuKpoeqQ5DUFw+IAEwrOoKz4gAzCsAAs8FwTBcH4gArCh-DWqAUgAGwAUMW47lQIGEGB3pcESfD4VI6gkcKZFihMlGeuBVBcDhqGEisADsKwABx4VUUhQQhzEitubEUe6VFehB0FoWJBFgIS0mscBCmcTRMH8QhalSMh4hAA)
 ```js
 function maxSubArray(nums: number[]): number {
    // 有紀錄的最大加總，作為最後返回的答案
    let res = nums[0];
    // 當前紀錄的加總
    let temp = nums[0];
 
    for(let i = 1; i < nums.length; i++){
      const curr = nums[i];

      // 從temp加上curr跟curr選一個較大值，更新到temp

      // 如果是curr比較大，意味著temp是負數
      // 題目是要比大，temp若是負數，留著temp沒有意義，所以用curr把它蓋過去
      // 如果是temp加上curr比較大，意味著temp是正數
      temp = Math.max(curr + temp, curr);

      // 每一輪都要檢查當前紀錄的加總有無比res大，如果有的話更新上去
      if(temp > res){
        res = temp;
      }
    }
 
   return res;
 };
 ```

8/29