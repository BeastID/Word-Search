# Word-Search-And-Count
import java.util.*;
import java.io.*;
public class Hamlet2
{
    public static void main(String[]args) throws FileNotFoundException
    {
        File f = new File(".txt");
        //Put the name of file we need to search
        Scanner read = new Scanner(f);
        int tokenCount = 0;
        while(read.hasNext())
        {
            String and = read.next();
            boolean Word = and.equalsIgnoreCase("and");
            //Count the word "and"
            if (Word){
            tokenCount++;}
        }
        System.out.println(" Total words: " + tokenCount);
    }
}
