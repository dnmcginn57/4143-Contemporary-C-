```csharp
//David McGinn
// 9-8-18
//CMPS 4143
//This program takes in two numbers, 
//  Displays the sum, average, and largest and smallest of the numbers

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Program_2
{
    class Program
    {
        static void Main(string[] args)
        {
            int num1, num2, sum, average, test = 1;
            bool res;

            //A while loop to make testing easier
            while (test != 0)
            {
                Console.Write("Enter first interger: ");
                res = int.TryParse(Console.ReadLine(), out num1);

                if (!res) //if statement to skip on invalid entry
                {
                    Console.WriteLine("that is invalid :( \n");
                }
                else
                {
                    Console.Write("Enter second interger: ");
                    res = int.TryParse(Console.ReadLine(), out num2);

                    if (!res)
                    {
                        Console.WriteLine("that is invalid :( \n");
                    }
                    else
                    {

                        sum = num1 + num2;
                        average = sum / 2;

                        Console.WriteLine("Sum: " + sum);
                        Console.WriteLine("Average: " + average);

                        if (num1 > num2)
                        {
                            Console.WriteLine(num1 + " is the largest");
                            Console.WriteLine(num2 + " is the smallest");
                        }
                        else if (num2 > num1)
                        {
                            Console.WriteLine(num2 + " is the largest");
                            Console.WriteLine(num1 + " is the smallest");
                        }
                        else
                        {
                            Console.WriteLine("these numbers are equal");
                        }
                    }
                }

                Console.WriteLine("\n press 0 to quit ");
                res = int.TryParse(Console.ReadLine(), out test);
                Console.WriteLine();

            }//while loop ends here
        }
    }
}

```
