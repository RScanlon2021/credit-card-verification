# credit-card-verification
#### A simple credit card verification program written in vanilla JavaScript, using the Luhn Algorithm as the verification method.

This program was written as a challenge project for Codecademy. Below I will list the step-by-step requrements for completing the project, along with code fences for the related functions. 

There are 15 arrays that each contain the digits of separate credit card numbers. They all have prefixes to reflect their status. There is also a `batch` array that stores all of the provided credit cards in a single array.

1. Create a function, `validateCred()` that takes a single parameter for an array that returns `true` if valid or `false` if invalid .

   - Use the [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm#Description) to find out if a card number is valid or not.

   - ```javascript
     function validateCred(arr) {
       let testArr = [];
       let item = 0;
       arr.forEach((item) => testArr.push(item));
       for (let i = arr.length - 2; i >= 0; i -= 2) {
         item = testArr[i] * 2;
         if (item > 9) {
           item -= 9;
           testArr[i] = item;
         }
         testArr[i] = item;
       }
       let sum = testArr.reduce((acc, cur) => acc + cur);
     
       return sum % 10 === 0;
     }
     
     ```

     

2. Create another function, `findInvalidCards()` that takes one parameter for a *nested array* of credit card numbers. The role of `findInvalidCards()` is to check through the nested array for which numbers are invalid, and return another nested array of invalid cards.

   - ```javascript
     function findInvalidCards(arr) {
       let invalidArr = [];
       let validity = "";
       for (let i = 0; i < arr.length; i++) {
         validity = validateCred(arr[i]);
         if (!validity) {
           invalidArr.push(arr[i]);
         }
       }
       return invalidArr;
     }
     ```

     

3. 
   Create a function, `idInvalidCardCompanies()` that has one parameter for a nested array of invalid numbers and returns an array of companies.

   Currently, there 4 accepted companies which each have unique first digits. The following table shows which digit is unique to which company:

   | First Digit | Company                 |
   | ----------- | ----------------------- |
   | 3           | Amex (American Express) |
   | 4           | Visa                    |
   | 5           | Mastercard              |
   | 6           | Discover                |

   If the number doesn’t start with any of the numbers listed, print out a message like: “Company not found”.

   `idInvalidCardCompanies()` should return an *array* of companies that have mailed out cards with invalid numbers. This array should NOT contain duplicates, i.e. even if there are two invalid Visa cards, `"Visa"` should only appear once in the array.

   - ​	

     ```javascript
     function idInvalidCardCompanies(arr) {
       let companies = new Set();
       for (let i = 0; i < arr.length; i++) {
         if (arr[i][0] === 3) {
           companies.add("Amex (American Express)");
         } else if (arr[i][0] === 4) {
           companies.add("Visa");
         } else if (arr[i][0] === 5) {
           companies.add("Mastercard");
         } else if (arr[i][0] === 6) {
           companies.add("Discover");
         } else {
           return "Company not found";
         }
       }
       let companiesArr = Array.from(companies);
       return companiesArr;
     }
     ```

     

   ​	

