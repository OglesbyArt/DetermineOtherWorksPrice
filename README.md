/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */

/**
 *
 * @author katiejesperson
 */
 package oglesby;

import java.util.*;
import java.text.*;



class DetermineOtherWorkPrice {

    //Desc: constructor for DetermineOtherWorkPrice
    //Post: Creates a new DetermineOtherWorkPrice
    public DetermineOtherWorkPrice()
    {
        executeDetermineOtherWorkPrice();
    }

    //Desc: Executes the major methods that allow a user to buy a painting.
    //  First the user must input values, then the user will view the
    //  suggested price. If the user chooses by buy then the bought painting
    //  file will be updated, otherwise the user can go back to the main
    //  menu
    //Pre: The coefficient of similarity must not be zero, otherwise
    //  the user is not interested in buying the painting.
    //Post: The user will have viewed the suggested maximum price for
    //  the painting they want to buy. If they chose to buy it, the files are
    //  now updated accordingingly.
    public static void executeDetermineOtherWorkPrice()
    {
       BoughtPainting bp = new BoughtPainting();

        bp.readInRecord();
        bp.setClassification("Other");
        double area =bp.getHeight()*bp.getWidth();
        boolean choice=false;
        double suggestedMaximumPurchasePrice=calculateOtherWorkPrice(bp.getArtistsFirstName(), bp.getArtistLastName(),area);

        if (suggestedMaximumPurchasePrice==0)
        {
            System.out.println("The Fashionability value for this artist either does not exist or is zero");
            choice=false;
        }
        else choice = userBuyChoice(suggestedMaximumPurchasePrice);
        if ( choice)
        {
            bp.setSuggestedMaximumPurchasePrice(suggestedMaximumPurchasePrice);
            bp.addRecentlyBought();
            System.out.println("");
             System.out.println("Press <ENTER> to return to the Buy menu.");
            UserInterface.pressEnter();
        }

        else
        {
            System.out.println("");
            System.out.println("Press <ENTER> to return to the Buy menu.");
            UserInterface.pressEnter();
        }
    }

    //Desc: calculate the price for the Masterwork the user wants to buy
    //Pre: there must be a most similar work and that work must have a an
    //  auction purchase price, the user must have entered
    //  the date of the work correctly
    //Return: the price of the Masterwork
    public static double calculateOtherWorkPrice(String artistFirstName, String artistLastName, double area)
    {

        DetermineMostSimilarWork ap = new DetermineMostSimilarWork();

    	int fashionability=ap.findFashionabilityValue(artistFirstName, artistLastName);
        if (fashionability==0)
        {

            return 0;
        }


        double otherWorkPrice=fashionability*area;

        return otherWorkPrice;


    }


    //Desc: display a value to the user and the user responds
    //  which is returned as a true or false value
    //Pre: the argument must be a double value
    //Return: a boolean value based on the user’s input
    public static boolean userBuyChoice(double d)
    {
    	DecimalFormat dec = new DecimalFormat("#.##");
        DecimalFormat comma = new DecimalFormat("#,###.00");
        double doubleComma =Double.parseDouble(dec.format(d));
        System.out.println("The Suggested Maximum Purchase Price is $" +comma.format(doubleComma) +". Do you want to buy? y/n");
    	String choice=UserInterface.getString();
        while (!choice.equalsIgnoreCase("y")&&!choice.equalsIgnoreCase("n"))
        {
            System.out.println("Please enter the correct format, either y or n");
            System.out.println("The Suggested Maximum Purchase Price is $" +comma.format(doubleComma) +". Do you want to buy? y/n");
            choice=UserInterface.getString();
        }

        if (choice.equalsIgnoreCase("y")) return true;
        else return false;


    }

}
