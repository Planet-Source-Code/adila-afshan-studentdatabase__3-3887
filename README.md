<div align="center">

## studentdatabase


</div>

### Description

Maintain the Student Records.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Adila Afshan](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/adila-afshan.md)
**Level**          |Intermediate
**User Rating**    |3.7 (11 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\)
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__3-5.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/adila-afshan-studentdatabase__3-3887/archive/master.zip)

### API Declarations

```
#include<iostream.h>
 #include<fstream.h>
 #include<conio.h>
 #define LEFT 20
 #define TOP 8
 #define RIGHT 12
 #define BOT 21
 #define DESLEFT 1
 #define DESTOP 1
 #define NUMCOLORS 16
 #include<string.h>
 #include<graphics.h>
 #define FONT_SIZE 6
 #define CL  300
 #define LEAD 40
```


### Source Code

```
/*including header files*/
 #include<iostream.h>
 #include<fstream.h>
 #include<conio.h>
 #define LEFT 20
 #define TOP 8
 #define RIGHT 12
 #define BOT 21
 #define DESLEFT 1
 #define DESTOP 1
 #define NUMCOLORS 16
 #include<string.h>
 #include<graphics.h>
 #define FONT_SIZE 6
 #define CL  300
 #define LEAD 40
 typedef int bool;
 const int TRUE = 1;
 const int FALSE = 0;
 /* this structure is the "heart" of the program */
 struct Student
 {
  char First_Name[35];
  char Last_Name[35];
  char Father_Name[30];
  char Age[3];
  char Department[35];
  char Roll_Number[15];
  char Semester[10];
  char G_P_A[8];
  char Address[50];
  char City[35];
  char Email_Address[35];
  char DOB[10];
  char Matric_Perc[7];
  char Grade[3];
  char Inter_Perc[7];
  char Igrade[3];
 };
 /* start of function prototypes */
 void Display_Students(Student [], int);
 void Listact_Students(Student [], int);
 bool Load_Student_Data(Student [], int &);
 int Lookup_Students(Student [],int, char *);
 void Get_Choice(int &);
 bool Add_Student(Student [], int &);
 bool Listadd_Student(Student [], int &);
 bool Delete_Student(Student [],int &);
 void Save_Data(Student [], int);
 void Sort_Student(Student [], int);
 /* end of function prototypes */
 int main()
 {
 clrscr();
 textbackground( BLACK );
 textcolor( GREEN );
 gotoxy(15, 8);
 cout<< "NOW START........................ ..Press Enter Key" ;
 getche();
 clrscr();
 int j;
 window(LEFT, TOP, RIGHT, BOT);
 textbackground( BLUE );
 for( j=0; j<98; j++ )
 {
  textcolor(j % NUMCOLORS );
  cout<<" WELCOME TO MY PROJECT  ";
 }
  movetext( LEFT, TOP, RIGHT, BOT, DESLEFT, DESTOP );
  getche();
  clrscr();
 {
  int driver = DETECT;
  int mode;
  int left, top, right, bot;
  initgraph( &driver, &mode, "c:\\tc\\bgi");
  left = top = 25;
  right = 600;
  bot = 450;
  setcolor( GREEN );
  setfillstyle( WIDE_DOT_FILL,LIGHTGRAY );
  floodfill(left, top, WHITE );
  rectangle( left, top, right, bot);
  settextstyle( TRIPLEX_FONT, HORIZ_DIR, FONT_SIZE );
  moveto( CL, LEAD*6);
  settextjustify( CENTER_TEXT, BOTTOM_TEXT);
  outtext("STUDENT DATABASE PROGRAM");
  getche();
  clrscr();
  setcolor( BLUE);
  setfillstyle( CLOSE_DOT_FILL,MAGENTA );
  floodfill(left, top, YELLOW );
  rectangle( left, top, right, bot);
  textcolor( BLUE );
  textbackground( WHITE );
  gotoxy(15,8);
  cout<<"      INTRODUCTION TO PROGRAM       ";
  gotoxy(15, 13);
  cout<<"   This program consists of 8 options     ";
  gotoxy(15, 15);
  cout<< " The Structure is the Heart of this Program. ";
  gotoxy(15, 17);
  cout<<"   This program  first open a file.    ";
  gotoxy(15, 19);
  cout<<"      Use file name with .DAT       ";
  gotoxy(15, 20);
  cout<<"          ENJOY            ";
  gotoxy(15, 24);
  cout<<"       MADE BY:- ADILA AFSHAN       ";
  getche();
  closegraph();
  }
 /*
 This is the main function.
 All this function does is will call the
 function Get_Choice and from there relay
 the information to any one of the other
 functions
 */
 Student RAM[100]; /* RAM stands for random access memory */
 int Number_of_Students; /*this int will be used throughout the run */
 int Choice;
 int Location;
 char Search_Key[35];
 window( LEFT, TOP,RIGHT, BOT);
 textcolor (BLUE );
 textbackground( GREEN );
 if(Load_Student_Data(RAM, Number_of_Students))
  /* check to see if file is valid during opening */
 {
 cout<<"Number of student read from file = "
 <<Number_of_Students<<endl;
	 /* start of user menu */
	 do
	 {
	 //call get choice
	 //this function will give back a user reply
	 Get_Choice(Choice);
	 switch(Choice)
	 {
	 case 1:
	 Display_Students(RAM, Number_of_Students);
	 break;
	 case 2:
	 clrscr();
	 Listact_Students(RAM, Number_of_Students);
	 break;
	 case 3:
	 clrscr();
	 if( Add_Student(RAM, Number_of_Students))
	{
	 clrscr();
	 textbackground( LIGHTBLUE );
	 textcolor( GREEN );
	 gotoxy(25,11);
	 cout<<"Student successfully added"<<endl;
	 gotoxy(25,12);
	 cout<<"Press enter to continue";
	 getch();
	}
	 else
	{
	 clrscr();
	 textbackground( WHITE );
	 textcolor( MAGENTA );
	 gotoxy(25,11);
	 cout<<"Student already in database"<<endl;
	 gotoxy(25,12);
	 cout<<"Student was not successfully added"<<endl;
	 gotoxy(25,13);
	 cout<<"Press enter to continue"<<endl;
	 getch();
	}
	 break;
	 case 4:
	 clrscr();
	 if( Listadd_Student(RAM, Number_of_Students))
	{
	 clrscr();
	 textbackground( YELLOW );
	 textcolor( GREEN );
	 gotoxy(25,11);
	 cout<<"Student successfully added"<<endl;
	 gotoxy(25,12);
	 cout<<"Press enter to continue";
	 getch();
	}
	 else
	{
	 clrscr();
	 textbackground( WHITE );
	 textcolor( MAGENTA );
	 gotoxy(25,11);
	 cout<<"Student already in database"<<endl;
	 gotoxy(25,12);
	 cout<<"Student was not successfully added"<<endl;
	 gotoxy(25,13);
	 cout<<"Press enter to continue"<<endl;
	 getch();
	}
	 break;
	 case 5:
	{
	 clrscr();
	 cin.ignore(80, '\n');
	 gotoxy(25, 11);
	 cout<<"Enter the student's first or last name: ";
	 cin.get(Search_Key, 35);
	 cin.ignore(80, '\n');
	 int loc =
	 Lookup_Students(RAM, Number_of_Students, Search_Key);
	 if(loc != -1){
	 clrscr();
	 cout<<"Student found: \n\n";
	 cout<<RAM[loc].First_Name<<endl;
	 cout<<RAM[loc].Last_Name<<endl;
	 cout<<RAM[loc].Father_Name<<endl;
	 cout<<RAM[loc].Age<<endl;
	 cout<<RAM[loc].Department<<endl;
	 cout<<RAM[loc].Roll_Number<<endl;
	 cout<<RAM[loc].Semester<<endl;
	 cout<<RAM[loc].G_P_A<<endl;
	 cout<<RAM[loc].Address<<endl;
	 cout<<RAM[loc].City<<endl;
	 cout<<RAM[loc].Email_Address<<endl;
	 cout<<"Press enter to continue";
	 getch();
	 cout<<endl;
	}
	 else
	{
	 clrscr();
	 gotoxy(25,11);
	 cout<<"Requested student was not found in the data base"<<endl;
	 gotoxy(25, 12);
	 cout<<"Press enter to continue";
	 getch();
	}
	};
	 break;
	 case 6:
	 if( Delete_Student(RAM, Number_of_Students) )
	{
	 clrscr();
	 gotoxy(25,11);
	 cout<<"Student successfully deleted"<<endl;
	 gotoxy(25,12);
	 cout<<"Press enter to continue"<<endl;
	 getch();
	}
	 else
	{
	 clrscr();
	 gotoxy(25,11);
	 cout<<"Student could not be found in database"<<endl;
	 gotoxy(25,12);
	 cout<<"Therefore student could not be deleted"<<endl;
	 gotoxy(25,13);
	 cout<<"Press enter to continue"<<endl;
	 getch();
	}
	 break;
	 case 7:
	 Save_Data(RAM, Number_of_Students);
	 break;
	}
	}
	 while(Choice!=8);
	 clrscr();
	 textcolor( WHITE );
	 textbackground( BLUE );
	 gotoxy(25,10);
	 cout<<"******THANK YOU******";
	 getche();
	}
	else
   {
	 clrscr();
	 gotoxy(25,11);
	 cout<<"An error has occurred in opening the file."<<endl;
	 gotoxy(25,12);
	 cout<<"The program execution has terminated."<<endl;
	 gotoxy(25,13);
	 cout<<"Press enter to continue";
	 getch();
   }
  return(0);
 }
 /*
 This is the start of all the functions used in this program
 Each function performs a different job.
 They basicly rely on getting a copy of RAM and the number of
 students.
 */
 void Get_Choice(int &Choice)
 {
 clrscr();
 window( LEFT, TOP, RIGHT, BOT);
 textbackground( YELLOW );
 textcolor (BLACK );
 /*keep repeating untill a valid choice is made */
   do
  {
   clrscr();
   window(LEFT, TOP, RIGHT, BOT);
   textbackground( WHITE );
   textcolor( MAGENTA );
   gotoxy(15,8);
   cout<<"WELCOME TO MY PROJECT";
   gotoxy(25, 9);
   cout<<"Enter choice: "<<endl;
   gotoxy(25, 10);
   cout<<"1 - Display student list"<<endl;
   gotoxy(25, 11);
   cout<<"2 - Display Acedemic Record"<<endl;
   gotoxy(25, 12);
   cout<<"3 - Add a student"<<endl;
   gotoxy(25, 13);
   cout<<"4 - Add acedemic Record "<<endl;
   gotoxy(25, 14);
   cout<<"5 - Search for a student"<<endl;
   gotoxy(25, 15);
   cout<<"6 - Delete a student"<<endl;
   gotoxy(25, 16);
   cout<<"7 - Save all changes"<<endl;
   gotoxy(25, 17);
   cout<<"8 - Exit"<<endl;
   gotoxy(25, 18);
   cout<<"Enter a choice 1-8 from above: ";
   cin>>Choice;
   cin.ignore(80, '\n');
   if( (Choice < 1) || (Choice > 8) )
   {
    clrscr();
    gotoxy(25, 11);
    cout<<"Choice must be 1, 2, 3, 4, 5,6,7 or 8!"<<endl;
    gotoxy(25, 12);
    cout<<"Press enter to continue"<<endl;
    getch();
   }
   }
   while( (Choice < 1) || (Choice > 8));
   }
 void Display_Students(Student Contact[], int Length)
 {
 clrscr();
 textbackground( YELLOW );
 textcolor( BLACK );
 Sort_Student(Contact, Length);
 for(int i = 0;i < Length; i++)
 {
 cout<<Contact[i].First_Name<<endl;
 cout<<Contact[i].Last_Name<<endl;
 cout<<Contact[i].Father_Name<<endl;
 cout<<Contact[i].Age<<endl;
 cout<<Contact[i].Department<<endl;
 cout<<Contact[i].Roll_Number<<endl;
 cout<<Contact[i].Semester<<endl;
 cout<<Contact[i].G_P_A<<endl;
 cout<<Contact[i].Address<<endl;
 cout<<Contact[i].City<<endl;
 cout<<Contact[i].Email_Address<<endl;
 cout<<endl; /*blank line */
 }
 cout<<"Press enter to continue";
 getch();
 }
 void Listact_Students(Student Contact[], int Length)
 {
 clrscr();
 textbackground( YELLOW );
 textcolor( BLACK );
 Sort_Student(Contact, Length);
 for(int i = 0;i < Length; i++)
 {
 cout<<Contact[i].First_Name<<endl;
 cout<<Contact[i].Last_Name<<endl;
 cout<<Contact[i].Father_Name<<endl;
 cout<<Contact[i].DOB<<endl;
 cout<<Contact[i].Matric_Perc<<endl;
 cout<<Contact[i].Grade<<endl;
 cout<<Contact[i].Inter_Perc<<endl;
 cout<<Contact[i].Igrade<<endl;
 cout<<endl; /* blank line */
 }
 cout<<"Press enter to continue";
 getch();
 }
 bool Load_Student_Data(Student Contact[], int &Length)
 {
 ifstream infile;
 char Inputfile[20];
 clrscr();
 gotoxy(25, 11);
 cout<<"Enter the name of the input file: ";
 cin.get(Inputfile, 20);
 cin.ignore(80, '\n');
 infile.open(Inputfile,ios::in);
 int Index = 0;
 if (infile)
 {
 while( !infile.eof() )
 {
 infile.get(Contact[Index].First_Name, 35);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Last_Name, 35);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Father_Name,30);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Age,3);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Department,35);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Roll_Number, 15);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Semester, 10);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].G_P_A, 8);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Address, 50);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].City, 35);
 infile.ignore(80, '\n');
 infile.get(Contact[Index].Email_Address, 35);
 infile.ignore(80, '\n');
 Index++;
 }
 infile.close();
 Length = Index - 1;
 return(TRUE);
 }
 else
 {
 return(FALSE);
 }
 }
 int Lookup_Students(Student Contact[], int Length, char key[])
 {
 for(int k = 0;k < Length; k++){
 if( (strcmp(key,Contact[k].First_Name) == 0) ||
   (strcmp(key,Contact[k].Last_Name) == 0))
 return(k);
 }
 return(-1);
 }
 bool Add_Student(Student Contact[], int &Length)
 {
 char First_Name[35];
 clrscr();
 textbackground( LIGHTBLUE );
 textcolor (LIGHTGREEN );
 gotoxy(25,11);
 cout<<"Please enter the student's first name: ";
 cin.get(First_Name, 35);
 cin.ignore(80, '\n');
 int Location =
 Lookup_Students(Contact, Length, First_Name);
 if(Location == -1)
 {
 int Counter = Length;
 Length++;
 clrscr();
 textbackground( CYAN );
 textcolor( BROWN );
 gotoxy(20, 5);
 cout<<"   THIS IS STUDENT'S RECORDS PROGRAM ";
 gotoxy(20, 6);
 cout<< "   ********************************* ";
 gotoxy(25, 9);
 cout<<"Please enter the student you wish to enter: "<<endl;
 gotoxy(25, 10);
 cout<<"First Name: ";
 cin.get(Contact[Counter].First_Name, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 11);
 cout<<"Last Name: ";
 cin.get(Contact[Counter].Last_Name, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 12);
 cout<<"Father_Name :";
 cin.get(Contact[Counter].Father_Name, 30);
 cin.ignore(80, '\n');
 gotoxy(25, 13);
 cout<<"Age : ";
 cin.get(Contact[Counter].Age,3);
 cin.ignore(80, '\n');
 gotoxy(25, 14);
 cout<<"Department :";
 cin.get(Contact[Counter].Department, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 15);
 cout<<"Roll_Number : ";
 cin.get(Contact[Counter].Roll_Number, 15);
 cin.ignore(80, '\n');
 gotoxy(25, 16);
 cout<<"Semester : ";
 cin.get(Contact[Counter].Semester, 10);
 cin.ignore(80, '\n');
 gotoxy(25, 17);
 cout<<"G_P_A :";
 cin.get(Contact[Counter].G_P_A, 8);
 cin.ignore(80, '\n');
 gotoxy(25, 18);
 cout<<"Address: ";
 cin.get(Contact[Counter].Address, 50);
 cin.ignore(80, '\n');
 gotoxy(25, 19);
 cout<<"City: ";
 cin.get(Contact[Counter].City, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 20);
 cout<<"Email_Address : ";
 cin.get(Contact[Counter].Email_Address, 35);
 cin.ignore(80, '\n');
 return(TRUE);
 }
 else
 {
 return(FALSE);
 }
 }
 bool Listadd_Student(Student Contact[], int &Length)
 {
 char First_Name[35];
 clrscr();
 textbackground( LIGHTBLUE );
 textcolor (LIGHTGREEN );
 gotoxy(25,11);
 cout<<"Please enter the student's first name: ";
 cin.get(First_Name, 35);
 cin.ignore(80, '\n');
 int Location =
 Lookup_Students(Contact, Length, First_Name);
 if(Location == -1)
 {
 int Counter = Length;
 Length++;
 clrscr();
 textbackground( CYAN );
 textcolor( BROWN );
 gotoxy(20, 5);
 cout<<"  THIS IS STUDENT'S ACEDEMIC RECORDS PROGRAM ";
 gotoxy(20, 6);
 cout<<"  *******************************************";
 gotoxy(25, 9);
 cout<<"Please enter the student you wish to enter: "<<endl;
 gotoxy(25, 10);
 cout<<"First Name: ";
 cin.get(Contact[Counter].First_Name, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 11);
 cout<<"Last Name: ";
 cin.get(Contact[Counter].Last_Name, 35);
 cin.ignore(80, '\n');
 gotoxy(25, 12);
 cout<<"Father_Name :";
 cin.get(Contact[Counter].Father_Name, 30);
 cin.ignore(80, '\n');
 gotoxy(25, 13);
 cout<<"D-O-B : ";
 cin.get(Contact[Counter].DOB,10);
 cin.ignore(80, '\n');
 gotoxy(25, 14);
 cout<<"Matric_Percentage :";
 cin.get(Contact[Counter].Matric_Perc, 7);
 cin.ignore(80, '\n');
 gotoxy(25, 15);
 cout<<"Grade : ";
 cin.get(Contact[Counter].Grade, 3);
 cin.ignore(80, '\n');
 gotoxy(25, 16);
 cout<<"Inter_Percentage :";
 cin.get(Contact[Counter].Inter_Perc, 7);
 cin.ignore(80, '\n');
 gotoxy(25, 17);
 cout<<"Inter Grade : ";
 cin.get(Contact[Counter].Igrade, 3);
 cin.ignore(80, '\n');
 return(TRUE);
 }
 else
 {
 return(FALSE);
 }
 }
 bool Delete_Student(Student Contact[], int &Length)
 {
 char Name[35];
 clrscr();
 textbackground( BLUE );
 textcolor( GREEN);
 gotoxy(5, 11);
 cout<<"Please enter the first or last name of the student to be deleted: ";
 cin.get(Name, 35);
 cin.ignore(80, '\n');
 int Location =
 Lookup_Students(Contact, Length, Name);
 int Counter = 0;
 if(Location != -1)
 {
 for(int i = 0;i < Length; i++)
 {
 if( (strcmp(Name,Contact[i].First_Name) == 0) ||
   (strcmp(Name,Contact[i].Last_Name) == 0))
 {
 Counter++;
 Length--;
 }
 strcpy(Contact[i].First_Name, Contact[Counter].First_Name);
 strcpy(Contact[i].Last_Name, Contact[Counter].Last_Name);
 strcpy(Contact[i].Father_Name, Contact[Counter].Father_Name);
 strcpy(Contact[i].Age, Contact[Counter].Age);
 strcpy(Contact[i].Department, Contact[Counter].Department);
 strcpy(Contact[i].Roll_Number, Contact[Counter].Roll_Number);
 strcpy(Contact[i].Semester, Contact[Counter].Semester);
 strcpy(Contact[i].G_P_A, Contact[Counter].G_P_A);
 strcpy(Contact[i].Address, Contact[Counter].Address);
 strcpy(Contact[i].City, Contact[Counter].City);
 strcpy(Contact[i].Email_Address, Contact[Counter].Email_Address);
 strcpy(Contact[i].DOB, Contact[Counter].DOB);
 strcpy(Contact[i].Matric_Perc, Contact[Counter].Matric_Perc);
 strcpy(Contact[i].Grade, Contact[Counter].Grade);
 strcpy(Contact[i].Inter_Perc, Contact[Counter].Inter_Perc);
 strcpy(Contact[i].Igrade, Contact[Counter].Igrade);
 Counter++;
 }
 return(TRUE);
 }
 else
 {
 return(FALSE);
 }
 }
 void Save_Data(Student Contact[], int Length)
 {
 ofstream outfile;
 char File_Name[35];
 clrscr();
 textbackground( GREEN );
 textcolor( YELLOW ) ;
 gotoxy(5, 11);
 cout<<"Please enter the name of the file you wish to save to: ";
 cin.get(File_Name, 35);
 cin.ignore(80, '\n');
 outfile.open(File_Name,ios::out); /* open file */
 if(outfile)
  {
   for(int k = 0;k < Length;k++)
  {
   outfile<<Contact[k].First_Name<<endl;
   outfile<<Contact[k].Last_Name<<endl;
   outfile<<Contact[k].Father_Name<<endl;
   outfile<<Contact[k].Age<<endl;
   outfile<<Contact[k].Department<<endl;
   outfile<<Contact[k].Roll_Number<<endl;
   outfile<<Contact[k].Semester<<endl;
   outfile<<Contact[k].G_P_A<<endl;
   outfile<<Contact[k].Address<<endl;
   outfile<<Contact[k].City<<endl;
   outfile<<Contact[k].Email_Address<<endl;
   outfile<<Contact[k].DOB<<endl;
   outfile<<Contact[k].Matric_Perc<<endl;
   outfile<<Contact[k].Grade<<endl;
   outfile<<Contact[k].Inter_Perc<<endl;
   outfile<<Contact[k].Igrade<<endl;
  }
   clrscr();
   textbackground( GREEN );
   textcolor ( BLUE );
   gotoxy(25, 11);
   cout<<"File successfully saved!"<<endl;
   gotoxy(25, 12);
   cout<<"Press enter to continue"<<endl;
   getch();
  }
  else
  {
   clrscr();
   textbackground( DARKGRAY );
   textcolor( LIGHTRED );
   gotoxy(25, 11);
   cout<<"An error has occurred!"<<endl;
   gotoxy(25, 12);
   cout<<"Program execution halted"<<endl;
   gotoxy(25, 13);
   cout<<"Press enter to continue"<<endl;
   getch();
  }
 }
 void Sort_Student(Student Contact[], int Length)
 {
  /* start of bubble sort */
  int Number_of_Comparisons = Length - 1;
  Student Temp;
  bool Swap_Occured;
  do
  {
  Swap_Occured = FALSE;
  for(int i = 0; i < Number_of_Comparisons; i++)
  {
  if( strcmp(Contact[i].First_Name, Contact[i + 1].First_Name) > 0)
	  {
	    Temp = Contact[i + 1];
	    Contact[i + 1] = Contact[i];
	    Contact[i] = Temp;
	    Swap_Occured = TRUE;
	  };
	}
   Number_of_Comparisons--;
   }
   while(Swap_Occured);
 }
```

