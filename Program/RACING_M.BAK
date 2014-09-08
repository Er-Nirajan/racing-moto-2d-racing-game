#include<iostream.h>
#include<fstream.h>
#include<stdlib.h>
#include<process.h>
#include<dos.h>
#include<conio.h>
#include<graphics.h>
#include<string.h>
#include<stdio.h>

struct game_result
{
		char name[100];
		long int score;
		int level;
};

void start();          //welcome screen
void main_menu();      //game menu
void game();           //the game
void instruct();       //instructions
void exit_menu();      //exit screen
void high_score();     //high score menu

void instruct()
{
	int gd = DETECT, gm;
	char ch,che;
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	setbkcolor(BLACK);
	setcolor(2);
	settextstyle(10,HORIZ_DIR,4);
	outtextxy(175,0,"Instructions");
	outtextxy(175,10,"__________");
	settextstyle(3,HORIZ_DIR,1);
	outtextxy(0,150,"* The main objective of the game is to avoid the obstacles");
	outtextxy(10,170," that come in your way.");
	outtextxy(0,200,"* The following are the three obstacles that may appear in any");
	outtextxy(10,220," of the three lanes : ");
	outtextxy(0,250,"     Bonus ---->");
	setcolor(WHITE);
	ellipse(200,275,0,360,20,15);
	settextstyle(3,HORIZ_DIR,3);
	outtextxy(195,260,"B");
	setcolor(2);
	settextstyle(3,HORIZ_DIR,1);
	outtextxy(0,320,"    Pit Hole ---->");
	setcolor(WHITE);
	circle(200,350,20);
	setcolor(2);
	outtextxy(0,390,"     Human---->");
	setcolor(WHITE);
	circle(205,5+410,5);
	line(205,10+410,205,25+410);
	line(205,13+410,200,20+410);
	line(205,13+410,210,20+410);
	line(205,25+410,200,30+410);
	line(205,25+410,210,30+410);
	setcolor(2);
	outtextxy(0,450,"Press Any Key To Show More............");
	ch=getch();
	if(ch==0||ch==224)
		che=getch();
	cleardevice();
	setbkcolor(BLACK);
	setcolor(2);
	settextstyle(10,HORIZ_DIR,4);
	outtextxy(175,0,"Instructions");
	outtextxy(175,10,"__________");
	settextstyle(3,HORIZ_DIR,1);
	outtextxy(0,100,"* Avoid 'Pit Holes' and 'Humans'. Your game ends if you fail to do so.");
	outtextxy(0,130,"* Collect 'Bonus'. Each time you collect 'Bonus', your score");
	outtextxy(10,150," increases by 100.");
	outtextxy(0,180,"* Change lanes by using left and right arrow keys.");
	outtextxy(0,210,"* After each level, the obstacles move faster towards you.");
	outtextxy(0,240,"* Initially, your control on the Bike is fairly difficult");
	outtextxy(10,260," (i.e. while shifting lanes). But as the game level increases, your");
	outtextxy(10,280," control on the bike tends to become better.");
	outtextxy(0,310,"* As the game level increases, your ability to shift the bike between ");
	outtextxy(10,330," the extreme lanes becomes harder.");
	outtextxy(0,360,"* Watch out for more instructions towards the left side of your screen ");
	outtextxy(10,380," while playing");
	outtextxy(0,455," Press Any Key To Return To The Previous Menu.............");
	ch=getch();
	if(ch==0||ch==224)
		che=getch();
	closegraph();
	main_menu();
}

void high_score()
{
	int gd = DETECT, gm;
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	game_result g3;
	ifstream ifile;
	char ch,che;
	ifile.open("High_Score.txt");
	while(!ifile.eof())
		ifile.read((char *)&g3,sizeof(g3));
	ifile.close();
	setbkcolor(4);
	settextstyle(10,HORIZ_DIR,5);
	outtextxy(125,20,"HIGH SCORE");
	outtextxy(125,30,"__________");
	settextstyle(3,HORIZ_DIR,3);
	outtextxy(200,215,"Name = ");
	gotoxy(40,15);
	cout<<g3.name;
	outtextxy(200,265,"Score = ");
	gotoxy(40,18);
	cout<<g3.score;
	outtextxy(110,325,"Levels Passed = ");
	gotoxy(40,22);
	cout<<g3.level-1;
	settextstyle(3,HORIZ_DIR,1);
	outtextxy(10,440,"Press Any Key To Return To The Previous Menu......");
	ch=getch();
	if(ch==0||ch==224)
		che=getch();
	closegraph();
	main_menu();
}

