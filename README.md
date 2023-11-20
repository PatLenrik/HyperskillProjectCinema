# HyperskillProjectCinema
Cinema purchase program - show the available places, book the tickets, show the statistics and exit.


package cinema;
import java.util.Scanner;

public class Cinema {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
// rows and seats 
        System.out.println("Enter the number of rows:");
        int rows = scanner.nextInt();
        System.out.println("Enter the number of seats in each row:");
        int seatsInRows = scanner.nextInt();
//original hashtag
        String[][] hashtag = new String [rows + 1][seatsInRows + 1];
        hashtag[0][0]= " ";
        for (int j = 1; j <= seatsInRows; j++) {
            hashtag[0][j] = " " + j;
            for (int i = 1; i <= rows; i++) {
                hashtag[i][0] = Integer.toString(i);
                hashtag[i][j] = " S";
            }
        }

//options 
        int purchaseTickets = 0;
        int currentIncome = 0;
        boolean exit = false;
        while (exit == false ) {
            System.out.println("""

                1. Show the seats
                2. Buy a ticket
                3. Statistics
                0. Exit""");
            
            int input = scanner.nextInt();
            switch (input) {
                case 1:
                    System.out.println("");
                    System.out.println("Cinema:");
                    for (int S1 = 0; S1 <= rows; S1++ ) {
                        for (int S2 = 0; S2 <= seatsInRows; S2++) {
                            System.out.print(hashtag[S1][S2]);
                        }
                        System.out.println("");
                    }
                    break;
                case 2:
                    boolean purchase = false;
                    while (purchase == false) {
                        System.out.println("""
                                           
                            Enter a row number:""");
                        int row1 = scanner.nextInt();
                        System.out.println("Enter a seat number in that row:");
                        int column1 = scanner.nextInt();
                        if (row1 > rows || column1 > seatsInRows) {
                            System.out.println("");
                            System.out.println("Wrong input!");
                        }else if (hashtag[row1][column1].equals(" B")) {
                            System.out.println("");
                            System.out.println("That ticket has already been purchased!");
                        }else {
                            int price = 0;
                            if (rows * seatsInRows <= 60) {
                                price = 10;
                            } else {
                                if (row1 <= rows / 2) {
                                    price = 10;
                                }else {
                                    price = 8;
                                }
                            }
                            System.out.println("Ticket price: $" + price);
                            hashtag[row1][column1]= " B";
                            currentIncome += price;
                            purchaseTickets++;
                            purchase = true;
                        }
                    }
                    break;
                case 3:
                    System.out.println("");
                    System.out.println("Number of purchased tickets: " + purchaseTickets);
                    int allSeats = rows * seatsInRows;
                    double percentage = 0.00;
                    if (purchaseTickets == 0) {
                        percentage = 0.00;
                        
                    }else {
                        double purchaseTicketsD = purchaseTickets;
                        percentage = (double)((purchaseTicketsD * 100)/ allSeats);
                        System.out.println(percentage);
                    }
                    System.out.printf("Percentage: %,.2f", percentage);
                    System.out.println("%");
                    System.out.println("Current income: $" + currentIncome);
                    int totalIncome = 0;
                    int priceT = 0;
                    if (rows * seatsInRows <= 60) {
                        priceT = 10;
                        totalIncome = rows * seatsInRows * 10;
                    } else {
                        totalIncome = (rows / 2 * seatsInRows * 10) + ((rows - rows / 2) * seatsInRows * 8);
                    }
                    System.out.println("Total income: $" + totalIncome);
                    break;
                case 0:
                    exit = true;
                    break;
            }
            
        }
    }
}
