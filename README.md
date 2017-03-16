package anju_new;
import java.util.ArrayList;
import java.util.Random;


public class projectfinal1 {
	//variables to check the comparisons and assignments in sorting method

	public static int assignment,comparison;
	public static int TOTAL_ELEMENTS = 2;

	/*FUNCTION TO PRINT ARRAY WITH EACH ELEMENT SEPERATED BY COMMA AND EACH LINE CONTAINIING Twenty ELEMENTS resulting in a total of 50 lines.*/

	public void print(ArrayList<Integer> array)
	{
		int j=0;
		System.out.println();
		for(int n:array)
		{
			j++;
			System.out.print(n+", ");
			if(j%20==0)
			{
				System.out.println();
			}
		}
		System.out.println("\n---------------------------");
	}

	/*SORTING ARRAY USING INSERTION SORT.*/

	public void sortarray(ArrayList<Integer> array1)
	{
		assignment=0;comparison=0;	
		for(int i=1;i<array1.size();i++)
		{
			assignment=assignment+1;
			int temp = array1.get(i);
			int k=-1;
			for( int j=i-1;j>=0;j--)
			{
				comparison = comparison+1;
				if(array1.get(j)>temp) 
				{
					array1.set(j+1,array1.get(j));
					assignment=assignment+1;
					k=j;				
				}
			}  
			if(k!=-1)
			{
				array1.set(k,temp);
				assignment=assignment+1;
			}
		}
		assignment=0;comparison=0;	
	}

	/*Linear search based insertion*/

	public void linearinsertion(ArrayList<Integer> array1,int num)
	{ 
		long time_start = System.currentTimeMillis();	
		projectfinal1 f = new projectfinal1();
		int i=0;
		ArrayList<Integer> array2 = new ArrayList<>(array1);
		f.sortarray(array2);
		while(i<array2.size())
		{	
			comparison++;
			if(array2.get(i)>=num)
			{
				break;

			}
			i++;
		}
		array2.add(i, num);	
		assignment+=array2.size()-i; // calculating assignments in array2.add operation of element num . 
		long time_end = System.currentTimeMillis();
		long time_taken = time_end-time_start;
		System.out.println("\n---------------------------");
		System.out.println("Total number of assignments in linear insertion is " + (assignment) + 
				"\n" +"Total number of comparisons  in linear insertion is "+ (comparison));
		System.out.println("Time taken is "+time_taken+ " milliseconds");
		System.out.println();
		//f.print(array2);
	}

	/*binary search based insertion */

	public void binaryinsertion(ArrayList<Integer> array1,int num)
	{
		long time_start=System.currentTimeMillis(); //difference of time1 and time2 to measure the total time taken for the function to execute insertion
		//int comparison=0;              //variables for assignments and comparisons for the given array array2
		projectfinal1 f = new projectfinal1();
		ArrayList<Integer> array2 = new ArrayList<>(array1); //creating a new temporary array list to store the elements
		f.sortarray(array2);  //  sorting the array
		//int size = array2.size()-1;   //size,mid, mfirst, mlast are variables used in calculation of new mid in each iteration
		int mid = Math.round((array2.size()-1)/2);
		int mfirst =0;
		int mlast = array2.size()-1;

		
		while(true)
		{  
			comparison++;
			if(num<=array2.get(mid))   // checking if num is found to the left of index mid
			{   

				if(mid-mfirst==1)     //ends loop if there is only one element left for comparison with num
				{

					comparison++;
					if(num<=array2.get(mfirst)) //compares num with last element
					{
						mid =mid-1;
					}

					break;
				} 
				mlast = mid;
				mid =Math.round(( mfirst+mid)/2); //calculate new value of mid

			}
			else  //  num is found to the right  of index mid
			{

				if(mlast-mid==1)             // ends iteration once there is only one element left for comparison
				{    
					comparison++;
					if(num>=array2.get(mlast))   //comparing with last element left for comparison in the array 
					{
						mid=mid+1;
					}
					mid = mid+1;
					break;
				}
				mfirst = mid;
				mid = Math.round((mid+mlast)/2); //finding new value of mid
			}
		}
		System.out.println("\n---------------------------");
		array2.add(mid, num);
		assignment+= array2.size() -mid;
		long time_end = System.currentTimeMillis();
		long time_taken = time_end-time_start;
		System.out.println("Total number of assignments in binary insertion is " + (assignment) + 
				"\n" +"Total number of comparisons  in binary insertion is "+ (comparison));
		System.out.println("Time taken is "+time_taken);
		f.print(array2);
	}

	public static void main(String[] args)
	{

		projectfinal1 f = new projectfinal1();

		ArrayList<Integer> array1 = new ArrayList<Integer>();
		Random r = new Random();
		for(int i=0;i<TOTAL_ELEMENTS;i++) // using random function to generate 1000 integers
		{
			int num = r.nextInt(TOTAL_ELEMENTS)+1;
			array1.add(num);
		}
		int insertno = r.nextInt(TOTAL_ELEMENTS); //the number to be used for binary and linear insertion
		f.print(array1);  //printing unsorted array.

		System.out.println("Inserted element: " +insertno); 
		f.linearinsertion(array1,insertno); //calling linear search insertion
		f.binaryinsertion(array1, insertno); //calling binary search insertion

	}





}
