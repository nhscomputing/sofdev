## Let's conquer the Quick Sort!
![yeswecan](https://memecrunch.com/meme/I5I4/doggie-says-you-can-do-it/image.jpg)


This tutorial is inspired by this legendary tech youtuber. You may need to refer to his video to get a better sense of the logics.
<a href="http://www.youtube.com/watch?feature=player_embedded&v=eqo2LxRADhU" target="_blank">
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQ23rPBj94MRA58kAe1FeNMZBKFcSpVOZl6O7_PZu3ZsvHliLNC" 
alt="Quicksort visualisation" width="240" height="180" border="3" /></a>

Imagine you have an unsorted array [7,2,6,5,4].
1. You are going to write a function to sort your array in ascending order. You name the function as quickSort. In your code editor you'll have something like this
```javascript
function quickSort(){

}
```
2. This function expects you to pass into it three parameters: 1. the original array you want to sort; 2. the index of the start/left element of the sub array; 3. the index of the end/right element of the sub array. The idea is you are going to recursively subdivide and subdivide and subdivide the array and keep sorting different parts of it until the whole array is sorted.By now your code should look like this
```javascript
function quickSort(arr, start, end){

}
```
3. You need to tell your algorithm when to stop subdividing and return. You probably don't want to exhaust your CPU resource by performing infinite recursion. It's like a dog chasing its own tail. The condition is when your start index is greater or equal to the end index. This means you ended up having only one element in the sub array and no doubt it is sorted so there's nothing more you can divide.
```javascript
function quickSort(arr, start, end){
    if(start >= end){
        return;
    }
}
```
4. While your end index is greater than your start index (meaning you have more than one element in the subarray), you call the function to subdivide the array using a pivot. You name the function as partition. This function returns the index value of where the pivot ends up. You will use it later to reresent the start and end index of subarrays.
```javascript
function quickSort(arr, start, end){
    if(start >= end){
        return;
    }
    let index = partition();
}   
```
5. Inside the partition function, you need to pass three parameters: 1. the original array to be sorted; 2. the index of the start element of the sub array; 3. the index of the end element of the sub array.
```javascript
function quickSort(arr, start, end){
    if(start >= end){
        return;
    }
    let index = partition(arr, start, end);
}  
```
6. Now that you've got that index of where that pivot is, you are going to recursively call on that array from start to that index minus one, also quickSort that array from index plus one to end. This is dividing and conquering. Your code should look like this:
```javascript
function quickSort(arr, start, end){
    if(start >= end){
        return;
    }
    let index = partition(arr, start, end);
    quickSort(arr,start,index - 1); 
    quickSort(arr, index + 1, end);
}
```
7. Make sure your return the sort array in the end
```javascript
function quickSort(arr, start, end){
    if(start >= end){
        return;
    }
    let index = partition(arr, start, end);
    quickSort(arr,start,index - 1);
    quickSort(arr, index + 1, end);
    return arr;
}
```
8. You are almost there!. Now that you've done the quickSort function. You are going to write the partition function, which is the core of the algorithm! The goal of your function is find and return the index value of where the pivot is supposed to at. Let's define the function first:
```javascript
function partition(arr, start, end){

}
```
9. Choose a pivot value. As mentioned previously, there are many ways to do so. In this tutorial, let's just pick the last one as it's easy. You can express the value as arr[end]
```javascript
function partition(arr, start, end){
    let pivotValue = arr[end];

}
```
10. Since you've got the pivot value, you can rearrange the array so that everything that's less than the pivot are on the left side, likewise, everything that's greater than the pivot are on the right side. The orders in each sub array doesn't matter. At this stage, you need a pointer to keep track of the pivot index. We aren't talking about the index of the pivot value you have picked in step 7. This pivot index refers to the actual position where the pivot will end up being at. You only need to create a variable to store the pivot index and you assume it point to the start index.
```javascript
function partition(arr, start, end){
    let pivotValue = arr[end];
    let pivotIndex = start;

}
```
### **Spoiler alert**:You are about to embark on a journey which requires lots of brain power. Just trust you can do it and you da the best! You may need to watch the video mentioned above.
![youdabest](https://i.pinimg.com/originals/9a/0d/84/9a0d8453a4628f5258ff5566a7c40358.jpg)

11. Now here's the real deal:
    1. You need to iterate through every element from the **start** and the **end - 1**. why excluding the end element?
    ```javascript
    for (let i = start; i < end; i++ ){

    }
    ```
    2. Compare every single element against the pivot value. If the current element is not less than the pivot value, do nothing; if the current element is less than the pivot value,you swap the current element with the element that the pivotIndex is pointing to. 
    ```javascript
    for (let i = start; i < end; i++ ){
        if(arr[i] < pivotValue){
            swap(arr, i, pivotIndex);
        }

    }
    ```
    3. Increment the pivotIndex by 1. 
     ```javascript
    for (let i = start; i < end; i++ ){
        if(arr[i] < pivotValue){
            swap(arr, i, pivotIndex);
            pivotIndex++;
        }
    }
    ```
    4. Swap the pivot index element with the end element. Why? You want to place the pivot in the position where it's meant to be.
     ```javascript
    for (let i = start; i < end; i++ ){
        if(arr[i] < pivotValue){
            swap(arr, i, pivotIndex);
            pivotIndex++;
        }
    }
    swap(arr, pivotIndex, end);
    ```
    5. You need to figure out the last step in this partition function. Remember what was your goal?

12. As the last step, you need to write the simple swap function
```javascript
    function swap(arr, a, b){
        let temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
```
Test your code with a random array. Best luck!
![Which are you at](https://i.pinimg.com/originals/d0/1d/7a/d01d7ab9cb331e370f83d1883f2dabf5.jpg)
## What's next? 
### Visualisation
You can challenge yourself to visualisa the quicksort by finishing watching the video tutorial.
### Quicksort dance
Please watch this funny quicksort dance. It is the most nerdiest thing I've ever seen.
[Click here](https://youtu.be/ywWBy6J5gz8)
### Another algorithm
[check out this video](https://youtu.be/Fiot5yuwPAg)
### Explain recursion to a 6yo kid
A saying goes you never fully understand something if you can't explain it to a six year old.
Think about how you will explain recursion to your younger siblings or cousins.
Feel free to watch this [video](https://youtu.be/bvbZxwUamTs) for some ideas
### Why quick sort is more efficent that selection sort?
Thanks Vincent for mentioning this awesome [Ted-Ed video about sorting](https://youtu.be/WaNLJf8xzC4). Hope you all find it helpful.
