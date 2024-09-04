# Atividade-40

#include <stdio.h>

#define SIZE 3

void printBoard(char board[SIZE][SIZE]) {
    printf("\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            if (j < SIZE - 1) printf("|");
        }
        printf("\n");
        if (i < SIZE - 1) {
            for (int j = 0; j < SIZE; j++) {
                printf("---");
                if (j < SIZE - 1) printf("+");
            }
            printf("\n");
        }
    }
    printf("\n");
}

int checkWin(char board[SIZE][SIZE], char player) {
    // Check rows and columns
    for (int i = 0; i < SIZE; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return 1;
        }
    }
    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1;
    }
    return 0;
}

int checkDraw(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (board[i][j] == ' ') {
                return 0; // Found an empty spot, not a draw yet
            }
        }
    }
    return 1; // Board is full, it's a draw
}

void playerMove(char board[SIZE][SIZE], char player) {
    int row, col;
    while (1) {
        printf("Player %c, enter row and column (0-2): ", player);
        scanf("%d %d", &row, &col);
        if (row >= 0 && row < SIZE && col >= 0 && col < SIZE && board[row][col] == ' ') {
            board[row][col] = player;
            break;
        } else {
            printf("Invalid move. Try again.\n");
        }
    }
}

int main() {
    char board[SIZE][SIZE] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };
    char currentPlayer = 'X';
    int gameStatus = 0; // 0: running, 1: X wins, 2: O wins, 3: draw

    while (1) {
        printBoard(board);
        playerMove(board, currentPlayer);
        if (checkWin(board, currentPlayer)) {
            gameStatus = (currentPlayer == 'X') ? 1 : 2;
            break;
        }
        if (checkDraw(board)) {
            gameStatus = 3;
            break;
        }
        // Switch player
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    printBoard(board);
    if (gameStatus == 1) {
        printf("Player X wins!\n");
    } else if (gameStatus == 2) {
        printf("Player O wins!\n");
    } else {
        printf("It's a draw!\n");
    }

    return 0;
}
