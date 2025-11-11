# c-
个人的一大步！
using Microsoft.VisualBasic;

namespace 飞行棋游戏
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Gametitle();//输入姓名，初始化
            #region(输入姓名)
            Console.WriteLine("请输入玩家a的姓名");
            player[0] = Console.ReadLine();//接收玩家a名字

            while (player[0] == " ")//判断a名字不为空格
            {
                Console.WriteLine("姓名不能为空，请重新输入");
                player[0] = Console.ReadLine();
            }

            Console.WriteLine("请输入用户b的姓名");//接收玩家b名字
            player[1] = Console.ReadLine();//接收b名字
            bool a;
            while (a = true)//判断b名字不相同a且不为空格
            {
                if (player[1] == " ")
                {
                    Console.WriteLine("姓名不能为空，请重新输入");
                    player[1] = Console.ReadLine();
                }
                else if (player[1] == player[0])
                {
                    Console.WriteLine("玩家名b不能和玩家名a相同，请重新输入");
                    player[1] = Console.ReadLine();
                }
                else if (player[1] == " ")
                {
                    Console.WriteLine("姓名不能为空，请重新输入");
                    player[1] = Console.ReadLine();
                }
                else
                {
                    a = false;
                    break;
                }//else if结尾
            }//while结尾
            Console.ReadKey();

            #endregion
            Console.Clear();//清屏
            Gametitle();
            Console.WriteLine("{0}的士兵用A表示", player[0]);
            Console.WriteLine("{0}的士兵用B表示", player[1]);
            InitialMaps();
            Drawmap();

            //当玩家A跟玩家B没有一个人在终点时，不停循环
            while (Gameplayer[0] < 99 && Gameplayer[1] < 99)
            {
                if (Flags[0] == false)
                {
                    PlayGame(0);
                }
                else
                {
                    Flags[0] = false;
                }

                if (Flags[1] == false)
                {
                    PlayGame(1);
                }
                else
                {
                    Flags[1] = false;
                }

                if (Gameplayer[0] >= 99)
                {
                    Console.WriteLine("玩家{0}幸运的赢了玩家{1}", player[0], player[1]);
                }
                if (Gameplayer[1] >= 99)
                {
                    Console.WriteLine("玩家{0}幸运的赢了玩家{1}", player[1], player[0]);
                }
                //ChangePos();               
            }//while

            Console.WriteLine("超级大胜利！！！！！！！！！！！！！！");
            Console.WriteLine("超级大胜利！！！！！！！！！！！！！！");
            Console.WriteLine("超级大胜利！！！！！！！！！！！！！！");
            Console.ReadKey();
        }//main

        #region (游戏头Gametitle)
        public static void Gametitle()
        {
            Console.ForegroundColor = ConsoleColor.Red;//给文字上颜色，前景色
            Console.WriteLine("*****************************");
            Console.ForegroundColor = ConsoleColor.Magenta;
            Console.WriteLine("*****************************");
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("*****************************");
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine(".Net基础班2025.11.3飞行棋游戏");
            Console.ForegroundColor = ConsoleColor.Cyan;
            Console.WriteLine("*****************************");
            Console.ForegroundColor = ConsoleColor.Gray;
            Console.WriteLine("*****************************");
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.WriteLine("*****************************");
        }//Gametitle结尾


        #endregion

        #region(声明各种东西，地图长度，字段全局变量maplenth)
        public static int[] MapLenth = new int[100];//地图长度数组，静态字段模拟全局变量
        public static int[] Gameplayer = new int[2];
        public static string[] player = new string[2];
        static bool[] Flags = new bool[2];//Flag[0]，[1]默认都是false
        #endregion

        #region(初始化地图InitialMaps)
        /// <summary>
        /// 初始化地图
        /// </summary>
        public static void InitialMaps()
        {

            //其他的格子为□  
            int[] Luckyturn = { 6, 23, 40, 55, 69, 83 };//幸运轮盘◎，幸运轮盘在地图数组的位置
            for (int i = 0; i < Luckyturn.Length; i++)//每个道具赋值编号
            {
                MapLenth[Luckyturn[i]] = 1;//地图数组[道具数组在地图数组的位置]，int数组默认值为0,改为不同值
            }
            int[] LandMIne = { 5, 13, 17, 33, 38, 50, 64, 80, 94 };//地雷●，地雷在地图数组的位置
            for (int i = 0; i < LandMIne.Length; i++)
            {
                MapLenth[LandMIne[i]] = 2;
            }
            int[] Pause = { 9, 27, 60, 93 };//暂停▲，暂停在地图数组的位置
            for (int i = 0; i < Pause.Length; i++)
            {
                MapLenth[Pause[i]] = 3;
            }
            int[] TimeTunnel = { 20, 25, 45, 63, 72, 88, 90 };//时空隧道○，时空隧道在地图数组的位置
            for (int i = 0; i < TimeTunnel.Length; i++)
            {
                MapLenth[TimeTunnel[i]] = 4;
            }
            //for (int i = 0; i < MapLenth.Length; i++)
            //{
            //    if (MapLenth[i] == "1")
            //    {
            //        Console.ForegroundColor = ConsoleColor.Magenta;
            //        _MapLenth[i] = "◎";
            //    }
            //    else if (MapLenth[i] == "2")
            //    {
            //        MapLenth[i] = "☆";
            //    }
            //    else if (MapLenth[i] == "3")
            //    {
            //        MapLenth[i] = "▲";
            //    }
            //    else if (MapLenth[i] == "4")
            //    {
            //        MapLenth[i] = "○";
            //    }
            //    else
            //    {
            //        //Console.ForegroundColor=ConsoleColor.Red;
            //        MapLenth[i] = "□";
            //    }
            //Console.Write(msg);
            //for循环结尾
        }//方法结尾

        #endregion        

        #region(判断位置，绘制地图m0)
        /// <summary>
        /// 判断ab位置，相同情况，地图绘制函数
        /// </summary>
        /// <param name="i"></param>
        public static void M0(int i)
        {
            if (Gameplayer[0] == Gameplayer[1] && Gameplayer[0] == i)
            {
                Console.Write("■");
            }
            else if (Gameplayer[0] == i)
            {
                Console.Write("A");
            }
            else if (Gameplayer[1] == i)
            {
                Console.Write("B");
            }
            else
            {
                switch (MapLenth[i])//把每个编号赋值图案
                {
                    case 0:
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.Write("□");
                        break;
                    case 1:
                        Console.ForegroundColor = ConsoleColor.Red;
                        Console.Write("◎");
                        break;
                    case 2:
                        Console.ForegroundColor = ConsoleColor.Yellow;
                        Console.Write("●");
                        break;
                    case 3:
                        Console.ForegroundColor = ConsoleColor.White;
                        Console.Write("▲");
                        break;
                    case 4:
                        Console.ForegroundColor = ConsoleColor.Cyan;
                        Console.Write("○");
                        break;
                }//switch结尾
            }//else结尾 
        }///函数结尾
        #endregion

        #region（画地图Drawmap）
        /// <summary>
        /// 画地图
        /// </summary>
        static void Drawmap()
        {
            #region
            Console.WriteLine("图例：幸运轮盘:◎    地雷:●    暂停:▲    时空隧道:○");
            for (int i = 0; i < 30; i++)//第一横行
            {
                M0(i);
            }//for循环结尾
            Console.WriteLine();
            for (int i = 30; i < 35; i++)//第一竖行
            {
                for (int j = 0; j < 29; j++)
                {
                    Console.Write(" ");
                }
                M0(i);
                Console.WriteLine();
            }
            for (int i = 64; i > 34; i--)//第二横行
            {
                M0(i);
            }
            Console.WriteLine();
            for (int i = 65; i < 70; i++)//第二竖行
            {
                M0(i);
                Console.WriteLine();
            }
            for (int i = 70; i < 100; i++)//第二横行
            {
                M0(i);
            }//for循环结尾
            Console.WriteLine();//画完最后一行应该换行
            #endregion

        }//方法结尾
        #endregion

        #region(游戏效果PlayGame)
        /// <summary>
        /// 实现踩到轮盘，暂停，炸弹，隧道的效果
        /// </summary>
        public static void PlayGame(int playNumber)
        {
            Random number = new Random();
            int rNumber = number.Next(1, 7);
            Console.WriteLine("玩家{0}按任意键开始掷骰子", player[playNumber]);
            Console.ReadKey(true);//重载，ture就为不显示输入的内容
            Console.WriteLine("{0}掷出了{1}", player[playNumber], rNumber);
            Gameplayer[playNumber] += rNumber;
            Console.ReadKey(true);
            Console.WriteLine("玩家{0}按任意键开始行动", player[playNumber]);
            Console.ReadKey(true);
            Console.WriteLine("玩家{0}行动完了", player[playNumber]);
            Console.ReadKey(true);
            //玩家A有可能踩到玩家B，，方块,幸运轮盘,地雷，暂停，时空隧道
            if (Gameplayer[playNumber] == Gameplayer[1 - playNumber])
            {
                Console.WriteLine("玩家{0}踩到了玩家{1}，玩家{2}退6格", player[playNumber], player[1 - playNumber], player[1 - playNumber]);
                Gameplayer[1 - playNumber] -= 6;
                Console.ReadKey(true);
            }
            else //踩到了道具上
            {
                //M0(Gameplayer[playNumber]);
                switch (MapLenth[Gameplayer[playNumber]])//玩家的坐标1，2，3，4，0
                {
                    case 0:
                        Console.WriteLine("玩家{0}踩到了方块，安全", player[playNumber]);
                        Console.ReadKey(true);
                        break;
                    case 1:
                        Console.WriteLine("玩家{0}踩到了幸运轮盘，请选择 1--交换位置  2--轰炸对方", player[playNumber]);
                        string input = Console.ReadLine();
                        while (true)
                        {
                            if (input == "1")
                            {
                                Console.WriteLine("玩家{0}选择跟玩家{1}交换位置", player[playNumber], player[1 - playNumber]);
                                Console.ReadKey(true);
                                int temp = Gameplayer[playNumber];
                                Gameplayer[playNumber] = Gameplayer[1 - playNumber];
                                Gameplayer[1 - playNumber] = temp;
                                Console.WriteLine("交换完成！！按任意键继续游戏！");
                                Console.ReadKey(true);
                                break;
                            }
                            else if (input == "2")
                            {
                                Console.WriteLine("玩家{0}选择轰炸玩家{1}，玩家{2}退6格", player[playNumber], player[1 - playNumber], player[1 - playNumber]);
                                Console.ReadKey(true);
                                Gameplayer[1 - playNumber] -= 6;
                                Console.WriteLine("玩家{0}退了6格", player[1 - playNumber]);
                                Console.ReadKey(true);
                                break;
                            }
                            else
                            {
                                Console.WriteLine("只能输入1或者2   1--交换位置  2--轰炸对方");
                                input = Console.ReadLine();
                            }
                        }
                        break;
                    case 2:
                        Console.WriteLine("玩家{0}踩到了地雷,退6格", player[playNumber]);
                        Console.ReadKey(true);
                        Gameplayer[playNumber] -= 6;
                        break;
                    case 3:
                        Console.WriteLine("玩家{0}踩到了暂停，暂停一回合", player[playNumber]);
                        Flags[playNumber] = true;
                        break;
                    case 4:
                        Console.WriteLine("玩家{0}踩到了时空隧道，前进10格", player[playNumber]);
                        Gameplayer[playNumber] += 10;
                        break;
                }//switch
            }//else
            if (Gameplayer[0] < 0)
                if (Gameplayer[0] < 0)
                {
                    Gameplayer[0] = 0;
                }
            if (Gameplayer[0] >= 99)
            {
                Gameplayer[0] = 99;
            }
            if (Gameplayer[1] < 0)
            {
                Gameplayer[1] = 0;
            }
            if (Gameplayer[1] >= 99)
            {
                Gameplayer[1] = 99;
            }
            Console.Clear();
            Drawmap();
        }
        #endregion

        #region(判断坐标)
        /// <summary>
        /// 当玩家坐标发生改变的时候要用
        /// </summary>
        ///// <param name="playNumber"></param>
        //public static void ChangePos()
        //{
        //    if (Gameplayer[0] < 0)
        //    {
        //        Gameplayer[0] = 0;
        //    }
        //    if (Gameplayer[0] >= 99)
        //    {
        //        Gameplayer[0] = 99;
        //    }
        //    if (Gameplayer[1] < 0)
        //    {
        //        Gameplayer[1] = 0;
        //    }
        //    if (Gameplayer[1] >= 99)
        //    {
        //        Gameplayer[1] = 99;
        //    }
        //}
        #endregion
    }
}
