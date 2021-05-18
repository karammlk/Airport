# Airport
# C

//Queen Alia Airport Project

//Dr Nayef Abuageel

//Eng Hikmat Shehadi

#include <stdio.h>

#include <string.h>

#include "foc_fa21.h"

//Prototypes

int People();

int Passenger();

void America();

void Europe();

void Africa();

int Employee();

void Get_statistcis();

void Check_name();

int main()
{
	
	printf("** Welcome to International Queen Alia Airport **\n");
	People();
	
	return 0;
}

// function that desplay the main menu 
int People()
{
	int number, counter;
	
	printf("1. passenger\n");
	printf("2. Employee\n");
	printf("3. Quit\n");
	printf("select a choice > ");
	scanf("%d",&number);
	
	counter = 0;
	while(number != 1 && number != 2 && number !=3 && counter < 2)
	{
		printf("Invalid number\n");
		printf("1. Passenger\n");
		printf("2. Employee\n");
		printf("3. Quit\n");
		printf("select a choice > ");
		scanf("%d",&number);
		counter++;
	}
	switch(number)
	{
		case 1 :
		printf("**********************************************\n");
		printf("Passenger\n");
		Passenger();
		break;
		
		case 2 :
		printf("**********************************************\n");
		printf("Employee\n");
		Employee();
		break;
		
		case 3 :
		printf("**********************************************\n");
		printf("Quit\n");
	}
}

//Function to choose destenation to travel to
int Passenger()
{
	int number, counter;
	
	printf("Select where do you want to go ?\n");
	printf("1. America\n");
	printf("2. Europe\n");
	printf("3. Africa\n");
	printf("4. Back\n");
	printf("select a choice > ");
	scanf("%d",&number);
	
	counter = 0;
	while(number != 1 && number != 2 && number != 3 && number != 4 && counter <2)
	{
		printf("Invalid number\n");
		printf("select a choice > %d\n",number);
		printf("Select where do you want to go ?\n");
		printf("1. America\n");
		printf("2. Europe\n");
		printf("3. Africa\n");
		printf("4. Back\n");
		printf("select a choice > ");
		scanf("%d",&number);
	}
	switch(number)
	{
		case 1 :
		printf("**********************************************\n");
		printf("America\n");
		America();
		break;
		
		case 2 :
		printf("**********************************************\n");
		printf("Europe\n");
		Europe();
		break;
		
		case 3 :
		printf("**********************************************\n");
		printf("Africa\n");
		Africa();
		break;
		
		case 4 :
		printf("**********************************************\n");
		printf("Back\n");
		People();
		break;
	}
}

// America function to check the valdity of visa number then save at the file if valid or inform passenger the visa in invalid
void America()
{
	char Traveler_name[20];
	int Visa_number, Test, Test1, counter = 0;
	
	FILE *Americaf;
	Americaf = fopen("America.txt" , "a");
	
	printf("Input your first name : ");
	scanf("%s",Traveler_name);
	
	printf("Ok Mr. %s please input your visa number : ",Traveler_name);
	scanf("%d",&Visa_number);
	
	if(Visa_number < 10000 || Visa_number >= 100000)
		printf("Your visa is invalid\n");
	
	else
	{
		Test = Visa_number / 100;
	
		if(Test != 123)
			printf("Your visa is invalid\n");
	
		else
		{
			Test1 = Visa_number % 100;
			
			if(Test1 <= 80 && Test1 >= 50)
			{
				printf("Please move to counter number four \n");			
				fprintf(Americaf, "first name : %s / Visa number = %d\n", Traveler_name, Visa_number);
			}
			else
				printf("Sorry! your visa needs to be validated please check that with the USA Embassy\n");	
		}
	}
	fclose(Americaf);
}

