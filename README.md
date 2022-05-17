# calc
class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();
        calc.Run();
        Console.ReadKey();
    }
}

class Calculator
{
    string[] nums;
    string[] signs;

    public void Run()
    {
        Input();
        int result = Calculate(0, Convert.ToInt32(nums[0], 2), Convert.ToInt32(nums[1], 2));
        Console.WriteLine("Результат: " + Convert.ToString(result, 2));
    }

    void Input()
    {
        Console.Write("Введите пример, разделяя значения пробелом:  ");
        string[] parts = Console.ReadLine().Split(' ');

        signs = new string[(parts.Length - 1) / 2];
        for (int i = 0; i < signs.Length; i++)
            signs[i] = parts[i * 2 + 1];

        nums = new string[(parts.Length - 1) / 2 + 1];
        for (int i = 0; i < nums.Length; i++)
            nums[i] = parts[i * 2];
    }

    int Calculate(int signIndex, int a, int b)
    {
        int result = 0;
        switch (signs[signIndex])
        {
            case "+": result = a + b; break;
            case "-": result = a - b; break;
            case "*": result = a * b; break;
            case "/": result = a / b; break;
        }
        if (signIndex == signs.Length - 1)
            return result;
        signIndex++;
        return Calculate(signIndex, result, Convert.ToInt32(nums[signIndex + 1], 2));
    }
}
