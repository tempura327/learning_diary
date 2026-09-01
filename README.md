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