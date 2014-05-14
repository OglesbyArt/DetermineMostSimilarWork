/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */

package oglesby;

import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.util.Date;

public class DetermineMostSimilarWork
{

    public DetermineMostSimilarWork()
    {
        
    }


    //Desc: compares two doubles and returns the larger of the two
    //Pre: the arguments must be doubles
    //Return: the larger of the two doubles
    public static double compareReturnLarger(double d1, double d2)
    {
        if (d1>d2)
            return d1;
        else return d2;
    }
    //Desc: compares two doubles and returns the smaller of the two
    //Pre: the arguments must be doubles
    //Return: the smaller of the two doubles
    public static double compareReturnSmaller(double d1, double d2)
    {
        if (d1<d2)
            return d1;
        else return d2;
    }

    //Desc: Searches the Auctionpainting file for masterpieces by the given 
    //  artist, it then finds the highest coefficient of similarity for that
    //  artist, the auction sales price for that painting witht the highest 
    //  coefficient of similarity is returned
    //Return: the auction sales price for the painting witht the highest 
    //  coefficient of similarity

    public static double findPrice(String alastname,  String med, String sub, double area)
    {
        try
        {
            AuctionPainting ap = new AuctionPainting();
            File paintingsFile = new File ("AuctionPainting.dat");
            boolean found = false;
            double max=0;
            double coeff=0;
            double dummycoeff=0;
            int subjectnumber=0;
            int mediumnumber=0;
            if (paintingsFile.exists())
            {
                
                RandomAccessFile inFile = new RandomAccessFile (paintingsFile, "r");
                while (!found && (inFile.getFilePointer()!=inFile.length()))
                {
                    ap.read (inFile);

                    if (ap.getArtistLastName().equalsIgnoreCase(alastname) )
                    {

                        if (ap.getSubject().equalsIgnoreCase(sub))
                        {
                            
                             subjectnumber=1;
                        }
                            
                        else subjectnumber=0;


                        if(ap.getMedium().equalsIgnoreCase(med))
                        {
                         
                            mediumnumber=1;
                        }
                            
                        else mediumnumber=0;

                        double largerArea=compareReturnLarger(ap.getWidth()*ap.getHeight(), area);
                        double smallerArea=compareReturnSmaller(ap.getWidth()*ap.getHeight(), area);
                        dummycoeff=(mediumnumber+subjectnumber)*smallerArea/largerArea;
                        if(dummycoeff>coeff && (inFile.getFilePointer()==inFile.length()))
                        {
                            found = true;
                            max=ap.getAuctionSalesPrice();
                            coeff=dummycoeff;
                        }
                        else if (dummycoeff>coeff && (inFile.getFilePointer()!=inFile.length()))
                        {
                            max=ap.getAuctionSalesPrice();
                            coeff=dummycoeff;
                        }

                    }
                }

                inFile.close();

            }
            if (coeff==0)
            {
                System.out.println("The coefficient of similarity is zero for this artist.");
                return 0;
            }else

            return max;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: DetermineMostSimilarWork.findPrice () *****");
            System.out.println ("\t" + e);
            return 0;
        }
    }
    
    //Desc: Searches the Auctionpainting file for masterpieces by the given 
    //  artist, it then finds the highest coefficient of similarity for that
    //  artist, the date of auction for that painting witht the highest 
    //  coefficient of similarity is returned
    //Return: the date of auction for the painting witht the highest 
    //  coefficient of similarity
    public static Date findDate(String alastname,  String med, String sub, double area)
    {
        try
        {
            AuctionPainting ap = new AuctionPainting();
            File paintingsFile = new File ("AuctionPainting.dat");
            boolean found = false;
            double max=0;
            double coeff=0;
            double dummycoeff=0;
            int subjectnumber=0;
            int mediumnumber=0;
            Date auctiondate=new Date();
            if (paintingsFile.exists())
            {
                RandomAccessFile inFile = new RandomAccessFile (paintingsFile, "r");
                while (!found && (inFile.getFilePointer()!=inFile.length()))
                {
                    ap.read (inFile);

                    if (ap.getArtistLastName().equalsIgnoreCase(alastname) )
                    {
                        if (ap.getSubject().equalsIgnoreCase(sub))
                             subjectnumber=1;
                        else subjectnumber=0;


                        if(ap.getMedium().equalsIgnoreCase(med))
                            mediumnumber=1;
                        else mediumnumber=0;

                        double largerArea=compareReturnLarger(ap.getWidth()*ap.getHeight(), area);
                        double smallerArea=compareReturnSmaller(ap.getWidth()*ap.getHeight(), area);
                        dummycoeff=(mediumnumber+subjectnumber)*smallerArea/largerArea;
                        if(dummycoeff>coeff && (inFile.getFilePointer()==inFile.length()))
                        {
                            found = true;
                            auctiondate=ap.getDateofAuction();
                            coeff=dummycoeff;
                        }
                        else if (dummycoeff>coeff && (inFile.getFilePointer()!=inFile.length()))
                        {
                            auctiondate=ap.getDateofAuction();
                            coeff=dummycoeff;
                        }


                    }
                }

                inFile.close();

            }

            return auctiondate;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: DeterminMostSimilarWork.findDate () *****");
            System.out.println ("\t" + e);
            return new Date();
        }
    }
        
    //Desc:uses the last name and the first name of an artist to find a record
    //     in the file
    //Return: returns the fashionability value for that artist
   public int findFashionabilityValue(String afirstname, String alastname)
    {

        try
        {
            Artist a = new Artist();
            File artistFile = new File ("artist.dat");
            boolean found = false;
            int fashionability=0;
            if (artistFile.exists())
            {
                RandomAccessFile inFile = new RandomAccessFile (artistFile, "r");


                while (!found && (inFile.getFilePointer()!=inFile.length()))
                {
                    a.read (inFile);
                    if (a.getArtistLastName().equalsIgnoreCase(alastname) &&
                    a.getArtistFirstName().equalsIgnoreCase(afirstname))
                    {
                        found = true;
                    fashionability=a.getArtistFashionabilityValue();
                    }
                }
                inFile.close();
            }
            return fashionability;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: DetermineMostSimilarWork.findFashionabilityValue () *****");
            System.out.println ("\t" + e);
            return 0;
        }
  }
}

