using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace CS13
{
    class quadro
    {
        private int[] sides = new int[4];
        private int perimeter;
        private double area;
        public int type;
        public quadro(int s1, int s2, int s3, int s4)
        {
            sides[0] = s1;
            sides[1] = s2;
            sides[2] = s3;
            sides[3] = s4;
            perimeter = s1 + s2 + s3 + s4;
            int p = (s1 + s2 + s3 + s4) / 2;
            area = Math.Sqrt((double)((p - s1) * (p - s2) * (p - s3) * (p - s4)));
            Console.Write("Периметр равен: {0}\n", perimeter);
            Console.Write("Площадь равна: {0}\n", Math.Round(area, 2));
        }
        public void what_is_that()
        {
            type = 0; //0 - разносторонний, 1 - квадрат, 2 - ромб, 3 - паралелограмм
            int tmp = 0;
            for (int i = 0; i < 3 && type == 0; i++)
                for (int j = i + 1; j < 4; j++)
                {
                    if (sides[i] == sides[j])
                        tmp++;
                    if(i == 0 && tmp == 3)
                    {
                        type = 2;
                        break;
                    }
                }
            if (tmp == 2)
                type = 3;

            switch(type)
            {
                case 0:
                    Console.Write("Разносторонний четырехугольник\n");
                    break;
                case 2:
                    Console.Write("Квадрат или ромб, мы не можем точно определить только по сторонам\n");
                    break;
                case 3:
                    Console.Write("Паралелограмм\n");
                    break;
            }             
        }
        public void func2(int angle)
        {
            if (angle == 90 && type == 2)
            {
                type = 1;
                Console.Write("Считаем, что это квадрат\n");
            }
            else if(type == 2)
                Console.Write("Считаем, что это ромб\n");

            //A - 1/4, B - 1/2, C - 2/3, D - 3/4
            //Используем угол A, т.е между первой и четвертой длинами

            double d = Math.Sqrt(sides[0]*sides[0]+sides[3]*sides[3]-2*sides[0]*sides[3]*Math.Cos(angle*Math.PI/180));

            Console.Write("Полученная диагональ равна: {0}\n", d);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Введите длины сторон:\n");
            int s1 = Convert.ToInt32(Console.ReadLine());
            int s2 = Convert.ToInt32(Console.ReadLine());
            int s3 = Convert.ToInt32(Console.ReadLine());
            int s4 = Convert.ToInt32(Console.ReadLine());
            Console.Write("Введите угол от 1 до 180 для рассчетов:\n");
            int angle = Convert.ToInt32(Console.ReadLine());
            quadro t = new quadro(s1, s2, s3, s4);
            t.what_is_that();
            t.func2(angle);
            Console.ReadKey();
        }
    }
}
