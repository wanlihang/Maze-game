//# The-First
//第一个C++工程，于大二上数据结构，迷宫小游戏
#include<stdio.h>
#include<conio.h>
#include<windows.h>
int maze[10][10]= //设置迷宫，最外围1为墙 里边0为可走路径 1为障碍
{    
    {1,1,1,1,1,1,1,1,1,1},
    {1,0,0,0,0,0,0,1,1,1},
    {1,0,1,1,1,1,1,0,0,1},
    {1,0,1,0,0,0,0,0,0,1},
    {1,0,0,0,1,0,1,1,1,1},
    {1,1,1,1,0,0,1,1,1,1},
    {1,0,0,0,0,1,1,1,1,1},
    {1,0,1,1,0,0,1,1,1,1},
    {1,0,0,0,0,0,0,0,0,1},
    {1,1,1,1,1,1,1,1,1,1}
};
int num;
struct
{
    int x,y,d;
}path[100];//x,y分别为垂直和水平方向
 
void solver()
{
    int top=0,x,y,d=-1,find=0;//d为设置方向，上下左右//find为设置是否找得到路
    path[top].x=1;
    path[top].y=1;
    maze[1][1]=-1;
    while(top>-1)
	{
        if(path[top].x==8&&path[top].y==8) 
        {
            printf("迷宫路径如下：\n");
            printf("start->");
            for(x=0;x<=top;x++)
            {
				printf("(%d,%d)-> ",path[x].x,path[x].y);//把找到的路径输出
                num++;
                if(num%8==0)
                    printf("\n");
            } 
            printf("->end!\n");
        }
        while(d<4&&find==0)
		{
            d++;
            switch(d)
			{
            case 0:x=path[top].x-1; y=path[top].y;  break;//方向为上
            case 1:x=path[top].x;   y=path[top].y+1;break;//方向为右
            case 2:x=path[top].x+1; y=path[top].y;  break;//方向为下
            case 3:x=path[top].x;   y=path[top].y-1;      //方向为左
			}
            if(maze[x][y]==0)
                find=1;
        }
         
        if(find==1)//判断是否找得到
		{     
            path[top].d=d;
            top++;
            path[top].x=x;
            path[top].y=y;
            d=-1;find=0;     //重新调整方向
            maze[x][y]=-1;
		}
        else
		{
            maze[path[top].x][path[top].y]=0;
            top--;d=path[top].d; //找不到的话退栈
        }
    }
}

void display()
{
	SetConsoleOutputCP(437);
	for(int i=0;i<10;i++)
	{
		for(int j=0;j<10;j++)
		{
			if(maze[i][j]==1)
				printf("%c",254);
			else
				printf("  ");
		}
	printf("\n");
	}
}

void main()
{
    solver();
	display();
	system("pause");
}
