// Function to initialize the Tic Tac Toe board
function initializeBoard() {
    return [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
    ];
}

// Function to print the Tic Tac Toe board
function printBoard(board) {
    for (let i = 0; i < board.length; i++) {
        console.log(board[i].join(' | '));
        if (i < board.length - 1) {
            console.log('---------');
        }
    }
}

// Function to check if the current player has won
function checkWinner(board, player) {
    // Check rows
    for (let i = 0; i < 3; i++) {
        if (board[i][0] === player && board[i][1] === player && board[i][2] === player) {
            return true;
        }
    }

    // Check columns
    for (let j = 0; j < 3; j++) {
        if (board[0][j] === player && board[1][j] === player && board[2][j] === player) {
            return true;
        }
    }

    // Check diagonals
    if ((board[0][0] === player && board[1][1] === player && board[2][2] === player) ||
        (board[0][2] === player && board[1][1] === player && board[2][0] === player)) {
        return true;
    }

    return false;
}

// Function to check if the board is full
function isBoardFull(board) {
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[i].length; j++) {
            if (board[i][j] === '') {
                return false;
            }
        }
    }
    return true;
}

// Function to make a random move by AI
function makeAIMove(board) {
    let row, col;
    do {
        row = Math.floor(Math.random() * 3);
        col = Math.floor(Math.random() * 3);
    } while (board[row][col] !== '');

    board[row][col] = 'O';
}

// Function to play the Tic Tac Toe game
function playGame() {
    let board = initializeBoard();
    let currentPlayer = 'X';

    while (true) {
        console.clear();
        printBoard(board);

        if (currentPlayer === 'X') {
            // Player's turn
            let row, col;
            do {
                row = parseInt(prompt('Enter row (0-2):'));
                col = parseInt(prompt('Enter column (0-2):'));
            } while (isNaN(row) || isNaN(col) || row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] !== '');

            board[row][col] = currentPlayer;
        } else {
            // AI's turn
            makeAIMove(board);
        }

        if (checkWinner(board, currentPlayer)) {
            console.clear();
            printBoard(board);
            console.log(currentPlayer + ' wins!');
            break;
        } else if (isBoardFull(board)) {
            console.clear();
            printBoard(board);
            console.log('It\'s a draw!');
            break;
        }

        currentPlayer = (currentPlayer === 'X') ? 'O' : 'X';
    }
}

// Start the game
playGame();

