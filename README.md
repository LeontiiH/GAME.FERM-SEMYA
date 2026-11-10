# GAME.FERM-SEMYA
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _21212321 
{ 
using System;
namespace TextRpgPrototype
{
    class Program
    {
        const int MapWidth = 20;
        const int MapHeight = 5;
        const int BaseDefensePower = 5;

        static void Main(string[] args)
        {
            Console.OutputEncoding = System.Text.Encoding.UTF8;

            string heroName = "Конан";
            int heroHealth = 100;
            int heroMaxHealth = 100;
            int heroGold = 50;

            int playerPositionX = 3;
            int playerPositionY = 2;

            bool isGameRunning = true;

            Console.WriteLine("Добро пожаловать в прототип текстовой RPG!");
            Console.WriteLine("Нажмите любую клавишу для начала...");
            Console.ReadKey();

            while (isGameRunning)
            {
                Console.Clear();

                Console.WriteLine($"--- ИГРОВОЙ ЭКРАН (Размер: {MapWidth}x{MapHeight}) ---");
                for (int y = 0; y < MapHeight; y++)
                {
                    for (int x = 0; x < MapWidth; x++)
                    {
                        if (x == playerPositionX && y == playerPositionY)
                        {
                            Console.Write("@");
                        }
                        else if (x == 0 || x == MapWidth - 1 || y == 0 || y == MapHeight - 1)
                        {
                            Console.Write("#");
                        }
                        else
                        {
                            Console.Write(".");
                        }
                    }
                    Console.WriteLine();
                }

                Console.WriteLine("\n--- СТАТУС ГЕРОЯ ---");
                Console.WriteLine($"Имя: {heroName} | Здоровье: {heroHealth}/{heroMaxHealth} | Золото: {heroGold} койн(ов)");
                Console.WriteLine($"Позиция на карте: [{playerPositionX}, {playerPositionY}]");
                Console.WriteLine("--------------------");

                Console.WriteLine("\nДоступные команды:");
                Console.WriteLine("1 - Шагнуть вглубь подземелья (Ловушка с уроном)");
                Console.WriteLine("2 - Найти мешок с золотом");
                Console.WriteLine("0 - Выйти из игры");
                Console.Write("\nВведите номер команды: ");

                string playerInput = Console.ReadLine();

                switch (playerInput)
                {
                    case "1":
                        Console.Write("\nВы наступили на скрытую ловушку! Введите силу ловушки (число от 10 до 50): ");
                        string damageInput = Console.ReadLine();

                        if (int.TryParse(damageInput, out int rawDamage))
                        {
                            int finalDamage = rawDamage - BaseDefensePower;

                            if (finalDamage < 0) finalDamage = 0;

                            heroHealth -= finalDamage;

                            if (heroHealth < 0) heroHealth = 0;

                            Console.WriteLine($"\nЛовушка нанесла вам {finalDamage} урона (чистый урон {rawDamage} - {BaseDefensePower} защиты)!");
                        }
                        else
                        {
                            Console.WriteLine("\n[Ошибка]: Вы ввели не-число! Ловушка заклинила, урон не нанесён.");
                        }
                        break;

                    case "2":
                        int foundGold = 15;
                        heroGold += foundGold;
                        Console.WriteLine($"\nВы нашли {foundGold} монет!");
                        break;

                    case "0":
                        isGameRunning = false;
                        Console.WriteLine("\nСпасибо за игру!");
                        break;

                    default:
                        Console.WriteLine("\nНеизвестная команда. Попробуйте еще раз.");
                        break;
                }

                if (heroHealth <= 0)
                {
                    Console.WriteLine("\nГерой погиб! Игра окончена.");
                    isGameRunning = false;
                }

                Console.WriteLine("\nНажмите любую клавишу, чтобы продолжить...");
                Console.ReadKey();
            }
        }
    }
}
}
