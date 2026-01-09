using System;

class ReportCard
{
    static void Main()
    {
        Console.Write("Enter Total Students : ");
        int totalStudents;

        while (!int.TryParse(Console.ReadLine(), out totalStudents) || totalStudents <= 0)
        {
            Console.Write("Invalid input. Enter a valid number of students: ");
        }

        // Multi-dimensional array to store:
        // [i,0] = Name, [i,1] = English, [i,2] = Math, [i,3] = Computer, [i,4] = Total
        string[,] students = new string[totalStudents, 5];

        for (int i = 0; i < totalStudents; i++)
        {
            Console.WriteLine("*********************************************");

            Console.Write("Enter Student Name : ");
            students[i, 0] = Console.ReadLine();

            students[i, 1] = ReadMarks("Enter English Marks (Out Of 100) : ");
            students[i, 2] = ReadMarks("Enter Math Marks (Out Of 100) : ");
            students[i, 3] = ReadMarks("Enter Computer Marks (Out Of 100) : ");

            int total = int.Parse(students[i, 1]) +
                        int.Parse(students[i, 2]) +
                        int.Parse(students[i, 3]);

            students[i, 4] = total.ToString();
        }

        // Sort by Total Marks (Descending)
        for (int i = 0; i < totalStudents - 1; i++)
        {
            for (int j = i + 1; j < totalStudents; j++)
            {
                if (int.Parse(students[j, 4]) > int.Parse(students[i, 4]))
                {
                    // Swap all columns
                    for (int k = 0; k < 5; k++)
                    {
                        string temp = students[i, k];
                        students[i, k] = students[j, k];
                        students[j, k] = temp;
                    }
                }
            }
        }

        Console.WriteLine("****************Report Card*******************");

        for (int i = 0; i < totalStudents; i++)
        {
            Console.WriteLine("****************************************");
            Console.WriteLine($"Student Name: {students[i, 0]}, Position: {i + 1}, Total: {students[i, 4]}/300");
            Console.WriteLine("****************************************");
        }
    }

    static string ReadMarks(string prompt)
    {
        int marks;
        Console.Write(prompt);

        while (!int.TryParse(Console.ReadLine(), out marks) || marks < 0 || marks > 100)
        {
            Console.Write("Invalid input. Enter marks between 0 and 100: ");
        }

        return marks.ToString();
    }
}
