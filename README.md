# DEAL-MANAGNEMENT-SYSTEM




#include<iostream>
#include<fstream>
#include<stdio.h>
#include<conio.h>
#include<process.h>
#include<stdlib.h>
#include<string.h>
#include<iomanip>
#include <graphics.h>
#include<direct.h>
using namespace std;

void intro();




class wcompany
{
	public:
	int ccode,wcore,wsize,wlen;
	char wtype[20],wcolour[20],cname[20];
	void getdata()
	{
		system("cls");
		cout<<"\n Enter the code of customer:";
		cin>>ccode;
		cout<<"\n Enter your name:";
		gets(cname);
		cout<<"\n Enter your order:";
		cout<<"\n Enter the type of wire:";
		gets(wtype);
		cout<<"\n Enter the number of core of wire:";
		cin>>wcore;
		cout<<"\n Enter the size of wire:";
		cin>>wsize;
		cout<<"\n Enter the colour of the wire:";
		gets(wcolour);
		cout<<"\n Enter the length of wire you want:";
		cin>>wlen;
	}
	void putdata()
	{
		system("cls");
		cout<<"\n Customer code is: "<<ccode;
		cout<<"\n Type of wire :";
		puts(wtype);
		cout<<"\n Number of cores of wire: "<<wcore;
		cout<<"\n Size of wire:"<<wsize;
		cout<<"\n Colour of the wire ";
		puts(wcolour);
		cout<<"\n Length of wire: "<<wlen;
	}
	int c_code()
	{
	return ccode;
	}
};


/*void items()
{
	cout<<"====================================================\n";
	cout<<" S.NO	WIRETYPE   CORE    SIZE	   COLOUR    LENGHT \n";
	cout<<"====================================================\n";
*/




void welcome_screen()
{
	system("cls");
	char ch;
	gotoxy(15,10);
	cout<<"******************* W E L C O M E ********************* ";
	gotoxy(20,12);
	cout<<"*** ARWACHIN BHARTI BHAWAN SR. SEC. SCHOOL *** " ;
	gotoxy(15,14);
	textcolor(WHITE);
	cout<<" W I R E  D E A L E R  M A N A G E M E N T  S O F T W A R E  ";
	gotoxy(33,16);
	textcolor(WHITE);
	cout<<" D O N E  B Y :  ";
	gotoxy(45,18);
	cout<<" NAMAN GUPTA";
	gotoxy(25,20);
	cout<<"";
	textcolor(WHITE);
	gotoxy(35,30);
	cout<<" *** PRESS ANY KEY TO CONTINUE ***";
	getch();
}




int password()
{
	system("cls");
	char p1,p2,p3,p4,p5;
	gotoxy(30,10);
	char str[30]="ENTER THE PASSWORD";
	for(int i=0;str[i]!='\0';i++)
	{ cout<<str[i];
	  delay(50);
	}
	gotoxy(35,20);
	p1=getch();
	cout<<"*";
	p2=getch();
	cout<<"*";
	p3=getch();
	cout<<"*";
	p4=getch();
	cout<<"*";
	p5=getch();
	cout<<"*";
	getch();
	gotoxy(30,20);
	if ((p1=='n'||p1=='N')&&(p2=='a'||p2=='A')&&(p3=='m'||p3=='M')&&(p4=='a'||p4=='A')&&(p5=='n'||p5=='N'))
	return 1;
	else
	return 0;
}
void search()
{
	system("cls");
	wcompany c;
	int r,m;
	int found=0;
	ifstream fin;
	fin.open("wire.dat",ios::in|ios::binary);
	cout<<"\n Enter the customer code to be searched:";
	cin>> r;
	if(!fin)
	{
		cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
		cout<<"\n\n\n Program is closing ....";
		getch();
		exit(0);
	}
	else
	{
		while(!fin.eof())
		{
			fin.read((char*)&c,sizeof(c));
			if(c.c_code()==r)
			{
				cout<<"\n Record found";
				cout<<"\n the record is:";
				c.putdata();
				found+=1;
				break;
			}
		}
	}
	fin.close();
	cout<<"\n Do you want to go back(press 1):";
	cin>>m;
	if(m==1)
	intro();
}



void modify_data()
{
	system("cls");
	wcompany c;
	int ccode,m;
	fstream f;
	f.open("wire.dat",ios::binary|ios::in|ios::out);
	if(!f)
	{
		cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
		cout<<"\n\n\n Program is closing ....";
		getch();
		exit(0);
	}
	else
	{
		cout<<"\n Enter the Code number you want to modify:";
		cin>>ccode;
		while(!f.eof())
		{
		f.read((char*)&c,sizeof(c));
		if(c.ccode==ccode)
		{
			cout<<"\n Enter the new details:";
			c.getdata();
			f.seekp(-1*sizeof(c),ios::cur);
			f.write((char*)&c,sizeof(c));
			cout<<"\n record modified";
		}
		}
	}
	f.close();
	cout<<"\n Do yo want to go back(press 1):";
	cin>>m;
	if(m==1)
	intro();
}


void delete_data()
{
	system("cls");
	wcompany c;
	int ccode,m;
	ifstream fin;
	ofstream fout;
	fin.open("wire.dat",ios::in|ios::binary);
	fout.open("temp.dat",ios::binary|ios::app);
	if(!fin)
	{
		cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
		cout<<"\n\n\n Program is closing ....";
		getch();
		exit(1);
	}
	else
	{
		cout<<"\n enter the customer code you want to delete:";
		cin>>ccode;
		while(!fin.eof())
		{
			fin.read((char*)&c,sizeof(c));
			if(c.ccode!=ccode)
			fout.write((char*)&c,sizeof(c));
			cout<<"\n Record deleted!!!";
		}
	}
	fin.close();
	fout.close();
	remove("wire.dat");
	rename("temp.dat","wire.dat") ;
	cout<<"\n Do you want to go back(press 1):";
	cin>>m;
	if(m==1)
	intro();
}



