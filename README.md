# Scrabble
**Description:**

This game is a revised version of the Scrabble word game, a description can be found here: https://en.wikipedia.org/wiki/Scrabble 


**Things to take note when placing tiles:** 

- Blank tiles are denoted by '#' in this version of the game. When playing a blank tile onto the board, player must designate its letter value by choosing an appropriate letter. 
- All tiles played must spell one main word of at least two letters, reading horizontally from left to right or vertically from top to bottom. 
- The word played must touch existing words either horizontally or vertically. 
- When the main word makes additional cross-words, they are each considered to be part of the play for the purposes of scoring the play and determining its validity. 


**Scoring system:** 

- At the end of a player's turn, the player's cumulative score will be calculated and enough tiles will be drawn to bring the player's total back to seven tiles (if possible).  
- The score of a word is the sum of the scores of its letters, each multiplied according to any letter bonus squares newly covered, then finally multiplied according to any word bonus squares newly covered. (The center square counts as a double word square.)  
- Each letter used will have a different value point. There are 100 tiles used in each game, with the tile value denoting as such:     

  - 0pts - Blank '#' (2 tiles) 
  - 1pt - A, E, I, L, N, O, R, S, T, U (9 A, 12 E, 9 I, 4 L, 6 N, 8 O, 6 R, 4 S, 6 T, 4 U) 
  - 2pts - D, G (4 D, 3 G) 
  - 3pts - B, C, M, P (2 tiles each) 
  - 4pts - F, H, V, W, Y (2 tiles each) 
  - 5pts - K (1 tile each) 
  - 8pts - J, X (1 tile each) 
  - 10pts - Q, Z (1 tile each) 
  - A 50-point _bingo_ bonus is awarded if all seven tiles are used 
 

**Documentation:**

It is required for this game to add to path the following files: Scrabble_board.png, Scrabble_rack.png, Scrabble_rules.text, and all 26 Lexicon text libraries (denoted by Lexicon_’X’.txt). 

The functions involved are documented below: 

**_init_game()._** This function generates the game board, shuffles the bag and determines the number of players. Possible expansions to the game (e.g. different board layout, tile number, etc.) can be implemented here.
 
**_whos_turn(game_turns, num_players)._** This function takes two parameters: the number of turns played so far, and the number of players. Populates the variable “player” with the object name of the player who's turn it is (player1 or player2). This allows a later function to automatically call the correct player’s attributes (e.g. the generic method player.hand will automatically give player1.hand if its Player 1’s turn). 

**_turn(player)._** This function takes the current player as an argument. It is the main loop that runs until the player chooses and commits to a move (play / skip / swap / end game). It first draws the players hand, then asks the player for their choice. 
 
**_swap()._** This function is run when the player chooses to swap their tiles. It will ask the player for tiles they intends to swap, validate their input, and then ask for a confirmation. 

**_play()._** This function is the control loop that is run when the player decides to play some tiles to the board.  

**_word_to_play()._** This function asks the user for tiles they intend to play and validates their input. It also allows them to skip their turn without playing any tiles. It returns the chosen word as a list of letters. 

**_choose_placement()._** This function asks the user for the intended placement of the chosen word to play, and validates their input according to physical rules. It returns two values: “valid” as a Boolean or placeholder string, and “played_letter_coordinates” as a list of coordinates corresponding to indexes of the played letters. The player is asked to choose a square on the board based off grid coordinates (e.g. B4, J10 etc.). The input is split after the first character, and both segments are checked separately against a dictionary of values. The dictionaries convert the played grid coordinates into indexes for processing (e.g. A1 -> [0][0], B4 -> [1][3] etc).

**_check_validity()._** This function takes in “played_letter_coordinates”, which are the coordinates of the recently played letters, and determines if the move was within the rules of the game and returns a Boolean value. 

**_scoring_words(played_letter_coordinates)._** This function takes in “played_letter_coordinates”, which are the coordinates of the recently played letters and returns “scored_word_coordinates”, which are the coordinates of all scored words (words that were modified and hence need their score calculated). 

**_count_score()._** This function takes in “scored_word_coordinates”, which is the list of coordinates of words that need to be scored, and outputs “wordlist”, which is the list of actual words from the board, as well as “score”, a list of scores for each of the words played.  

**_displayBoard(board), displayHand(hand)._** These functions take in the board values and the player’s hand at the start of every turn and uses matplotlib to display an image corresponding to the current board in play, and the player’s tiles in hand. 

**_check_words(wordlist)._** This function checks for the validity of the word(s) played against the Lexicon, the official dictionary used in Scrabble. To avoid any error encountered with blank letters denoted by '*', it first makes a copy of the word(s) played and checks for the first letter of the word(s), before opening the respective Lexicon and scanning through the entire list for the presence of the word(s) played. (This is due to the limitation of Jupyter Notebook that prevents saving all 270,000 words in a list/dictionary without modifying the jupyter_notebook_config.py file). Lastly, the function returns the validity status of the word(s). 

**_game_end()._** This function is run before the start of every turn and checks if the endgame conditions have been met. If so, the main loop is exited and the game ends. 

The conditions for the game to end are: The bag is empty, and the hand of the player who's turn just ended is empty.
 

**References:**

- NASPA (Ed.). (2017, January 20). NASPA Official Tournament Rules: Player Edition. Retrieved 2020, from http://www.scrabbleplayers.org/w/Official_Tournament_Rules 

- Collins Scrabble Tools. (2020, December 03). Retrieved December 08, 2020, from https://blog.collinsdictionary.com/scrabble/scrabble-tools/ 

- Make a Big Scrabble Board: Tutorial [Digital image]. (2016). Retrieved 2020, from https://www.creativeinchicago.com/2016/06/make-a-big-scrabble-board-tutorial.html 

- Gries, D., Lee, L., Marschner, S., &amp; White, W. (2014). CS 1110: Introduction to Computing Using Python Fall 2014 Assignment 4: Word Puzzles [Digital image]. Retrieved 2020, from https://www.cs.cornell.edu/courses/cs1110/2014fa/assignments/assignment4/ 
