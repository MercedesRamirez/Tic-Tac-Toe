# Tic-Tac-Toe
import java.util.Scanner;
import java.util.logging.Level;
import java.util.logging.Logger;

public class TicTacToe {
    
    public static final String RESET = "\u001B[0m";
    public static final String BLACK = "\u001B[30m";
    public static final String RED = "\u001B[31m";
    public static final String GREEN = "\u001B[32m";
    public static final String YELLOW = "\u001B[33m";
    public static final String BLUE = "\u001B[34m";
    public static final String PURPLE = "\u001B[35m";
    public static final String CYAN = "\u001B[36m";
    public static final String WHITE = "\u001B[37m";

    public static void main(String[] args) {
        String[][] board = {
            {"", "", ""},
            {"", "", ""},
            {"", "", ""}
        };
        printBoard(board);
        
        // Add user input
        Scanner scan = new Scanner(System.in);
        char[] players = {'X', 'O'};
        char player;
        int row = -1, col = -1;
        int count = 0;
        char choice;
        
       do {
        
        // Determine whose turn it is
        if (count % 2 == 0) {
            player = players[0];
            // Prompt user for row/col
            System.out.print("Enter your choice (A - I): ");
            choice = scan.next().charAt(0);
            
             if(choice == 'A') { row = 0; col = 0;  }
             else if(choice == 'B') { row = 0; col = 1; }
             else if(choice == 'C') { row = 0; col = 2; }
             else if(choice == 'D') { row = 1; col = 0; }
             else if(choice == 'E') { row = 1; col = 1; }
             else if(choice == 'F') { row = 1; col = 2; }
             else if(choice == 'G') { row = 2; col = 0; }
             else if(choice == 'H') { row = 2; col = 1; }
             else if(choice == 'I') { row = 2; col = 2; }
            
            board = updateBoard(board, 'X', row, col);
        } else {
            player = players[1];
            board = AIMove(board);
        }
         
        
        printBoard(board);
        
        // Check if somebody won
        if(victoryCheck(board, player)) {
            System.out.println("Player " + player + " WINS!!!");
            System.exit(0);
        }
        
        count++; // Move to next player
       }while(count < 9);
       // Game ends in tie
       System.out.println("The game ended in a tie.");
        
    }
    
    public static void printBoard(String[][] board) {
        char[][] letterGrid = {
            {'A', 'B', 'C'},
            {'D', 'E', 'F'},
            {'G', 'H', 'I'}
        };
        
        // Rows
        for (int r = 0; r < board.length; r++) {
            // Cols
            for (int c = 0; c < board[r].length; c++) {
               if(board[r][c].equals("")) {
                System.out.print("[" + letterGrid[r][c] + "]");
               }
               else {
                   System.out.print(board[r][c]);
               }
            }
            System.out.println("");
        }
        System.out.println("---------");
    }
    
    public static String[][] updateBoard(String[][] board, char player, int row, int col) {
        Scanner scan = new Scanner(System.in);
        if (board[row][col].equals("")) {
            board[row][col] = "[" + GREEN + player + "]" + RESET;
        } else {
            System.out.println("Someone was already placed there. Please try again.");
            System.out.print("Enter your desired ROW (0 - 2): ");
            row = scan.nextInt();
            System.out.print("Enter your desired COL (0 - 2): ");
            col = scan.nextInt();
            updateBoard(board, player, row, col);
        }
        
        return board;
    }
    
    public static String[][] AIMove(String[][] board) {
        System.out.println("AI Time!");
        try {
            Thread.sleep(1000);
        } catch (InterruptedException ex) {
            Logger.getLogger(TicTacToe8.class.getName()).log(Level.SEVERE, null, ex);
        }
        int row = (int)(Math.random() * 3);
        int col = (int)(Math.random() * 3);
        
        System.out.println("Attempting to place at row " + row + " col " + col);
        if (board[row][col].equals("")) {
            // Instructor Change (C): Change user player to print BLUE (Also updated in VC)
            board[row][col] = BLUE + "[O]" + RESET;
        } else {
            System.out.println("Recursion!");
            AIMove(board);
        }
        return board;
    }
    
    public static boolean victoryCheck(String[][] board, char player) {
        String p;
        if(player == 'X') p = "[" + GREEN + player + "]" + RESET;
        else p = BLUE + "[O]" + RESET;
       
        if( (board[0][0].equals(p) && board[0][1].equals(p) && board[0][2].equals(p))) {
            return true;
        } 
        // Second Row
        else if( (board[1][0].equals(p) && board[1][1].equals(p) && board[1][2].equals(p))) {
           return true;
        }
        // Third Row
        else if( (board[2][0].equals(p) && board[2][1].equals(p) && board[2][2].equals(p))) {
            return true;
        }
        // Diag top left down
        else if( (board[0][0].equals(p) && board[1][1].equals(p) && board[2][2].equals(p))) {
            return true;
        }
        // Diag Right
        else if( (board[0][2].equals(p) && board[1][1].equals(p) && board[2][0].equals(p))) {
           return true;
        }
         // First col down
        else if( (board[0][0].equals(p) && board[1][0].equals(p) && board[2][0].equals(p))) {
           return true;
        }
        // Second col down
        else if( (board[0][1].equals(p) && board[1][1].equals(p) && board[2][1].equals(p))) {
            return true;
        }
        // Third col down
        else if( (board[0][2].equals(p) && board[1][2].equals(p) && board[2][2].equals(p))) {
           return true;
        }
        return false;
        
    }
    
}
