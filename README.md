![project](pomodoro.gif)
![challenge-explaination](screen.png)

Having the word of ‘timer’ invite SETTIMEOUT to my mind and word of ‘count’ reminds me of a while loop which I am not sure about it. 

![brain-warming](brain-warming.jpg)

- What about  considering a function that every one second do reduction and replace the string?!!!
And we need to clear set timeout for pause or cancel. 
We might need things like<br>
`Let count=25;`
`Count--`
`document.querySelector().innerHTML`

- Actually if we are going to have settimeout so which function should put for callback.


- After I have writen basic html and css I have noticed that "oh" we have **minutes** and **seconds** means after 60 seconds should change minues ?!!!!!!!!

- Can I make a reaping function for seconds? like every 59 seconds comes back to start and for minutes every 60000 reduce 1 !!!!???????? :clock12:
- Do I need to use `setTimeut` or `seInterval` ?
![brain-warming2](brain-warming2.jpg)

- to choose between *innerHTML, innerText, and textContent* I have read 
[betterprogramming website](https://betterprogramming.pub/whats-best-innertext-vs-innerhtml-vs-textcontent-903ebc43a3fc)

-first lines of Js
```
    let workminutes = 25;
        let workseconds = 60;
        const secondsElement = document.querySelector('.seconds');
        function setSeconds() {
            workseconds--;
            secondsElement.innerText = workseconds;
            if (workseconds <= 0) {
                workseconds = 59
            }
            setTimeout(setSeconds, 1000)
        }
        document.querySelector('#start-button').addEventListener('click', setSeconds)
```

so exciting when i saw the seconds part is working,

![dance](dance.gif)

but somethings should get changed like : to add 0 before single numbers and it went to 58 after 0 not 59

I added the function for minutes 
```

        const minutesElement =  document.querySelector('.minutes');
        function setMinutes() {
            workminutes--;
            minutesElement.innerText = workminutes;
            if (workminutes <= 0) {
                workminutes = 0;
            }
            setTimeout(setMinutes, 60000)
        }
```

to call both function together when click event happens, I made a callback includes both
```
  function workTimer(){
            setSeconds();
            setMinutes();
        }
```
-let's see what will happen

Ok
- I need to concatenate **Colone:**
- but before seconds comes to zero , minutes get reduce :expressionless:
what about if I add a callback function in setSeconds function when the seconds comes to zero !!!! like :

```
 function setSeconds() {
            workseconds--;
            secondsElement.innerText = workseconds;
            if (workseconds <= 0) {
                workseconds = 60;
                 setMinutes()                         //this line has added and settimeout hase removed from setminutes function
            }
            setTimeout(setSeconds, 1000)
        }

           function setMinutes() {
            workminutes--;
            minutesElement.innerText = workminutes;
            if (workminutes <= 0) {
                workminutes = 0;
            }
        }
```

when I click start button the minut is 25 and it shows 25:59 but I want  24:59 so I will make a call back that first change inner html to 24
```
 function setTimer(){
            minutesElement.innerText = 24;
            setSeconds();
        }
        document.querySelector('#start-button').addEventListener('click', setTimer)
```
- when the seconds was equal **1** the minute gets changed but I dont want it so I separate the if statment in the setsecond function 

-so the if statement has changed to 
```
            if (workseconds == 1) {
                workseconds = 60
            }
            if(workseconds == 59){
                setMinutes();
            }
```
-ok , it looks better . so I dont need setTimer to change the htmlcontent to 24. strait away I call setSeconds then .