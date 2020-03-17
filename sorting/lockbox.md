# Lock box Challenge
![lockbox](https://i.ytimg.com/vi/aT3RcCmwLqs/maxresdefault.jpg)

You may have already seen a green suit case in your classroom. There are some mystery prize inside it. However, it is locked. Your challenge is find the passcode to unlock the case!
The passcode consists of three digits. You have 3 clues to uncover the passcode.

## Clue for digit 1:
Choose the correct answers for the following questions and add up your choices.
Q1. In the process of sorting an array of eight integers using the quick sort algorithm, the first partitioning with the array appears as follows.

![q1.img](https://content.screencast.com/users/Sensei2020/folders/Jing/media/8731ea91-d4fa-4ea9-8996-c59980594e6e/2020-03-17_1505.png)

Which one of the following statements is correct?
1. Neither 17 nor 19 was the pivot.
2. The pivot was either 17 or 19.
3. The pivot was 17, but was not 19.
4. The pivot was not 17, but it could have been 19.

Q2. Which one of the following is a correct statement about selection sort and quick sort for large files?
1. A selection sort is normally faster than a quick sort, which uses a pivot.
2. A quick sort is normally faster than a seletion sort, which uses a pivot.
3. The algorithm for a quick sort produces fewer comparisions than the algorithm for a selection sort.
4. The algorithm for a selection sort produces fewer comparisons than the algorithm for a quick sort.

Q3. 
![q3img](https://content.screencast.com/users/Sensei2020/folders/Jing/media/c0ac621e-3971-4219-a400-bcee1335cc22/2020-03-17_1518.png)
1. quick sort
2. bubble sort
3. linear search
4. selection sort

By now you should have added up all the numbers of your choices. Hope it is a single digit!
How do you feel? This or that?
![tooeasy](https://thumbs.gfycat.com/FaroffThoroughAmericanquarterhorse-size_restricted.gif)
![noidea](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTh7RQ8CEiG-vR3D5BTL7bIYQT9dmk7hp7K2YsKxQ4A5yECs-e2&s)

## Clue for 2nd digit
Measure the performance of the two sorting algorithms we have learned. Once you have completed all the following steps, you will be given the 2nd digit!!!
How???
1. Create a function to generate an array with a given number of random integers. e.g. randArr(50) will return an array with 50 integers ranging from 0 to 50. You may need to use Math.random and Math.floor functions.
```javascript
    function randArr(num){
        let arr = [];
        for(let i = 0; i < num; i++>){
            arr.push(_______________); // fill in the blank pls
        }
        return ____________ 
    }
```
2. Use selection sort and quick sort to sort the same randomly generated array. You need to run the two sorting algorithms on the same array. Place all the functions in the same file. It should look like this
```javascript
    let tstArray = randArr(50);
    selectionSort(tstArray);
    quickSort(____,_______,____________)// fill in the blank
    // make sure you put the actual functions below

    function selectionSort(){
        .
        .
        .
    }

    function quickSort(){
        .
        .
        .
    }
    function partition(){
        .
        .
        .
    }
    function swap(){
        
    }
```
3. Compare which algorithm is more efficient timewise.You need to figure out how to measure the time taken by a function to execute. You can try with this code.
```javascript
// start a timer
    console.time('time for running selection sort')
    selectionSort()
    console.timeEnd('time for running selection sort')
    
```
Alternatively you can experiement with **performance.now()**. [See more detail here](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)

## Clue for 3rd digit
Use quick sort to sort the list of your names in **descending order**. Hint: you can compare two strings. e.g. the expression 'Hello' < 'hello' is True as the ASCII code for the Letter H is less than h. You need only make one change in your current quick sort algorithm.
You can grab the array as below for your code. 
```javascript
    const heros = [
                'Rick Anastasiadis',
               'Vincent Crowe',
                'Andre Feliciani',
                'Oliver Guzowski',
                'Joseph Happ',
                'Sam Louise-Brown',
                'Zachary Meaney',
                'Matthew Papoulias',
                'Nicolas Rodda',
               'Michael Tang',
               'Michael Tsetsos',
                'Max Verhoef'
            ];
```
The 3rd digit is the number of letters in the first name of the second name element in your result. Have fun team!