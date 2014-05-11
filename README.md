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



class DetermineOtherWorkPrice {

private String artistFirstName;
private String artistLastName;
private Date dateOfWork;
private double height;
private double width;
private String medium;
private String subject;
private double suggestedMaximumPurchasePrice;

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
    public  void executeDetermineOtherWorkPrice()
    {
       BoughtPainting bp = new BoughtPainting();

        bp.readInRecord();
        artistFirstName= bp.getArtistsFirstName();
        artistLastName=bp.getArtistLastName();
        dateOfWork= bp.getDateofWork();
        height=bp.getHeight();
        width=bp.getWidth();
        medium=bp.getMedium();
        subject=bp.getSubject();


        suggestedMaximumPurchasePrice=calculateOtherWorkPrice();

        if ( userBuyChoice(suggestedMaximumPurchasePrice))

                bp.addRecentlyBought();

        else
        UserInterface.pressEnter();
    }

    //Desc: calculate the price for the Masterwork the user wants to buy
    //Pre: there must be a most similar work and that work must have a an
    //  auction purchase price, the user must have entered
    //  the date of the work correctly
    //Return: the price of the Masterwork
    public double calculateOtherWorkPrice()
    {

        Artist ap = new Artist();

    	int fashionability=ap.findFashionabilityValue(artistFirstName, artistLastName);
        if (fashionability==0)
        {
            UserInterface.pressEnter();
        }

        double otherWorkPrice=fashionability*height*width;

        return otherWorkPrice;


    }


    //Desc: display a value to the user and the user responds
    //  which is returned as a true or false value
    //Pre: the argument must be a double value
    //Return: a boolean value based on the user’s input
    public static boolean userBuyChoice(double d)
    {
    	System.out.println("The price is" +d +". Do you want to buy? y/n");
    	String choice=UserInterface.getString();
        while (!choice.equalsIgnoreCase("y")&&!choice.equalsIgnoreCase("n"))
        {
            System.out.println("Please enter the correct format, either y or n");
            System.out.println("The price is" +d +". Do you want to buy? y/n");
            choice=UserInterface.getString();
        }

        if (choice.equalsIgnoreCase("y")) return true;
        else return false;


    }

}