void game()
{
	int gd = DETECT, gm;
	char ch,che;
	game_result g1,g2,g3;
	char name[100];
	int already_choosen[12]={0};
	int pos[12]={0};
	int level,choose_ob,choose_lane,x,y;
	int i=0;
	int flag=0;
	int lane[20]={1,3,2,3,2,1,1,2,3,2,3,2,3,3,1,1,2,3,1,2};                     //1-bonus 2-pit 3-human
	int ob[35]={0,1,2,2,3,4,3,4,4,2,3,2,1,1,4,3,3,2,4,3,3,1,1,2,4,2,1,3,1,3,2,1,3,4,3};   //4-bonus,pit
	level=1;
	choose_ob=1;
	long int score;
	int no_of_iterations=0;
	score=0;
	int speed=0;
	randomize();
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	settextstyle(3,HORIZ_DIR,3);
	outtextxy(100,198,"Enter Your Name = ");
	gotoxy(43,14);
	gets(name);
	strcpy(g1.name,name);
	outtextxy(50,400,"Press Any Key To Continue......");
	getch();
	cleardevice();
	setcolor(BLUE);                   //track
	setlinestyle(0,0,3);
	line(244,0,244,450);
	line(247,0,247,450);
	line(250,0,250,450);
	line(600,0,600,450);
	line(603,0,603,450);
	line(606,0,606,450);
	setcolor(WHITE);
	setlinestyle(0,0,1);
	line(250+116,0,250+116,450);
	line(250+116+117,0,250+116+117,450);
	while(1)
	{
	if(level>15)                                           // to choose obstacle and lane
	{
		if(no_of_iterations%4==0 && no_of_iterations!=0)
		{
			choose_ob=(rand()%34);
			choose_lane=(rand()%19);
		}
		else
		{
			choose_ob=0;
			choose_lane=1;
		}
	}
	else
	{
		if(no_of_iterations%3==0 && no_of_iterations!=0)
		{
			choose_ob=(rand()%34);
			choose_lane=(rand()%19);
		}
		else
		{
			choose_ob=0;
			choose_lane=1;
		}
	}
	if(i==0)                                           //initial position of the bike
	{
		fillellipse(310+120,447,7,10);
		rectangle(305+120,458,315+120,477);
		rectangle(295+120,434,325+120,437);
		rectangle(306+120,417,313+120,433);
		moveto(200,100);
		i++;
	}
	while(kbhit())                                   //movement of bike
	{
		ch=getch();
		if(ch==0||ch==224)
		{
			che=getch();
			x=getx();
			y=gety();
			if(che==75 && x==200)     //left & 2nd position
			{
				moveto(100,100);
				for(x=295+120;x<=325+120;x++)               //2nd position
				{
					for(y=417;y<=477;y++)
						putpixel(x,y,BLACK);
				}
				setfillstyle(9,7);
				fillellipse(310,447,7,10);
				rectangle(305,458,315,477);
				rectangle(295,434,325,437);
				rectangle(306,417,313,433);
			}
			else if(che==75 && x==100)   //left and 1st position
				;
			else if(che==75 && x==300)   //left and 3rd position
			{
				moveto(200,100);
				for(x=295+120+121;x<=325+120+121;x++)     //3rd position
				{
					for(y=417;y<=477;y++)
						putpixel(x,y,BLACK);
				}
				setfillstyle(9,7);
				fillellipse(310+120,447,7,10);
				rectangle(305+120,458,315+120,477);
				rectangle(295+120,434,325+120,437);
				rectangle(306+120,417,313+120,433);
			}
			else if(che==77 && x==100)   //right and 1st position
			{
				moveto(200,100);
				for(x=295;x<=325;x++)                         //1st position
				{
					for(y=417;y<=477;y++)
						putpixel(x,y,BLACK);
				}
				setfillstyle(9,7);
				fillellipse(310+120,447,7,10);
				rectangle(305+120,458,315+120,477);
				rectangle(295+120,434,325+120,437);
				rectangle(306+120,417,313+120,433);
			}
			else if(che==77 && x==200)    //right and 2nd position
			{
				moveto(300,100);
				for(x=295+120;x<=325+120;x++)               //2nd position
				{
					for(y=417;y<=477;y++)
						putpixel(x,y,BLACK);
				}
				setfillstyle(9,7);
				fillellipse(310+241,447,7,10);
				rectangle(305+241,458,315+241,477);
				rectangle(295+241,434,325+241,437);
				rectangle(306+241,417,313+241,433);
			}
			else if(che==77 && x==300)
				;
			else
				;
		}
		else
			;
	}
	if((ob[choose_ob]==1 && lane[choose_lane]==1) || (already_choosen[0]==1))           //bonus+lane 1
	{
		if((ob[choose_ob]==1 && lane[choose_lane]==1) && !(already_choosen[0]==1))
		{
			ellipse(300,15,0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295,0,"B");
			already_choosen[0]=1;
		}
		if(!(ob[choose_ob]==1 && lane[choose_lane]==1) && (already_choosen[0]==1))
		{
			for(int q=280;q<=320;q++)
			{
				for(int w=0+pos[0];w<=30+pos[0];w++)
					putpixel(q,w,BLACK);
			}
			pos[0]+=30;
			ellipse(300,15+pos[0],0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295,0+pos[0],"B");
		}
		if((ob[choose_ob]==1 && lane[choose_lane]==1) && (already_choosen[0]==1))
		{
			if(pos[0]>360)
			{
				for(int q=280;q<=320;q++)
				{
					for(int w=0+pos[0];w<=30+pos[0];w++)
						putpixel(q,w,BLACK);
				}
				pos[0]=0;
				ellipse(300,15,0,360,20,15);
				settextstyle(3,HORIZ_DIR,3);
				outtextxy(295,0,"B");
			}
			else
				;
		}
		if(pos[0]>360)
		{
			for(int q=280;q<=320;q++)
			{
				for(int w=0+pos[0];w<=30+pos[0];w++)
					putpixel(q,w,BLACK);
			}
			pos[0]=0;
			already_choosen[0]=0;
		}
	}
	if((ob[choose_ob]==1 && lane[choose_lane]==2) || (already_choosen[1]==1))           //bonus+lane 2
	{
		if((ob[choose_ob]==1 && lane[choose_lane]==2) && !(already_choosen[1]==1))
		{
			ellipse(300+120,15,0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295+120,0,"B");
			already_choosen[1]=1;
		}
		if(!(ob[choose_ob]==1 && lane[choose_lane]==2) && (already_choosen[1]==1))
		{
			for(int q=280+120;q<=320+120;q++)
			{
				for(int w=0+pos[1];w<=30+pos[1];w++)
					putpixel(q,w,BLACK);
			}
			pos[1]+=30;
			ellipse(300+120,15+pos[1],0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295+120,0+pos[1],"B");
		}
		if((ob[choose_ob]==1 && lane[choose_lane]==2) && (already_choosen[1]==1))
		{
			if(pos[1]>360)
			{
				for(int q=280+120;q<=320+120;q++)
				{
					for(int w=0+pos[1];w<=30+pos[1];w++)
						putpixel(q,w,BLACK);
				}
				pos[1]=0;
				ellipse(300+120,15,0,360,20,15);
				settextstyle(3,HORIZ_DIR,3);
				outtextxy(295+120,0,"B");
			}
			else
				;
		}
		if(pos[1]>360)
		{
			for(int q=280+120;q<=320+120;q++)
			{
				for(int w=0+pos[1];w<=30+pos[1];w++)
					putpixel(q,w,BLACK);
			}
			pos[1]=0;
			already_choosen[1]=0;
		}
	}
	if((ob[choose_ob]==1 && lane[choose_lane]==3) || (already_choosen[2]==1))            //bonus+lane 3
	{
		if((ob[choose_ob]==1 && lane[choose_lane]==3) && !(already_choosen[2]==1))
		{
			ellipse(300+120+121,15,0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295+120+121,0,"B");
			already_choosen[2]=1;
		}
		if(!(ob[choose_ob]==1 && lane[choose_lane]==3) && (already_choosen[2]==1))
		{
			for(int q=280+120+121;q<=320+120+121;q++)
			{
				for(int w=0+pos[2];w<=30+pos[2];w++)
					putpixel(q,w,BLACK);
			}
			pos[2]+=30;
			ellipse(300+120+121,15+pos[2],0,360,20,15);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(295+120+121,0+pos[2],"B");
		}
		if((ob[choose_ob]==1 && lane[choose_lane]==3) && (already_choosen[2]==1))
		{
			if(pos[2]>360)
			{
				for(int q=280+120+121;q<=320+120+121;q++)
				{
					for(int w=0+pos[2];w<=30+pos[2];w++)
						putpixel(q,w,BLACK);
				}
				pos[2]=0;
				ellipse(300+120+121,15,0,360,20,15);
				settextstyle(3,HORIZ_DIR,3);
				outtextxy(295+120+121,0,"B");
			}
			else
				;
		}
		if(pos[2]>360)
		{
			for(int q=280+120+121;q<=320+120+121;q++)
			{
				for(int w=0+pos[2];w<=30+pos[2];w++)
					putpixel(q,w,BLACK);
			}
			pos[2]=0;
			already_choosen[2]=0;
		}
	}
	if((ob[choose_ob]==2 && lane[choose_lane]==1) || (already_choosen[3]==1))          //pit+lane 1
	{
		if((ob[choose_ob]==2 && lane[choose_lane]==1) && !(already_choosen[3]==1))
		{
			circle(305,20,20);
			already_choosen[3]=1;
		}
		if(!(ob[choose_ob]==2 && lane[choose_lane]==1) && (already_choosen[3]==1))
		{
			for(int q=285;q<=325;q++)
			{
				for(int w=0+pos[3];w<=40+pos[3];w++)
					putpixel(q,w,BLACK);
			}
			pos[3]+=30;
			circle(305,20+pos[3],20);
		}
		if((ob[choose_ob]==2 && lane[choose_lane]==1) && (already_choosen[3]==1))
		{
			if(pos[3]>390)
			{
				for(int q=285;q<=325;q++)
				{
					for(int w=0+pos[3];w<=40+pos[3];w++)
						putpixel(q,w,BLACK);
				}
				pos[3]=0;
				circle(305,20,20);
			}
			else
				;
		}
		if(pos[3]>390)
		{
			for(int q=285;q<=325;q++)
			{
				for(int w=0+pos[3];w<=40+pos[3];w++)
					putpixel(q,w,BLACK);
			}
			pos[3]=0;
			already_choosen[3]=0;
		}
	}
	if((ob[choose_ob]==2 && lane[choose_lane]==2) || (already_choosen[4]==1))               //pit+lane 2
	{
		if((ob[choose_ob]==2 && lane[choose_lane]==2) && !(already_choosen[4]==1))
		{
			circle(305+120,20,20);
			already_choosen[4]=1;
		}
		if(!(ob[choose_ob]==2 && lane[choose_lane]==2) && (already_choosen[4]==1))
		{
			for(int q=285+120;q<=325+120;q++)
			{
				for(int w=0+pos[4];w<=40+pos[4];w++)
					putpixel(q,w,BLACK);
			}
			pos[4]+=30;
			circle(305+120,20+pos[4],20);
		}
		if((ob[choose_ob]==2 && lane[choose_lane]==2) && (already_choosen[4]==1))
		{
			if(pos[4]>390)
			{
				for(int q=285+120;q<=325+120;q++)
				{
					for(int w=0+pos[4];w<=40+pos[4];w++)
						putpixel(q,w,BLACK);
				}
				pos[4]=0;
				circle(305+120,20,20);
			}
			else
				;
		}
		if(pos[4]>390)
		{
			for(int q=285+120;q<=325+120;q++)
			{
				for(int w=0+pos[4];w<=40+pos[4];w++)
					putpixel(q,w,BLACK);
			}
			pos[4]=0;
			already_choosen[4]=0;
		}
	}
	if((ob[choose_ob]==2 && lane[choose_lane]==3) || (already_choosen[5]==1))             // pit+lane 3
	{
		if((ob[choose_ob]==2 && lane[choose_lane]==3) && !(already_choosen[5]==1))
		{
			circle(305+120+121,20,20);
			already_choosen[5]=1;
		}
		if(!(ob[choose_ob]==2 && lane[choose_lane]==3) && (already_choosen[5]==1))
		{
			for(int q=285+120+121;q<=325+120+121;q++)
			{
				for(int w=0+pos[5];w<=40+pos[5];w++)
					putpixel(q,w,BLACK);
			}
			pos[5]+=30;
			circle(305+120+121,20+pos[5],20);
		}
		if((ob[choose_ob]==2 && lane[choose_lane]==3) && (already_choosen[5]==1))
		{
			if(pos[5]>390)
			{
				for(int q=285+120+121;q<=325+120+121;q++)
				{
					for(int w=0+pos[5];w<=40+pos[5];w++)
						putpixel(q,w,BLACK);
				}
				pos[5]=0;
				circle(305+120+121,20,20);
			}
			else
				;
		}
		if(pos[5]>390)
		{
			for(int q=285+120+121;q<=325+120+121;q++)
			{
				for(int w=0+pos[5];w<=40+pos[5];w++)
					putpixel(q,w,BLACK);
			}
			pos[5]=0;
			already_choosen[5]=0;
		}
	}
	if((ob[choose_ob]==3 && lane[choose_lane]==1) || (already_choosen[6]==1))           //human+lane 1
	{
		if((ob[choose_ob]==3 && lane[choose_lane]==1) && !(already_choosen[6]==1))
		{
			circle(305,5,5);
			line(305,10,305,25);
			line(305,13,300,20);
			line(305,13,310,20);
			line(305,25,300,30);
			line(305,25,310,30);
			already_choosen[6]=1;
		}
		if(!(ob[choose_ob]==3 && lane[choose_lane]==1) && (already_choosen[6]==1))
		{
			for(int q=300;q<=310;q++)
			{
				for(int w=0+pos[6];w<=30+pos[6];w++)
					putpixel(q,w,BLACK);
			}
			pos[6]+=30;
			circle(305,5+pos[6],5);
			line(305,10+pos[6],305,25+pos[6]);
			line(305,13+pos[6],300,20+pos[6]);
			line(305,13+pos[6],310,20+pos[6]);
			line(305,25+pos[6],300,30+pos[6]);
			line(305,25+pos[6],310,30+pos[6]);
		}
		if((ob[choose_ob]==3 && lane[choose_lane]==1) && (already_choosen[6]==1))
		{
			if(pos[6]>390)
			{
				for(int q=300;q<=310;q++)
				{
					for(int w=0+pos[6];w<=30+pos[6];w++)
						putpixel(q,w,BLACK);
				}
				pos[6]=0;
				circle(305,5,5);
				line(305,10,305,25);
				line(305,13,300,20);
				line(305,13,310,20);
				line(305,25,300,30);
				line(305,25,310,30);
			}
			else
				;
		}
		if(pos[6]>390)
		{
			for(int q=300;q<=310;q++)
			{
				for(int w=0+pos[6];w<=30+pos[6];w++)
					putpixel(q,w,BLACK);
			}
			pos[6]=0;
			already_choosen[6]=0;
		}
	}
	if((ob[choose_ob]==3 && lane[choose_lane]==2) || (already_choosen[7]==1))                 //human+lane 2
	{
		if((ob[choose_ob]==3 && lane[choose_lane]==2) && !(already_choosen[7]==1))
		{
			circle(305+120,5,5);
			line(305+120,10,305+120,25);
			line(305+120,13,300+120,20);
			line(305+120,13,310+120,20);
			line(305+120,25,300+120,30);
			line(305+120,25,310+120,30);
			already_choosen[7]=1;
		}
		if(!(ob[choose_ob]==3 && lane[choose_lane]==2) && (already_choosen[7]==1))
		{
			for(int q=300+120;q<=310+120;q++)
			{
				for(int w=0+pos[7];w<=30+pos[7];w++)
					putpixel(q,w,BLACK);
			}
			pos[7]+=30;
			circle(305+120,5+pos[7],5);
			line(305+120,10+pos[7],305+120,25+pos[7]);
			line(305+120,13+pos[7],300+120,20+pos[7]);
			line(305+120,13+pos[7],310+120,20+pos[7]);
			line(305+120,25+pos[7],300+120,30+pos[7]);
			line(305+120,25+pos[7],310+120,30+pos[7]);
		}
		if((ob[choose_ob]==3 && lane[choose_lane]==2) && (already_choosen[7]==1))
		{
			if(pos[7]>390)
			{
				for(int q=300+120;q<=310+120;q++)
				{
					for(int w=0+pos[7];w<=30+pos[7];w++)
						putpixel(q,w,BLACK);
				}
				pos[7]=0;
				circle(305+120,5,5+120);
				line(305+120,10,305,25+120);
				line(305+120,13,300,20+120);
				line(305+120,13,310,20+120);
				line(305+120,25,300,30+120);
				line(305+120,25,310,30+120);
			}
			else
				;
		}
		if(pos[7]>390)
		{
			for(int q=300+120;q<=310+120;q++)
			{
				for(int w=0+pos[7];w<=30+pos[7];w++)
					putpixel(q,w,BLACK);
			}
			pos[7]=0;
			already_choosen[7]=0;
		}
	}
	if((ob[choose_ob]==3 && lane[choose_lane]==3) || (already_choosen[8]==1))            //human+lane 3
	{
		if((ob[choose_ob]==3 && lane[choose_lane]==3) && !(already_choosen[8]==1))
		{
			circle(305+120+121,5,5);
			line(305+120+121,10,305+120+121,25);
			line(305+120+121,13,300+120+121,20);
			line(305+120+121,13,310+120+121,20);
			line(305+120+121,25,300+120+121,30);
			line(305+120+121,25,310+120+121,30);
			already_choosen[8]=1;
		}
		if(!(ob[choose_ob]==3 && lane[choose_lane]==3) && (already_choosen[8]==1))
		{
			for(int q=300+120+121;q<=310+120+121;q++)
			{
				for(int w=0+pos[8];w<=30+pos[8];w++)
					putpixel(q,w,BLACK);
			}
			pos[8]+=30;
			circle(305+120+121,5+pos[8],5);
			line(305+120+121,10+pos[8],305+120+121,25+pos[8]);
			line(305+120+121,13+pos[8],300+120+121,20+pos[8]);
			line(305+120+121,13+pos[8],310+120+121,20+pos[8]);
			line(305+120+121,25+pos[8],300+120+121,30+pos[8]);
			line(305+120+121,25+pos[8],310+120+121,30+pos[8]);
		}
		if((ob[choose_ob]==3 && lane[choose_lane]==3) && (already_choosen[8]==1))
		{
			if(pos[8]>390)
			{
				for(int q=300+120+121;q<=310+120+121;q++)
				{
					for(int w=0+pos[8];w<=30+pos[8];w++)
						putpixel(q,w,BLACK);
				}
				pos[8]=0;
				circle(305+120+121,5,5+120+121);
				line(305+120+121,10,305,25+120+121);
				line(305+120+121,13,300,20+120+121);
				line(305+120+121,13,310,20+120+121);
				line(305+120+121,25,300,30+120+121);
				line(305+120+121,25,310,30+120+121);
			}
			else
				;
		}
		if(pos[8]>390)
		{
			for(int q=300+120+121;q<=310+120+121;q++)
			{
				for(int w=0+pos[8];w<=30+pos[8];w++)
					putpixel(q,w,BLACK);
			}
			pos[8]=0;
			already_choosen[8]=0;
		}
	}
	if((ob[choose_ob]==4 && lane[choose_lane]==1) || (already_choosen[9]==1))            //pit+human+lane 1
	{
		if((ob[choose_ob]==4 && lane[choose_lane]==1) && !(already_choosen[9]==1))
		{
			circle(305,20,20);
			circle(305+120,5,5);
			line(305+120,10,305+120,25);
			line(305+120,13,300+120,20);
			line(305+120,13,310+120,20);
			line(305+120,25,300+120,30);
			line(305+120,25,310+120,30);
			already_choosen[9]=1;
		}
		if(!(ob[choose_ob]==4 && lane[choose_lane]==1) && (already_choosen[9]==1))
		{
			for(int q=285;q<=325;q++)
			{
				for(int w=0+pos[9];w<=40+pos[9];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300+120;e<=310+120;e++)
			{
				for(int r=0+pos[9];r<=30+pos[9];r++)
					putpixel(e,r,BLACK);
			}
			pos[9]+=30;
			circle(305,20+pos[9],20);
			circle(305+120,5+pos[9],5);
			line(305+120,10+pos[9],305+120,25+pos[9]);
			line(305+120,13+pos[9],300+120,20+pos[9]);
			line(305+120,13+pos[9],310+120,20+pos[9]);
			line(305+120,25+pos[9],300+120,30+pos[9]);
			line(305+120,25+pos[9],310+120,30+pos[9]);
		}
		if((ob[choose_ob]==4 && lane[choose_lane]==1) && (already_choosen[9]==1))
		{
			if(pos[9]>390)
			{
				for(int q=285;q<=325;q++)
				{
					for(int w=0+pos[9];w<=40+pos[9];w++)
						putpixel(q,w,BLACK);
				}
				for(int e=300+120;e<=310+120;e++)
				{
					for(int r=0+pos[9];r<=30+pos[9];r++)
						putpixel(e,r,BLACK);
				}
				pos[9]=0;
				circle(305,20,20);
				circle(305+120,5,5);
				line(305+120,10,305+120,25);
				line(305+120,13,300+120,20);
				line(305+120,13,310+120,20);
				line(305+120,25,300+120,30);
				line(305+120,25,310+120,30);
			}
			else
				;
		}
		if(pos[9]>390)
		{
			for(int q=285;q<=325;q++)
			{
				for(int w=0+pos[9];w<=40+pos[9];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300+120;e<=310+120;e++)
			{
				for(int r=0+pos[9];r<=30+pos[9];r++)
					putpixel(e,r,BLACK);
			}
			pos[9]=0;
			already_choosen[9]=0;
		}
	}
	if((ob[choose_ob]==4 && lane[choose_lane]==2) || (already_choosen[10]==1))            //pit+human+lane 2
	{
		if((ob[choose_ob]==4 && lane[choose_lane]==2) && !(already_choosen[10]==1))
		{
			circle(305+120,20,20);
			circle(305+241,5,5);
			line(305+241,10,305+241,25);
			line(305+241,13,300+241,20);
			line(305+241,13,310+241,20);
			line(305+241,25,300+241,30);
			line(305+241,25,310+241,30);
			already_choosen[10]=1;
		}
		if(!(ob[choose_ob]==4 && lane[choose_lane]==2) && (already_choosen[10]==1))
		{
			for(int q=285+120;q<=325+120;q++)
			{
				for(int w=0+pos[10];w<=40+pos[10];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300+120+121;e<=310+120+121;e++)
			{
				for(int r=0+pos[10];r<=30+pos[10];r++)
					putpixel(e,r,BLACK);
			}
			pos[10]+=30;
			circle(305+120,20+pos[10],20);
			circle(305+120+121,5+pos[10],5);
			line(305+120+121,10+pos[10],305+120+121,25+pos[10]);
			line(305+120+121,13+pos[10],300+120+121,20+pos[10]);
			line(305+120+121,13+pos[10],310+120+121,20+pos[10]);
			line(305+120+121,25+pos[10],300+120+121,30+pos[10]);
			line(305+120+121,25+pos[10],310+120+121,30+pos[10]);
		}
		if((ob[choose_ob]==4 && lane[choose_lane]==2) && (already_choosen[10]==1))
		{
			if(pos[10]>390)
			{
				for(int q=285+120;q<=325+120;q++)
				{
					for(int w=0+pos[10];w<=40+pos[10];w++)
						putpixel(q,w,BLACK);
				}
				for(int e=300+120+121;e<=310+120+121;e++)
				{
					for(int r=0+pos[10];r<=30+pos[10];r++)
						putpixel(e,r,BLACK);
				}
				pos[10]=0;
				circle(305+120,20,20);
				circle(305+120+121,5,5);
				line(305+120+121,10,305+120+121,25);
				line(305+120+121,13,300+120+121,20);
				line(305+120+121,13,310+120+121,20);
				line(305+120+121,25,300+120+121,30);
				line(305+120+121,25,310+120+121,30);
			}
			else
				;
		}
		if(pos[10]>390)
		{
			for(int q=285+120;q<=325+120;q++)
			{
				for(int w=0+pos[10];w<=40+pos[10];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300+120+121;e<=310+120+121;e++)
			{
				for(int r=0+pos[10];r<=30+pos[10];r++)
					putpixel(e,r,BLACK);
			}
			pos[10]=0;
			already_choosen[10]=0;
		}
	}
	if((ob[choose_ob]==4 && lane[choose_lane]==3) || (already_choosen[11]==1))            //pit+human+lane 3
	{
		if((ob[choose_ob]==4 && lane[choose_lane]==3) && !(already_choosen[11]==1))
		{
			circle(305+121+120,20,20);
			circle(305,5,5);
			line(305,10,305,25);
			line(305,13,300,20);
			line(305,13,310,20);
			line(305,25,300,30);
			line(305,25,310,30);
			already_choosen[11]=1;
		}
		if(!(ob[choose_ob]==4 && lane[choose_lane]==3) && (already_choosen[11]==1))
		{
			for(int q=285+120+121;q<=325+120+121;q++)
			{
				for(int w=0+pos[11];w<=40+pos[11];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300;e<=310;e++)
			{
				for(int r=0+pos[11];r<=30+pos[11];r++)
					putpixel(e,r,BLACK);
			}
			pos[11]+=30;
			circle(305+121+120,20+pos[11],20);
			circle(305,5+pos[11],5);
			line(305,10+pos[11],305,25+pos[11]);
			line(305,13+pos[11],300,20+pos[11]);
			line(305,13+pos[11],310,20+pos[11]);
			line(305,25+pos[11],300,30+pos[11]);
			line(305,25+pos[11],310,30+pos[11]);
		}
		if((ob[choose_ob]==4 && lane[choose_lane]==3) && (already_choosen[11]==1))
		{
			if(pos[11]>390)
			{
				for(int q=285+120+121;q<=325+120+121;q++)
				{
					for(int w=0+pos[11];w<=40+pos[11];w++)
						putpixel(q,w,BLACK);
				}
				for(int e=300;e<=310;e++)
				{
					for(int r=0+pos[11];r<=30+pos[11];r++)
						putpixel(e,r,BLACK);
				}
				pos[11]=0;
				circle(305+121+120,20,20);
				circle(305,5,5);
				line(305,10,305,25);
				line(305,13,300,20);
				line(305,13,310,20);
				line(305,25,300,30);
				line(305,25,310,30);
			}
			else
				;
		}
		if(pos[11]>390)
		{
			for(int q=285+120+121;q<=325+120+121;q++)
			{
				for(int w=0+pos[11];w<=40+pos[11];w++)
					putpixel(q,w,BLACK);
			}
			for(int e=300;e<=310;e++)
			{
				for(int r=0+pos[11];r<=30+pos[11];r++)
					putpixel(e,r,BLACK);
			}
			pos[11]=0;
			already_choosen[11]=0;
		}
	}
	for(int y=0;y<=11;y++)                                     //check if game is over
	{
		if(already_choosen[y]==1)
		{
			if(y==0||y==1||y==2)
			{
				if(getx()==100 && y==0 && pos[0]==360)
				{
					gotoxy(2,16);
					printf("BONUS !!!");
					gotoxy(2,17);
					printf("+100");
					delay(500);
					score+=100;
					gotoxy(2,16);
					printf("         ");
					gotoxy(2,17);
					printf("    ");
				}
				if(getx()==200 && y==1 && pos[1]==360)
				{
					gotoxy(2,16);
					printf("BONUS !!!");
					gotoxy(2,17);
					printf("+100");
					delay(500);
					score+=100;
					gotoxy(2,16);
					printf("         ");
					gotoxy(2,17);
					printf("    ");
				}
				if(getx()==300 && y==2 && pos[2]==360)
				{
					gotoxy(2,16);
					printf("BONUS !!!");
					gotoxy(2,17);
					printf("+100");
					delay(500);
					score+=100;
					gotoxy(2,16);
					printf("         ");
					gotoxy(2,17);
					printf("    ");
				}
			}
			if(y==3||y==4||y==5)
			{
				if(y==3 && getx()==100 && pos[3]==390)
				{
					gotoxy(2,16);
					printf("You Fell Into The Pit :p ");
					gotoxy(2,17);
					printf("HA HA HA HA HA :D :D :D");
					flag=1;
					break;
				}
				if(y==4 && getx()==200 && pos[4]==390)
				{
					gotoxy(2,16);
					printf("You Fell Into The Pit :p ");
					gotoxy(2,17);
					printf("HA HA HA HA HA :D :D :D");
					flag=1;
					break;
				}
				if(y==5 && getx()==300 && pos[5]==390)
				{
					gotoxy(2,16);
					printf("You Fell Into The Pit :p ");
					gotoxy(2,17);
					printf("HA HA HA HA HA :D :D :D");
					flag=1;
					break;
				}
			}
			if(y==6||y==7||y==8)
			{
				if(y==6 && getx()==100 && pos[6]==390)
				{
					gotoxy(2,16);
					printf("You Just Killed Someone !!!");
					gotoxy(2,17);
					printf("NOT COOL !!!");
					flag=1;
					break;
				}
				if(y==7 && getx()==200 && pos[7]==390)
				{
					gotoxy(2,16);
					printf("You Just Killed Someone !!!");
					gotoxy(2,17);
					printf("NOT COOL !!!");
					flag=1;
					break;
				}
				if(y==8 && getx()==300 && pos[8]==390)
				{
					gotoxy(2,16);
					printf("You Just Killed Someone !!!");
					gotoxy(2,17);
					printf("NOT COOL !!!");
					flag=1;
					break;
				}
			}
			if(y==9||y==10||y==11)
			{
				if(y==9 && pos[9]==390 && (getx()==100||getx()==200))
				{
					gotoxy(2,16);
					printf("Are You Sure You Know How");
					gotoxy(2,17);
					printf("Ride A Bike ???");
					flag=1;
					break;
				}
				if(y==10 && pos[10]==390 && (getx()==200||getx()==300))
				{
					gotoxy(2,16);
					printf("Are You Sure You Know How");
					gotoxy(2,17);
					printf("Ride A Bike ???");
					flag=1;
					break;
				}
				if(y==11 && pos[11]==390 && (getx()==100||getx()==300))
				{
					gotoxy(2,16);
					printf("Are You Sure You Know How");
					gotoxy(2,17);
					printf("Ride A Bike ???");
					flag=1;
					break;
				}
			}
		}
	}
	gotoxy(4,3);                                      //score and level info
	printf("Welcome %s !!!",name);
	settextstyle(3,HORIZ_DIR,3);
	outtextxy(30,375,"Level = ");
	gotoxy(17,25);
	printf("%d",level);
	outtextxy(20,355,"Score = ");
	gotoxy(17,24);
	printf("%ld",score);
	score+=10;
	no_of_iterations++;
	if(no_of_iterations==80 || no_of_iterations==110 || no_of_iterations==140 || no_of_iterations==170)         //levels
	{
		if(no_of_iterations==80 && level<=5)
		{
			gotoxy(1,5);
			printf("You Just Cleared Level %d !!!",level);
			level++;
			gotoxy(1,6);
			printf("Keep Racing !!!");
			gotoxy(1,13);
			printf("Press Any Key To Continue.....");
			gotoxy(1,10);
			printf("The Obstacles Will Now");
			gotoxy(1,11);
			printf("Move Faster !!!");
			ch=getch();
			if(ch==0||ch==224)
				che=getch();
			gotoxy(1,5);
			printf("                             ");
			gotoxy(1,6);
			printf("               ");
			gotoxy(1,13);
			printf("                              ");
			gotoxy(1,10);
			printf("                      ");
			gotoxy(1,11);
			printf("               ");
			no_of_iterations=0;
			speed+=50;
		}
		if(no_of_iterations==110 && level<=13 && level>5)
		{
			gotoxy(1,5);
			printf("You Just Cleared Level %d !!!",level);
			level++;
			gotoxy(1,6);
			printf("Keep Racing !!!");
			gotoxy(1,13);
			printf("Press Any Key To Continue.....");
			gotoxy(1,10);
			printf("The Obstacles Will Now");
			gotoxy(1,11);
			printf("Move Faster !!!");
			ch=getch();
			if(ch==0||ch==224)
				che=getch();
			gotoxy(1,5);
			printf("                             ");
			gotoxy(1,6);
			printf("               ");
			gotoxy(1,13);
			printf("                              ");
			gotoxy(1,10);
			printf("                      ");
			gotoxy(1,11);
			printf("               ");
			no_of_iterations=0;
			speed+=25;
		}
		if(no_of_iterations==140 && level<=21 && level>13)
		{
			gotoxy(1,5);
			printf("You Just Cleared Level %d !!!",level);
			level++;
			gotoxy(1,6);
			printf("Keep Racing !!!");
			gotoxy(1,13);
			printf("Press Any Key To Continue.....");
			gotoxy(1,10);
			printf("The Obstacles Will Now");
			gotoxy(1,11);
			printf("Move Faster !!!");
			ch=getch();
			if(ch==0||ch==224)
				che=getch();
			gotoxy(1,5);
			printf("                             ");
			gotoxy(1,6);
			printf("               ");
			gotoxy(1,13);
			printf("                              ");
			gotoxy(1,10);
			printf("                      ");
			gotoxy(1,11);
			printf("               ");
			no_of_iterations=0;
			speed+=25;
		}
		if(no_of_iterations==170 && level>21)
		{
			gotoxy(1,5);
			printf("You Just Cleared Level %d !!!",level);
			level++;
			gotoxy(1,6);
			printf("Keep Racing !!!");
			gotoxy(1,13);
			printf("Press Any Key To Continue.....");
			gotoxy(1,10);
			printf("The Obstacles Will Now");
			gotoxy(1,11);
			printf("Move Faster !!!");
			ch=getch();
			if(ch==0||ch==224)
				che=getch();
			gotoxy(1,5);
			printf("                             ");
			gotoxy(1,6);
			printf("               ");
			gotoxy(1,13);
			printf("                              ");
			gotoxy(1,10);
			printf("                      ");
			gotoxy(1,11);
			printf("               ");
			no_of_iterations=0;
			speed+=10;
		}
	}
	if(flag==1)                                    //game over
	{
		gotoxy(2,19);
		printf("GAME OVER !!!");
		gotoxy(2,20);
		printf("Press Any Key To Continue...");
		ch=getch();
		if(ch==0||ch==224)
			che=getch();
		break;
	}
	delay(700-speed);
	}
	g1.score=score;                           //storing info into a file
	g1.level=level-1;
	ifstream ifile;
	ofstream ofile;
	ifile.open("High_Score.txt");
	ifile.read((char *)&g2,sizeof(g2));
	ifile.close();
	if(g2.score<g1.score)
	{
		ofile.open("High_Score.txt");
		ofile.write((char *)&g1,sizeof(g1));
		ofile.close();
	}
	cleardevice();
	settextstyle(3,HORIZ_DIR,6);                   //game statistics
	outtextxy(150,20,"Game Stats");
	outtextxy(150,30,"________");
	settextstyle(3,HORIZ_DIR,4);
	outtextxy(230,160,"Name = ");
	gotoxy(50,12);
	printf("%s",name);
	outtextxy(145,210,"Final Score = ");
	gotoxy(50,15);
	printf("%ld",score);
	outtextxy(100,260,"Levels Passed = ");
	gotoxy(50,18);
	printf("%d",level-1);
	settextstyle(3,HORIZ_DIR,2);
	outtextxy(20,450,"Press Any Key To Continue........");
	char f,g;
	f=getch();
	if(f==0||f==224)
		g=getch();
	closegraph();
	main_menu();
}

void exit_menu()
{
	int gd = DETECT, gm;
	int x,i;
	char quit[10];
	char ch,che;
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	settextstyle(3,HORIZ_DIR,4);
	outtextxy(50,200,"Are Your Sure You Want To Quit ???");
	gotoxy(7,17);
	cin>>quit;
	if(quit[0]=='y' || quit[0]=='Y' || !(strcmpi(quit,"yes")))
	{
		x=0;
		cleardevice();
		for(i=0;i<11;i++,x+=50)
		{
			circle(x+50,300,23);
			circle(x+50,300,17);
			circle(x+150,300,23);
			circle(x+150,300,16);
			fillellipse(x+110,265,23,16);
			int points[]={x+55,262,x+70,250,x+100,280,x+80,290,x+55,262};
			drawpoly(5, points);
			int points1[]={x+150,255,x+135,220,x+132,220,x+147,255,x+150,255};
			fillpoly(5,points1);
			line(x+49,299,x+69,279);
			circle(x+49,299,2);
			line(x+47,297,x+67,277);
			line(x+150,300,x+130,275);
			line(x+147,300,x+127,275);
			circle(x+151,301,2);
			rectangle(x+20,250,x+60,265);
			floodfill(x+21,251,WHITE);
			floodfill(x+56,262,WHITE);
			rectangle(x+130,255,x+155,270);
			settextstyle(3,HORIZ_DIR,4);
			outtextxy(30,50,"Thanks For Playing.....See You Soon !!!");
			outtextxy(30,420,"Created By C.Aditya.....");
			delay(300);
			cleardevice();
		}
		closegraph();
		exit(0);
	}
	else
	{
		settextstyle(3,HORIZ_DIR,3);
		outtextxy(30,420,"Press Any Key To Enter The Previous Menu......");
		ch=getch();
		if(ch==0||ch==224)
			che=getch();
		closegraph();
		main_menu();
	}
}

void start()
{
	int x,y,i,x1,x2,y1;
	char ch,che;
	int gd = DETECT, gm;
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	setbkcolor(1);
	settextstyle(0,HORIZ_DIR,6);
	delay(2000);
	for(i=0,x=0,y=0,x1=440,y1=360;i<5;x+=40,y+=40,x1-=40,y1-=40,i++)
	{
		outtextxy(x,y+10,"RACING");
		outtextxy(x1-50,y1+40,"MOTO");
		delay(500);
		cleardevice();
	}
	delay(1000);
	settextstyle(3,HORIZ_DIR,6);
	for(x1=0,x2=500,y=200;x1<200 && x2>200;x1+=50,x2-=50)
	{
		outtextxy(x1,y,"RACING");
		outtextxy(x2,y,"MOTO....");
		delay(750);
		cleardevice();
	}
	delay(1000);
	settextstyle(7,HORIZ_DIR,7);
	outtextxy(90,150,"Racing Moto.....");
	delay(1000);
	settextstyle(8,HORIZ_DIR,3);
	outtextxy(350,260,"VROOM VROOM !!!");
	outtextxy(110,220,"Your Ultimate Racing Experience");
	delay(3000);
	cleardevice();
	setbkcolor(BLACK);
	while(1)
	{
		x=0;
		for(i=0;i<11 && !kbhit();i++,x+=50)
		{
			circle(x+50,300,23);
			circle(x+50,300,17);
			circle(x+150,300,23);
			circle(x+150,300,16);
			fillellipse(x+110,265,23,16);
			int points[]={x+55,262,x+70,250,x+100,280,x+80,290,x+55,262};
			drawpoly(5, points);
			int points1[]={x+150,255,x+135,220,x+132,220,x+147,255,x+150,255};
			fillpoly(5,points1);
			line(x+49,299,x+69,279);
			circle(x+49,299,2);
			line(x+47,297,x+67,277);
			line(x+150,300,x+130,275);
			line(x+147,300,x+127,275);
			circle(x+151,301,2);
			rectangle(x+20,250,x+60,265);
			floodfill(x+21,251,WHITE);
			floodfill(x+56,262,WHITE);
			rectangle(x+130,255,x+155,270);
			settextstyle(3,HORIZ_DIR,3);
			outtextxy(0,450,"Press Any Key To Continue..........");
			delay(300);
			cleardevice();
		}
		if(kbhit())
		{
			ch=getch();
			if(ch==0||ch==224)
				che=getch();
			break;
		}
	}
	closegraph();
	main_menu();
}

void main_menu()
{
	char ch,che;
	int x,y;
	int gd = DETECT, gm;
	initgraph(&gd, &gm, "H:\\TC\\BGI");
	setbkcolor(BLUE);
	setcolor(7);
	settextstyle(2,HORIZ_DIR,5);
	outtextxy(0,450," *  Press 'Enter' To Select The Menu");
	outtextxy(0,430," *  Use 'Down' And 'Up' Arrow Keys To Switch Between Menus");
	settextstyle(3,HORIZ_DIR,2);
	outtextxy(250,105,"Game Menu");
	outtextxy(250,110,"________");
	outtextxy(250,112,"________");
	gotoxy(32,13);
	cout<<" Play Game";
	gotoxy(32,15);
	cout<<" Instructions";
	gotoxy(32,17);
	cout<<" High Score";
	gotoxy(32,19);
	cout<<" Exit";
	gotoxy(27,13);
	cout<<"-->";
	while(1)
	{
		ch=getch();
		if(ch==13)
		{
			y=wherey();
			if(y==13)
			{
				closegraph();
				game();
			}
			if(y==15)
			{
				closegraph();
				instruct();
			}
			if(y==17)
			{
				closegraph();
				high_score();
			}
			if(y==19)
			{
				closegraph();
				exit_menu();
			}
		}
		if(ch==0||ch==224)
		{
			che=getch();
			if(che==72)
			{
				x=wherex();
				y=wherey();
				if(y==15||y==17||y==19)
				{
					gotoxy(27,y);
					cout<<"   ";
					gotoxy(27,y-2);
					cout<<"-->";
				}
				else if(y==13)
				{
					gotoxy(27,y);
					cout<<"   ";
					gotoxy(27,19);
					cout<<"-->";
				}
			}
			else if(che==80)
			{
				x=wherex();
				y=wherey();
				if(y==13||y==15||y==17)
				{
					gotoxy(27,y);
					cout<<"   ";
					gotoxy(27,y+2);
					cout<<"-->";
				}
				else if(y==19)
				{
					gotoxy(27,y);
					cout<<"   ";
					gotoxy(27,13);
					cout<<"-->";
				}
			}
			else
				continue;
		}
		else
			continue;
	}
}

void main()
{
	clrscr();
	start();
}