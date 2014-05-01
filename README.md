DetermineOtherWorksPrice
========================
import java.util.*;

public class DetermineOtherWorkPrice
{

private String artistFirstName;
private String artistLastName;
private String titleOfWork;
private String classification;
//private date dateOfWork;
private double height;
private double width;
private String medium;
private String subject;
private double suggestedMaximumPurchasePrice;



    //Desc: constructor for DetermineOtherWorkPrice
	//Post: allows class to set the value of all Painting fields 
    // in a record
    public DetermineOtherWorkPrice(String fname, String lname, String work, String clas, double h,double w, String med, String sub, double max)
    {
		artistFirstName=fname;
		artistLastName=lname;
		titleOfWork=work;
	//	dateOfWork=dwork
		classification=clas;
		height=h;
		width=w;
		medium=med;
		subject=sub;
		suggestedMaximumPurchasePrice=max;
    }

    
   //Desc: get the fashionability value for the artist of the 
    // painting in question
    //Pre: the fashionability value for the artist must exist in 
    // the artist file, if it doesn’t the method returns 0
    //Return: the fashionability value for the artist or 0
    public static double getFashionabilityValue()
    {
    	//instentiate Artist object ;
    	//artist.find(artistLastName, artistFirstName) ;
    	//artistfile.get(fashionabilityvalue);
    	double fashionabilityValue=0;
    	return fashionabilityValue;
    }

    //Desc: calculate the price for the “Other Work” that the user wants to buy
    //Pre: the area of the painting and the fashionability value must exist
    //Return: the price for the “Other Work”
    public double calculateOtherWorkPrice()
    {
    	double fashionability=getFashionabilityValue();
    	double area=width*height;
    	return fashionability*area;
    }
}
