DetermineMostSimilarWork
========================

public class DetermineMostSimilarWork 
{

     //Desc: Compares two strings and returns a 1 if the strings match and 
    // 0 if the strings do not match
    //Pre: the arguments must be strings
    //Return: 1 if the strings match and 0 if they do not match
    public static int computeScore(String s1, String s2)
    {
        if (s1.equals(s2))
            return 1;
        else return 2;
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

    
    //Desc: computes the coefficient of similarity based on the given values
    //Pre: the arguments must be an int, a double and a double
    //Return: the coefficient of similarity
    public static double computeCoefficientofSimilarity(int i, double d1, double d2)
    {
        return i*d1/d2;
    }
}
