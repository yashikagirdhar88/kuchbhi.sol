pragma solidity ^0.8.0;

contract BadmintonTournament {
    address public director;
    uint public playerCount;
    uint public matchCount;

    struct Player {
        uint id;
        string name;
        uint age;
    }

    struct Match {
        uint id;
        uint player1;
        uint player2;
        uint player1Score;
        uint player2Score;
        bool isCompleted;
    }

    mapping(uint => Player) public players;
    mapping(uint => Match) public matches;

    event PlayerRegistered(uint id, string name, uint age);
    event MatchReported(uint id, uint player1Score, uint player2Score);

    modifier onlyDirector() {
        require(msg.sender == director, "Only the director of tournament can perform this action");
        _;
    }

    constructor() {
        director = msg.sender;
    }

    function registerPlayer(string memory _name, uint _age) public onlyDirector {
        require(bytes(_name).length > 0, "Name cannot be empty");
        require(_age >= 18, "Player must be at least 18 years old");

        playerCount++;
        players[playerCount] = Player(playerCount, _name, _age);

        emit PlayerRegistered(playerCount, _name, _age);
    }

    function reportMatch(uint _player1, uint _player2, uint _player1Score, uint _player2Score) public onlyDirector {
        require(players[_player1].id == _player1, "Player 1 is not registered");
        require(players[_player2].id == _player2, "Player 2 is not registered");
        require(_player1 != _player2, "Players must be different");

        matchCount++;
        matches[matchCount] = Match(matchCount, _player1, _player2, _player1Score, _player2Score, true);

        emit MatchReported(matchCount, _player1Score, _player2Score);

        assert(matches[matchCount].isCompleted == true);

        if (_player1Score == _player2Score) {
            revert("Match cannot end in a draw");
        }
    }

    function getWinner(uint _matchId) public view returns (string memory) {
        Match memory match_ = matches[_matchId];

        require(match_.isCompleted, "Match is not completed yet");

        if (match_.player1Score > match_.player2Score) {
            return players[match_.player1].name;
        } else if (match_.player2Score > match_.player1Score) {
            return players[match_.player2].name;
        } else {
            revert("Match cannot end in a draw");
        }
    }
}