//Check schengen number then decide the country
void Europe()
{
	int Number_of_Schengen, counter = 0;
	
	FILE *Europef;
	Europef = fopen("Europe.txt" , "a");
	
	printf("Input your Schengen number : ");
	scanf("%d",&Number_of_Schengen);
	
	if(Number_of_Schengen < 10)
		printf("Invalid Schengen number\n");
	
	else if(Number_of_Schengen >= 10 && Number_of_Schengen < 100)
	{
		printf("Germany, Window 10\n");
		fprintf(Europef, "Schengen number is : %d\n" ,Number_of_Schengen);
	}
	else if(Number_of_Schengen >= 100 && Number_of_Schengen < 1000)
	{
		printf("Italy, Window 11\n");
		fprintf(Europef, "Schengen number is : %d\n" ,Number_of_Schengen);
	}
	else if(Number_of_Schengen >= 1000 && Number_of_Schengen < 10000)
	{
		printf("Spain, Window 12\n");
		fprintf(Europef, "Schengen number is : %d\n" ,Number_of_Schengen);
	}	
	else
	{
		printf("Greece, Window 13\n");
	 	fprintf(Europef, "Schengen number is : %d\n" ,Number_of_Schengen);
	}
	fclose(Europef);
}

//Draw the location where to go
void Africa()
{
	printf("Please move to this location");
	
	int location[200][400], Rows, columns;
	
	for(Rows = 0; Rows < 200; Rows++)
	{
		for(columns = 0; columns < 400; columns++)
		{
			location[Rows][columns] = 0;
			
			if(Rows == 100 || columns == 200)
				location[Rows][columns] = 255;
			
			if(Rows >= 40.31 && Rows <= 60.31 && columns > 320.290 && columns <= 340.290)
				location[Rows][columns] = 255;
		}
	}
	showArray(200,400,location);
}

//Check password , give three times then open the selection menu
int Employee()
{
	int Number, counter, comparison;
	char password[10];
	
	printf("You have three tries\n");
	printf("Please enter the password : ");
	scanf("%s",password);
	comparison = strcmp("admin",password);
	
	counter = 1;
	while(comparison != 0 && counter < 3)
	{
		printf("Password != %s\n",password);
		printf("Please enter the password : ");
		scanf("%s",password);
		comparison = strcmp("admin",password);
		counter++;
	}
	
	if(comparison != 0)
		printf("Invalid password\n");
	
	else
	{
		printf("1.Get statistcis\n");
		printf("2.Check name\n");
		printf("3.Back\n");
		printf("select a choice > ");
		scanf("%d",&Number);
		
		counter = 1;
		while(Number != 1 && Number != 2 && Number != 3 && counter < 3)
		{
			printf("Invalid number\n");
			printf("1.Get statistcis\n");
			printf("2.Check name\n");
			printf("3.Back\n");
			printf("select a choice > ");
			scanf("%d",&Number);
			counter++;
		}
		switch(Number)
		{
			case 1 :
			printf("***************************************\n");
			printf("Get statistcis\n");
			Get_statistcis();
			break;
			
			case 2 :
			printf("***************************************\n");
			printf("Check name\n");
			Check_name();
			break;
			
			case 3 :
			printf("***************************************\n");
			printf("Back\n");
			People();
			break;
			
			default :
			printf("Invalid choice\n");
		}
	}
}

