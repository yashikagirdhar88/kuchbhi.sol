# requireassertrevert (badmintonTournament)
below is the explaination of code which focus on functionality of require(), assert( ) and revert() statements.
The “BadmintonTournament” smart contract is a program written in Solidity that manages player registrations and match reports for a badminton tournament.
So, in contract structure we firstly have some variables as director- the address of the person who deploys the contract, playerCount and matchCount to keep track of players and matches.
Than we have two structures ‘Player’ having information about player id, name and age.
And Match having information about match id, player1 id , player2 id, and their respective scores and whether the match is completed .
Than we are mapping players and matches array to struct ‘Player’ and ‘Match’.
After this we have two events  PlayerRegistered and MatchReported which are emitted when a new player is registered and a match result is reported respectively.
We have modifier that restricts certain functionalities to be called by  director only with the help of require statement and we have a constructor for this modifier that sets contract deployer as the ‘director’.
Now first we have registerPlayer function that registers new player and this is can only be done by director only .
It uses require statement to ensure name is not empty and age of player is atleast 18, it increments the ‘playerCount’ and adds a new player to players array and emits the ‘PlayerRegistered’ event.
Next we have reportMatch function which reports a match result and it also uses require statement to check if both players are registered and they are not same player. After this matchCount gets incremented and new Match is added to matches array, it emits the ‘MatchReported’ event.
It uses assert statement to check (certain internal conditions are true) that is match is marked as completed , and it also uses a revert statement to revert the message and prevents the match from ending in draw.
Last we have a getWinner function to return the winner of a specific match , it uses require statement to check if match is completed and compare the scores of players to return the winner name and it also uses revert to handle any case where match ends in draw.

