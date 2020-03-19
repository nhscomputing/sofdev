Hi Team, I guess you probably feel like this now when you find out Ms Sun won't be at school today. I will be back on Monday.

![happy](https://media2.giphy.com/media/TXJiSN8vCERuE/giphy.gif)

However it's not party time. Please make full use of the class time to study the search algorithm.

I put the agenda for you to better organise your time:
1. (5min) play the number guessing game with a partner or in a small group. Discuss your strategies with your partners. 
2. (15min) study binary search: read the definition below. If it doesn't make sense to you. Find yourself a youtube video.
3. (20min) Implement it in JS. Once you understand how the algorithm works, follow my tutorial below to code binary search. Make sure you test your code before moving on. **Check my code in the bisearch.html should you get stuck**.
4. (15min)Tweak binary search to sort an array with duplicated elements. This is a very important task! You will need it in your module 3.
Best luck with learning search.
5. By the end of the period, email me what you have done and any road blocks please.


## Number guessing game
1. Find yourself a partner
2. Pick a whole number from 1 to 1000.
3. Let's your partner make a guess.
4. For each guess, you tell your partner if the guess is correct, or is higher or lower than the secret number.
5. Each guess will cost your partner $1.
6. Switch the role once the guess is made correctly.
7. Count the cost and whoever has the less cost wins.
### Questions to think about:
* How should I choose my guess number, sequentially, randomly or strategically?
* What strategies can I use to minimise the cost?
* If you choose the guess number sequentially, how much will cost you?

## Linear Search
Maybe you guessed 1, then 2, then 3, then 4, and so on, until you guessed the right number. We call this approach **linear search**, because you guess all the numbers as if they were lined up in a row. It would work. But what is the highest number of guesses you could need? If your partner selects 999, you would need 999 guesses. 
## Binary Search
* Watch this video from Harvard Uni on binary search. [Click here to watch](https://youtu.be/T98PIp4omUA)
* Binary Search (Half-Interval Search) is a Search Algorithm to find a specific element located in an Array (**ONLY works with Sorted Arrays**). 
* Faster and more efficiently than linear search due to less number of comparisons made.
* Instead of searching an array at index 0, 1, 2, 3, 4, and so on like we do in a *while* Loop, Binary Search allows us to divide our search in half each time we look for a target value.
* We define a middleIndex or midpoint from the element in the middle of the array (Divide) to see if our target value is greater than or less than the middleIndex or midpoint. Depending on if the target value is greater than or less than the middleIndex, we can remove the left or right of our array from our search (Conquer).

![linear search](https://miro.medium.com/max/600/1*EYkSkQaoduFBhpCVx7nyEA.gif)
## Binary Search implementation
You can either use recursive or iterative method to code binary search. In this tut, we will use iterative method with a while loop.


1. Create a function that takes two parameters, which is the array and the target value.
```javascript
function binarySearch(arr,target){

}
```
2. The core of the process is to keep halving the array until the target value is found. Therefore you need to keep track of 3 things of the sub arrays:
    1. *startIndex*. The initial value is 0. It points to the first element of the original array. Each halving process, the startIndex will change depending on if the target is greater or less than the Middle Value.
    2. *endIndex*. The initial value is arr.length. It points to the last element of the original array. endIndex varies each halving process too.
    3. *MidIndex*. To calculate the index for the midpoint element, you can use (startIndex + endIndex)/2. To get a whole number result, you need to use either Math.ceil() to round up or Math.floor() to round down. We will use Math.floor() in our case. It will change as per each halving process.
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
}
```
3. While the startIndex is less than or equal to the endIndex, you repeat the halving process. This can be translate into code as below:
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
    while(startIndex <= endIndex>){

    }
}

```
4. Inside the loop, use the startIndex and endIndex to calculate the midppoint Index.
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
    while(startIndex <= endIndex){
        let midIndex = Math.floor((startIndex + endIndex) / 2);
    }
}

```
5. Compare the middle value with the target. There are 3 possiblities. If the midIndex value matches with the target, then problem solved. You simply return the midIndex value
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
    while(startIndex <= endIndex>){
        let midIndex = Math.floor((startIndex + endIndex) / 2);
        if(target == arr[midIndex]){
            return arr[midIndex];
        }
    }
}

```
6. If your target is greater than the midIndex value, you know your target will be somewhere to the right of the midIndex value. You chop off the left half of the array and you can narrow the search to the right half of the array. In saying this, you need to update the startIndex to the midIndex + 1
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
    while(startIndex < = endIndex){
        let midIndex = Math.floor((startIndex + endIndex) / 2);
        if(target == arr[midIndex]){
            return arr[midIndex];
        }
        else if(target > arr[midIndex]){
            startIndex = midIndex + 1;
        }
    }
}
```
7. If your target is less than the midIndex, you know your target will be somewhere to the left of the midIndex value. I leave it to you to complet the code.
```javascript
function binarySearch(arr,target){
    let startIndex = 0;
    let endIndex = arr.length;
    while(startIndex <= endIndex){
        let midIndex = Math.floor((startIndex + endIndex) / 2);
        if(target == arr[midIndex]){
            return true;
        }
        else if(target > arr[midIndex]){
            startIndex = midIndex + 1;
        }
        else {
            ___________________________ 
        }
    }
    return false;
}
```
8. Test your code with the following array and compare the results. Try searching 17!
```javascript
let tstarr = [1, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59];
let tstarr1 = [7, 3,60, 1, 11, 13, 59, 19, 41, 29, 31, 21, 23, 43, 37, 53, 17];

```
## From theory to reality
In real life, you tend to receive multiple entries that match with your key word(s). You may say that's easy, just iterate each entry and push the index of the matching elements. It will work but how can you make it more efficient. Can you adapt the binary search algorithms to make it work?
Suppose you have an array with duplicated elements like this
```javascript
let arr = [1,1,1,3,3,3,3,5,5,8,9,9,9,9,9,14,15,16,16,16]
```
Your challenge is to search for the target and return the index of the first matching element and last matchin element.
Hint: use binary search to land at your first target. Then move backward to the left and forward to the right to locate the index of the first element that doesnt match with the target. This is how you find the bounds of the duplicated portion. Hope it makes sense to you. Don't forget you can google it!

## What's next?
We will be searching records with matching strings from a csv file next week. Therefore, you need to be proficient in the following tasks:
* load/read CSV files into an array of objects
* extract the year,month and date from a date string