void search_name()
{
	system("cls");
	char name[20];
	int m;
	wcompany c;
	int flag=0;
	cout<<"\n";
	cout<<"\t\t\t*-----------*"<<"\n";
	cout<<"\t\t\t| SEARCHING |"<<"\n";
	cout<<"\t\t\t*-----------*"<<"\n"<<"\n";
	cout<<"\n\tENTER THE NAME TO BE SEARCHED :";
	gets(name);
	cout<<"\n";
	ifstream fin;
	fin.open("wire.dat",ios::in|ios::binary);
	if(!fin)
	{
		cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
		cout<<"\n\n\n Program is closing ....";
		getch();
		exit(0);
	}
	else
	{
	while(!fin.eof())
	{
		fin.read((char *) &c,sizeof(c));
		if(strcmp(c.cname,name)==0)
		{
			flag=1;
			c.putdata();
			break;
		}
	}
	if(flag==0)
	{
		cout<<"\tSORRY\n";
		cout<<"\tTHE NAME DOES NOT EXIST.\n";
	}
	cout<<"\n Do you want to go back(press 1):";
	cin>>m;
	if(m==1)
	intro();
}
getch();
}

void enter_data();


void entry_menu()
{
	system("cls");
	char ch2;
	cout<<"\n\n\n\tENTRY MENU";
	cout<<"\n\n\t1.CREATE CUSTOMER RECORD";
	cout<<"\n\n\t2.SEARCH CUSTOMER RECORD BY NAME";
	cout<<"\n\n\t3.MODIFY CUSTOMER RECORD";
	cout<<"\n\n\t4.DELETE CUSTOMER RECORD";
	cout<<"\n\n\t5.BACK TO MAIN MENU";
	cout<<"\n\n\tPlease Enter Your Choice : ";
	cin>>ch2;
	switch(ch2)
	{
		case '1': system("cls");
			  enter_data();
			  break;
		case '2': search_name();
			  break;
		case '3': modify_data();
			  break;
		case '4': delete_data();
			  break;
		case '5': intro();
			  break;
		//default:cout<<"\a";
		}
		entry_menu();
}



void show_tabular()
{
       wcompany c;
	cout<<c.ccode<<setw(12)<<c.cname<<setw(10)<<
	c.wtype<<setw(3)<<c.wcore<<setw(3)<<c.wsize<<
	setw(3)<<c.wcolour<<setw(3)<<c.wlen<<endl;
}


void all_rec()
{
	system("cls");
	int m;
	wcompany c;
	ifstream fin;
	fin.open("wire.dat",ios::in|ios::binary);
		if(!fin)
		{
			cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
			cout<<"\n\n\n Program is closing ....";
			getch();
			exit(0);
		}
		else
		{
		cout<<"\n\n\t\tALL CUSTOMERS ORDER \n\n";
		cout<<"====================================================\n";
		cout<<"Customer No. Name          TYPE  CORE  SIZE  COLOUR  LENGHT \n";
		cout<<"====================================================\n";
	while(!fin.eof())
	{
		fin.read((char*)&c,sizeof(c));
		c.putdata();
	}
	fin.close();
	getch();
}
cout<<"\n\tDo you want to exit(press 1):";
cin>>m;
if(m==1)
intro();
}



void display()
{
	system("cls");
	int rno;char ch1,ch2='y';
	system("cls");
	cout<<"\n\n\nDISPLAY MENU";
	cout<<"\n\n\n1. All customer records\n\n2. Customer Record\n\n3.Back to Main Menu";
	cout<<"\n\n\nEnter Choice (1/2)? ";
	cin>>ch1  ;
	switch(ch1)
	{
		case '1' : all_rec();
			 break;
		case '2' :while(ch2=='y'||ch2=='Y')
			{
				search();
				cout<<"\n\nDo you want to See More Result (y/n)?";
				cin>>ch2;
			 }
			break;
		case '3':intro();
		       break;
		default:  cout<<"\n\t Wrong choice entered";
	}
}



void enter_data()
{
	system("cls");
	int m;
	wcompany c;
	ofstream fout;
	fout.open("wire.dat",ios::binary|ios::app);
	if(!fout)
	{
		cout<<"ERROR!!! FILE COULD NOT BE OPEN\n\n\n Go To Entry Menu to create File";
		cout<<"\n\n\n Program is closing ....";
		getch();
		exit(0);
	}
	else
	{
		c.getdata();
		fout.write((char*)&c,sizeof(c));
		cout<<"\n One record added";
		getch();
	}
	fout.close();
	cout<<"\n Do you want to exit(press 1):";
	cin>>m;
	if(m==1)
	intro();
}



void intro()
{
	system("cls");
	char ch;
	textcolor(WHITE);
	cout<<"\n\n\n\tMAIN MENU";
	cout<<"\n\n\t01. ENTRY/EDIT MENU";
	cout<<"\n\n\t02. DISPLAY MENU";
	cout<<"\n\n\t03. EXIT";
	cout<<"\n\n\tPlease Select Your Option (1-3) ";
	cin>>ch;
	switch(ch)
	{
		case '1': system("cls");
			  entry_menu();
			  break;
		case '2': display();
			  break;
		case '3':exit(0);
		default :cout<<"\a";
	}while(ch!='3');
}


int main()
{
	system("cls");
	wcompany c;
	textcolor (WHITE);
	welcome_screen();
	if(!password())
	{
		cout<<"\nWrong password \n Exiting....";
		delay(1000);
		exit(1);
	}
	intro();
	return 0;
}
