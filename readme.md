# Tee’s Game

_(q: question, p: player)_

## Home Screen
- [create game → creates new room with name made of rnd adj & rnd noun or rnd adv & rnd verb]
- [list of buttons for created games]

## Join Game
- ⮑ playerId is exact time joined (UST)… (🔧concurrent join issue fix)
  - ⮑ save in local storage
  - ⮑ save on firebase playersDb
- First to join is mod, successive are auto-assigned player numbers

## Question Visual
- “Please enter a question”
- [text input]
- [submit button (visible when text input > 5 chars)] (🔧low quality q mitigator)
- ⮑ record q w/ corresponding playerId on firebase playersDb
- ⮑ remove input, show “q submitted. please wait for the game to start.”

## Mod Component
- display table of p’s
- beside p number is ✅ if they’ve submitted a question
- below… [“assign q’s at random and start” button]
  - ⮑remove p’s w/out submitted q’s (🔧player reconnection issue mitigator)
  - ⮑assign q’s at rnd to all p’s (no self-assignment)
  - ⮑on question visual for each player, show the q that the p was assigned
  - ⮑[“reassign random q” button] appears on p table for mod  
    (🔧p reconnection issue mitigator, 🔧 low quality q issue mitigator)
- [“reset game to enter questions phase” button]

## Database
- I suppose there needs to be a
  - table of players (w playerId, submittedQ, receivedQ)
  - table for game sessions? (enableSubmissions bool, display q’s, time created, gameId)

## Issues
- ⁉️ what if player enters crap question or “asdf”?  
  (low quality question)
  - 🔧 ameliorate w min char q’s
  - 🔧 ameliorate w reassigning p’s q (if their q sucks)
- ⁉️ players may leave by accident, join with a different browser  
  (player reconnection)  
  - solution - if any p gets a bad q, mod can reassign random q
  - what should be done in this case? is this only a problem if they submitted a question?
  - 🔧 ameliorate w mod features (kick)
- ⁉️💯🤷‍♂️ what if two players join at the same time  
  (concurrent join)  
  - solution - just save exact time joined, and it’ll be saved as their player ID in local storage
  - 🔧 fix by having playerId be a time stamp (in standardized time)

## Bonus (optional) features
- show when user is “online” (on the current screen)  
  w .onDisconnect or .info/connected