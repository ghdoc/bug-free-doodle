- Array

- Multi-Dimensional (rectangular) [,]
             //Assigning the array elements at the time of declaration
             int[,] arr = {{11,12,13,14},
                           {21,22,23,24},
                           {31,32,33,34}};
             //printing values of array using for each loop
             foreach (int i in arr)
             {
                 Console.Write(i + " ");
             }
             Console.WriteLine("\n");
             //printing the values of array using nested for loop
             for (int i = 0; i < arr.GetLength(0); i++)
             {
                 for (int j = 0; j < arr.GetLength(1); j++)
                 {
                     Console.Write(arr[i, j] + " ");
                 }
             }
             
- Jagged (array of arrays) [][]  
    static void Main(string[] args)
         {
             //Creating an jagged array with four rows
             int[][] arr = new int[4][];
             //Initializing each row with different column size
             // Uisng one dimensional array
             arr[0] = new int[5];
             arr[1] = new int[6];
             arr[2] = new int[4];
             arr[3] = new int[5];
             //printing the values of jagged array using nested for loop
             //It will print the default values as we are assigning any
             //values to the array
             for (int i = 0; i < arr.GetLength(0); i++)
             {
                 for (int j = 0; j < arr[i].Length; j++)
                 {
                     Console.Write(arr[i][j] + " ");
                 }
             }
             Console.WriteLine();
             //assigning values to the jagged array by using nested for loop
             for (int i = 0; i < arr.GetLength(0); i++)
             {
                 for (int j = 0; j < arr[i].Length; j++)
                 {
                     arr[i][j] = j++;
                 }
             }
             //print values the values of jagged array by using foreach loop within for loop
             for (int i = 0; i < arr.GetLength(0); i++)
             {
                 foreach (int x in arr[i])
                 {
                     Console.Write(x + " ");
                 }
             }
             Console.ReadKey();
         }

- Bulk Upgrade dotnet framwork on csproj project files

- Using VS Extension "Target Framework Migrator" by Pavel
- [https://github.com/TargetFrameworkMigrator/TargetFrameworkMigrator](https://github.com/TargetFrameworkMigrator/TargetFrameworkMigrator)

- Remove old *.lock.json *.dgspec.json *.assets.json by del /s *.lock.json recursively removes files matching extensions

- Build csproj from commandline  
    D:\Users\sdivekar\Documents\Git\standard-widgets\OEMS.Common>nuget pack OEMS.Common.csproj   -Properties "Configuration=Release;Platform=AnyCPU" -Verbosity Detailed