//Calculate the number of travelers from the files of each destenation
// Draw colum for each destenation that represent the percentage of travelers to all travelers
void Get_statistcis()
{
	int Number_of_passenger[200][600], Rows, columns;
	double Number_of_travelers_to_America, Number_of_travelers_to_Europe, Number_of_travelers_to_Africa, Avg_America, Avg_Europe, Avg_Africa, Sum;
	char pointer;

	FILE *Americaf;
	Americaf = fopen("America.txt" , "r");
	
	for(pointer = getc(Americaf); pointer != EOF; pointer = getc(Americaf))
		if(pointer == '\n')
			Number_of_travelers_to_America++;
	printf("The number of travelers to America = %.2lf\n",Number_of_travelers_to_America);
	
	FILE *Europef;
	Europef = fopen("Europe.txt" , "r");
	
	for(pointer = getc(Europef); pointer != EOF; pointer = getc(Europef))
		if(pointer == '\n')
			Number_of_travelers_to_Europe++;
	printf("The number of travelers to Europe = %.2lf\n",Number_of_travelers_to_Europe);
	
	FILE *Africaf;
	Africaf = fopen("Africa.txt" , "r");
		
	for(pointer = getc(Africaf); pointer != EOF; pointer = getc(Africaf))
		if(pointer == '\n')
			Number_of_travelers_to_Africa++;
	printf("The number of travelers to Africa = %.2lf\n",Number_of_travelers_to_Africa);
	
	Sum = Number_of_travelers_to_America + Number_of_travelers_to_Europe + Number_of_travelers_to_Africa;
	printf("Sum of travelers = %.2lf\n",Sum);
	
	Avg_America = 200 - (100 * Number_of_travelers_to_America / Sum);
	printf("Avg_America = %.2f\n", Avg_America);
	
	Avg_Europe = 200 - (100 * Number_of_travelers_to_Europe / Sum);
	printf("Avg_Europe = %.2f\n", Avg_Europe);
	
	Avg_Africa = 200 - (100 * Number_of_travelers_to_Africa / Sum);
	printf("Avg_Africa = %.2f\n", Avg_Africa);
	
	int Break;
	printf("To continue input a number : ");
	scanf("%d",&Break);
	
	for(Rows = 0; Rows < 200; Rows++)
	{
		for(columns = 0; columns < 600; columns++)
		{
			Number_of_passenger[Rows][columns] = 255;
			
			if(Rows <= 200 && Rows >= 100 && columns >= 100 && columns <= 120)
			Number_of_passenger[Rows][columns] = 127.5;
			
			if(Rows <= 200 && Rows >= 102 && columns >= 102 && columns <= 118)
			Number_of_passenger[Rows][columns] = 255;
			
			if(Rows <= 200 && Rows >= Avg_America && columns >= 100 && columns <= 120)
			Number_of_passenger[Rows][columns] = 0;
			
			if(Rows <= 200 && Rows >= 100 && columns >= 300 && columns <= 320)
			Number_of_passenger[Rows][columns] = 127.5;
			
			if(Rows <= 200 && Rows >= 102 && columns >= 302 && columns <= 318)
			Number_of_passenger[Rows][columns] = 255;
			
			if(Rows <= 200 && Rows >= Avg_Europe && columns >= 300 && columns <= 320)
			Number_of_passenger[Rows][columns] = 0;
			
			if(Rows <= 200 && Rows >= 100 && columns >= 500 && columns <= 520)
			Number_of_passenger[Rows][columns] = 127.5;
			
			if(Rows <= 200 && Rows >= 102 && columns >= 502 && columns <= 518)
			Number_of_passenger[Rows][columns] = 255;
			
			if(Rows <= 200 && Rows >= Avg_Africa && columns >= 500 && columns <= 520)
			Number_of_passenger[Rows][columns] = 0;
		
		}
	}
	showArray(200,600,Number_of_passenger);
	
	fclose(Americaf);
	fclose(Europef);
	fclose(Africaf);
}

// Search for a name in the file Names, then print if the passenger can travel or not
void Check_name()
{
	char names[20], name_test[20];
	int travel, comparison;
	
	FILE *Namef;
	Namef = fopen("Name.txt" , "r");
	
	printf("Enter the name : ");
	scanf("%s",name_test);
	
	if(Namef == NULL)
	printf("Error! couldn't open file");
	
	else
	{
		while(!feof(Namef))
		{
			fscanf(Namef, "%s %d\n" ,names, &travel);
			comparison = strcmp(name_test, names);
			
			if(comparison == 0)
			{
				if(travel == 1)
					printf("The passenger can travel\n");
				
				else if(travel == 0)
					printf("The passenger can't travel\n");
				
			}
			if(comparison == 0)
			break;
		}
		if(comparison != 0)
		printf("The passenger not found\n");
	}
	fclose(Namef);
}
