# Cash-register
 java project cash register 
/**
* Creating a program that functions as a simple cash register system.
*  Must be able to insert/remove articles, sell articles, and present sales history.
1. Getting input from the user: what he/she wants to perform.
2. Define the variables
3. Creating methods for printing menu, getting input, adding and removing articles, printing and sorting
4. Call the menu and check the user choice
5. Call method and print results 
*/

import java.util.Date;
import java.util.Scanner;
import java.util.Random;
class Main
  {
     //Get the input from the user
     private static Scanner userInput = new Scanner(System.in);
    
   public static void main(String[] args) {
      // Variables declaration
      int articleNumber = 1000;
      int[][]articles = new int[10][3];
      int[]noOfArticles = new int[10];
      int[][] sales = new int[1000][3];
      int[]price = new int[10];
      Date[] salesDate = new Date[1000];
      int userSelection; 
      int artNumAdd;

     // repeat the menu for each choice until the input = 7
     while(true){
         userSelection = menu();

         // check the input if it is 7
         if (userSelection == 7) {
              System.out.println(" Exit! ");
              break;
         }

         // check the input and call its method
         else if(userSelection == 1) {
             System.out.println("Enter the number of articles you want to add: " );       
             artNumAdd = input();
             // Insert articles using insertArticles 
             articles = insertArticles(articles, articleNumber, artNumAdd); 
             articleNumber = articleNumber + artNumAdd;
         }
           
         else if(userSelection == 2){
              System.out.println("Enter the article number you want to remove: ");
              // Remove articles using method removeArticle()
              removeArticle(articles);
         }
           
         else if(userSelection == 3){
              System.out.println(" Items: ");
              printArticles(articles);
         }
           
         else if(userSelection == 4){
              sellArticle(sales, salesDate, articles);
         }

         else if(userSelection == 5){
              System.out.println("Sales History: ");
              printSales(sales, salesDate);
         }

         else if(userSelection == 6){
               // call sorted Table to sort the sales table
               sortedTable(sales, salesDate);
               // print the sales
               printSales(sales, salesDate);
          }
      }
  }

  /** 
   * Method for presenting the menu, loads and returns the user's selection.
   * @return userSelect
   */
 public static int menu() {
      int userSelect;
  
           //print the title
           System.out.println();
           System.out.print("1. Add items"+"\n"+ "2. Remove item"+"\n"+ "3. Show items"+"\n"+ "4. Sales"+"\n"+ "5. Order history" +"\n"+ "6. Sort order history table"+"\n"+ "7. Exit"+"\n"+ "Your choice: ");
  
           //Get the input from the input's method
           userSelect = input();
  
      return userSelect;
}

    
 /**
  * Method for input, reads the user's input and returns an integer.
  * Check if it is integer
  * @return - integer
  */
 public static int input(){

     int in;
     //Use while to repeat until 7
     while(true) {
            // Check if it is an int
            if(userInput.hasNextInt()) {
                  return (userInput.nextInt()); 
             } else {
                  in = userInput.nextInt();
                  return in;
             }
      }
 }

  /**
  * Method to Add items in the matrix 
  * First check that the number of vacancies is sufficient. 
  * @param articles
  * @param articleNumber
  * @param noOfArticles
  * @return matrix of articles
  */
 public static int[][] insertArticles (int[][]articles, int articleNumber, int noOfArticles){
  
         Random newArticle = new Random();
         // call the checkFull method 
         articles = checkFull(articles,noOfArticles);

         //check that the number of vacancies is sufficient.
         for(int i = 0; i < noOfArticles; i++)
         {
            for(int j = 0; j < articles.length; j++)
            {
               if(articles[j][0] == 0)
               {                               
                   int quantity = newArticle.nextInt(10)+1;
                   int price = newArticle.nextInt(1000)+100;
         
               articles[j][articles[0].length-3] = articleNumber;
               articles[j][articles[0].length-2] = quantity;
               articles[j][articles[0].length-1] = price;   

               articleNumber++;
               break;}
         }
      }
       return  articles;
     }


   /** 
    * Method Checks if the matrix holds the specified number of new items
    * If not create new matrix
    * @param articles
    * @param noOfArticles
    * @return
    */
    public static int[][] checkFull(int[][]articles, int noOfArticles){

         int[][] articlesSpase = null; 
         int empty = 0; 

         for(int i = 0; i < articles.length; i++)
         {     
              // check if there is any space 
              if(articles[i][0] == 0)
                  empty++;
               }
              if(noOfArticles <= empty)
               {
                   return articles;
               }
      else if(noOfArticles > empty)
      {
         // creating matrix
         articlesSpase = new int[(articles.length-empty)+ noOfArticles][3];
          for(int roo = 0; roo < articles.length; roo++)
          {
              for(int coo = 0; coo < 3; coo++)
                {articlesSpase[roo][coo]= articles[roo][coo];}
          }
      }
      //return the result 
      return articlesSpase;  
   }   


   /** 
    * Method to remove articles
    * @param articles
    */
   public static void removeArticle (int[][]articles){
       // get the input from user
       int artRemove = input();
       int removeOk = 0;

       for(int i = 0; i < articles.length; i++) {
            // check which article the user wants to remove
            if(articles[i][0] == artRemove)
            {
              
       for( int j = 0; j < articles[j].length; j++) {
             articles[i][j] = 0;
        }
           removeOk = 1;
           break;
             }      
        }
      // check if that article doesn't exist 
      if(removeOk!=1){
         System.err.println("There is no article with this number!"); 
      }
   } 
   

  /** 
    * Method for printing article number, number, and price for all articles in articles that have an article number.
    * @param articles
    */
   public static void printArticles (int[][]articles)
    {
      // print the title
      System.out.println();
      System.out.printf("%-6s %-2s %-3s%n", "  Art  ", "Numb  ","Price");
      
      for (int row = 0; row < articles.length; row++) 
      {              
          for (int columns = 0; columns < articles[row].length; columns++)
          {  
             // check if the article exists, print if it is not empty
             if(articles[row][0] != 0)
             {
                System.out.printf("%6s",articles[row][columns]); }
          }     
        if(articles[row][0] != 0)
         {
         System.out.println();
         }
      } 
   }

/**
  * Method to sell articles, asks for article number and number of items to be sold.
  * If there are enough goods in stock, the number of goods is reduced and a sale is registered 
  * @param sales
  * @param salesDate
  * @param articles
  */ 
 public static void sellArticle(int[][]sales, Date[] salesDate, int[][]articles)
   {
     int itemNotFound=0;
        //Asks for article number and number of items to be sold.
        System.out.println("Inter the article number: ");
        int articleNumber = input();

         System.out.println("Inter the number of items to be sold: ");
         int quantity = input();

      // Checks if there are enough goods in stock. If not, send an error message.
      for (int i = 0; i < articles.length; i++)
      {  
          if(articleNumber == articles[i][0])
          {    itemNotFound = 1;           
               if(quantity > articles[i][1])
               {
                   System.out.println("The item does not have that many units in stock.");
                   break;
                }
               if(quantity <= articles[i][1])
               {   
                   //save the date and time of the transaction 
                   Date now = new Date(); 
              
                   int empty = -1;
                   // Get first empty index in sales array
                   for(int p = 0; p < sales.length; p++) 
                   {
                      if(sales[p][0] == 0)
                      {
                         empty = p;
                         break;
                       }
                   }     
                      //The date and time of the transaction
                      salesDate[empty] = now;    
                      sales[empty][0] = articles[i][0];           
                      sales[empty][1] = quantity;
                      sales[empty][2] = quantity*articles[i][2];
                 
                       articles[i][1] = articles[i][1]-quantity;
                }
          } 
      }
     if(itemNotFound==0){
            System.out.println("Error: This article number doesn't exist.");
          }
     return;
   }

/**
  * Method to print all sales transactions with date, item number, number, and amount.
  * @param sales
  * @param salesDate
  */ 
  public static void printSales(int[][]sales, Date[] salesDate)
   {
        // print the title
        System.out.println();
        System.out.printf("%-8s %-2s %-2s %-16s%n","   Item", " number", " Amount"," Date");

        for (int ro = 0; ro < sales.length; ro++) 
        {  
           // check if the row is not empty
           if( sales[ro][0]!=0 )
           {
               for (int co = 0; co < sales[ro].length; co++)
                  
                  System.out.printf("%7s",sales[ro][co]);
                  System.out.printf("     %1$td.%1$tB.%1$ty %tT %n",salesDate[ro]);
           }
        }
  }

/**
  * Method to sort the selling table by article number, in ascending order.
  * The program shall print the sorted table
  * keeps the correct information about the time and price of the sold articles.
  * @param sales
  * @param salesDate
  */ 
 public static void sortedTable(int[][]sales, Date[] salesDate)
  {
      // define the variables
      int temp;
      Date chengeDate;
     
      for( int i = 0; i < sales.length; i++) 
      {
           for(int j = i + 1; j < sales.length; j++)
           {
             // check if the article number is greater than next one
             if(sales[i][0] > sales[j][0])
                 {
                   for(int col = 0; col < 3; col++)
                    {
                      
                     //swap the article
                     temp = sales[i][col];
                     sales[i][col] = sales[j][col];
                     sales[j][col] = temp;

                     // swap the date of the sales
                     chengeDate = salesDate[i];
                     salesDate[i]= salesDate[j];
                     salesDate[j]= chengeDate;
                    }
                }
           }
      } 
        System.out.println("Sorted history table: ");   
   }
}
