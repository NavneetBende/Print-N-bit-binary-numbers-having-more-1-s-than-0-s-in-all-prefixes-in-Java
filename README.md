# Print-N-bit-binary-numbers-having-more-1-s-than-0-s-in-all-prefixes-in-Java

N-bit binary numbers having more  or equal 1’s than 0’s in Java
Here, in this page we will discuss the program to print n-bit binary numbers having more or equal 1’s than 0’s in Java programming language. We are given with an integer value n, and need to print n-bit binary numbers.

 

N-bit binary numbers
Method Discussed :
Method 1 : Using Recursive Way
Method 2 : Using  Non-Recursive Way
Let’s discuss them one by one in brief,

Method 1:
In this method we use recursion. At each point in the recursion, we append 0 and 1 to the partially formed number and recur with one less digit. 

Method 1 : Code in Java
Run
import java.io.*;
 
class Main {
    static void printRec(String number, int extraOnes, int remainingPlaces)
    {
        if (0 == remainingPlaces) {
            System.out.print(number + " ");
            return;
        }
 
        printRec(number + "1", extraOnes + 1, remainingPlaces - 1);
 
        if (0 < extraOnes)
            printRec(number + "0", extraOnes - 1, remainingPlaces - 1);
    }
 
    static void printNums(int n)
    {
        String str = "";
        printRec(str, 0, n);
    }
 
    public static void main(String[] args)
    {
        int n = 4;
       
        printNums(n);
    }
}
Output :
1111 1110 1101 1100 1011 1010
Method 2:
In this non-recursive method , the idea is to directly generate the numbers in the range of 2^N to 2^(N-1), then require only these which satisfies the condition

N-bit binary numbers having more or equal 1's than or equal 0's
Method 2 : Code in Java
Run
import java.io.*;
import java.util.*;
class Main
{
 
  static String getBinaryRep(int N, int num_of_bits)
  {
    String r = "";
    num_of_bits--;
 
    while (num_of_bits >= 0)
    {
      if ((N & (1 << num_of_bits))!=0)
        r += "1";
      else
        r += "0";
      num_of_bits--;
    }
    return r;
  }
 
  static ArrayList NBitBinary(int N)
  {
    ArrayList r = new ArrayList();
    int first = 1 << (N - 1);
    int last = first * 2;

    for (int i = last - 1; i >= first; --i)
    {
      int zero_cnt = 0;
      int one_cnt = 0;
      int t = i;
      int num_of_bits = 0;
 
      while (t > 0)
      {
        if ((t & 1) != 0)
          one_cnt++;
        else
          zero_cnt++;
        num_of_bits++;
        t = t >> 1;
      }
 
      if (one_cnt >= zero_cnt)
      {
        boolean all_prefix_match = true;
        int msk = (1 << num_of_bits) - 2;
        int prefix_shift = 1;
        while (msk > 0)
        {
 
          int prefix = (msk & i) >> prefix_shift;
          int prefix_one_cnt = 0;
          int prefix_zero_cnt = 0;
          while (prefix > 0)
          {
            if ((prefix & 1)!=0)
              prefix_one_cnt++;
            else
              prefix_zero_cnt++;
            prefix = prefix >> 1;
          }
          if (prefix_zero_cnt > prefix_one_cnt)
          {
            all_prefix_match = false;
            break;
          }
          prefix_shift++;
          msk = msk & (msk << 1);
        }
        if (all_prefix_match)
        {
          r.add(getBinaryRep(i, num_of_bits));
        }
      }
    }
    return r;
  }
 
  
  public static void main (String[] args)
  {
 
    int n = 4;

    ArrayList results = NBitBinary(n);
    
    for (int i = 0; i < results.size(); ++i)
      System.out.print(results.get(i)+" ");
    
    System.out.println();
  }
}
Output :
1111 1110 1101 1100 1011 1010 
