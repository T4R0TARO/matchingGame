```js
/*
* addEventListener('DOMContentLoaded')
*/
    document.addEventListener('DOMContentLoaded', () => {
        //  All logic will go here
        //  create board
        //  check for match
        //  flip your card
    }
```


The *DOMContentLoaded* event fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. 
All of the logic of the game will be contained withing this event listener.

------------------------------------------------------------------------------------
```js
/*
* Array.sort()
* Math.random()
*/
/*Sorts the items withing the array
  Then randomize the numer order*/
     cardArray.sort(() => Math.random())
```

1. If we, to start the game the imgs will be set im the same spot ever time 
2. To randomize the arrays content we will use sort() and Math.random()
3. We take the cardsArray and randomize the order with  sort() and Math.random()
------------------------------------------------------------------------------------

```js
/*document.querySelector()*/
/*Contain elements in variables; select elements by using the DOM*/
      const grid = document.querySelector('.grid')
      const resultDisplay = document.querySelector( `#result` )
      let cardsChosen = [];
      let cardsChosenId = [];
      let cardsWon = [];
```


1. Select the needed elements and contain them in variable for later use. 
2. Select the varaibles with `document.querySelector`. 


------------------------------------------------------------------------------------

```js
/*
* for...loop
* document.createElement()
* setAttribute()
* data-id
* appendChild
*/
          //create your board
      function createBoard() {
          for(let i = 0; i < cardArray.length; i++){
              let card = document.createElement('img');
              card.setAttribute('src', 'images/blank.png')
              card.setAttribute('data-id', i)
              card.addEventListener('click', flipCard)
              grid.appendChild(card)
          }
      }  
```

1.  To create the board for the board game we need to DO something so, create a function to createBoard()
2.  Use a for...loop to loop through the cardArray.length
3.  For every loop, create a new element card with `createElement('img')`
4.  Set a src attribute with a path to the img with `setAttribute('src', 'images/blank.png)`
5.  Set another new attribute to the new card item with `setAttribute('data-id, i)`; Why? `data-id` is a custom attribute instead of using `class`; then set the value of `data-id` to the counter varibale `i` 
6.  Set for later use, flipCard() will be made later down the doc
7.  Make the new card items children of the variable *grid* with `appendChild()`

- When the page loads the function createboard() will fire
- The function will loop through each item of the array and create a new card element every loop
- Each loop will also set the attributes of the new card item 
- Each loop will make a card item a child of the variable *grid*
- Variable *grid* will display on the doc and all its new card children
- The loop will end when the array has counted all the cards in the array
 

------------------------------------------------------------------------------------


```js
/*
* document.querySelectorAll()
* else...if
* textConent
* if...
*/
          //checks your match
    function checkForMatch() {
        let cards = document.querySelectorAll('img')
        const optionOneId = cardsChosenId[0];
        const optionTwoId = cardsChosenId[1];
        if (cardsChosen[0] === cardsChosenId[1]){
            alert('You found a match')
            cards[optionOneId].setAttribute('src', 'images/white.png')
            cards[optionTwoId].setAttribute('src', 'images/white.png')
            cardsWon.push(cardsChosen)
        } else if (cardsChosen[0] === cardsChosen[1]) {
            alert('You found a match')
            cards[optionOneId].setAttribute('src', 'images/white.png')
            cards[optionTwoId].setAttribute('src', 'images/white.png')
            cards[optionOneId].removeEventListener('click', flipCard)
            cards[optionTwoId].removeEventListener('click', flipCard)
            cardsWon.push(cardsChosen)
        } else {
            cards[optionOneId].setAttribute('src', 'images/blank.png')
            cards[optionTwoId].setAttribute('src', 'images/blank.png')
            alert('Sorry, try  again')
        }
        cardsChosen = []
        cardsChosenId = []
        resultDisplay.textContent = cardsWon.length
        if (cardsWon.length === cardArray.length/2) {
            resultDisplay.textContent = 'Congratulations! You found them all!'
        }
    }   
```

1. We need to do something so create a function to checkForMatch()
2. Capture ALL the new card items with `document.querySelectorAll()
3. Create seperate variables for the card options from the cardsChosenID array
4. Next create a condition where the items inside the cardsChosen array must equal each other
5. If the cards are equal then assign the white image to the card
6. Also make another empty array named `cardsWon` and push() the matched cards to the array 
7. If the cards do NOT match, we want to have the cards flip back so they can be played again so we set the attribute to the blank img 
8. Next, regardless of what outcome occurs we want the arrays cleared afterward so set the *cardsChose* array and  *cardsChosenId* to and empty array
9. With *textConent* we can display the text of the player score. Capture the `<span>` in a variable 
10. If the cardsWon array's length is equal to cardArray length we know that we used all the cards in the array and we can alert the user with text on the page




------------------------------------------------------------------------------------

```js
/*
* .this
* getAttribute()
* .push()
* setTimeout()
*/
              //flip your card 
      function flipCard() {
          let cardId = this.getAttribute('data-id')
          cardsChosen.push(cardArray[cardId].name)
          cardsChosenId.push(cardId)
          this.setAttribute('src', cardArray[cardId].img)
          if (cardsChosen.length === 2) {
              setTimeout(checkForMatch, 500)
          }
      }
```

1. We need to DO something so, create a function to flipCard()
2. get the `data-id` attribute and contain it within a varible refering to `this` functions card chosen 
3. Make an empty array called ` let cardsChosen = []`; placed higher up on the doc 
4. With `push()`, push the *card* from the *cardArray* by using its *[cardId]* when the card is located *name* property obtained.
5. Do the same with the  push *cardId* to the *cardsChosenId*
6. Since this `flipCard()` is a function inside the eventListener function; the first card should already be selected
7. `this.setAttribute()` will allow us to set an img on the card, based on the cards id 
8. We only want to put 2 cards in the *cardsChosen* array. Why? Player flips two cards to check for match 
9.  if the *cardsChosen* is equal to 2 then the *checkForMatch* function will fire. `setTimeout`(checkForMatch, 500) will fire function after 500ms

- We need to do something so create a function to flipCard()
- get the card by its data-id and contain in a variable
- Create two empty arrays and store cardChosen and cardsChosenId
- this cards attribute will set the image to the card item chosen by its cardId
- cardChosen has a max of 2 and when that value is each the function checkForMatch() fires
------------------------------------------------------------------------------------
