# eulerODE
the code written in C for newton cooling law using eulers method

#include <stdio.h>
#include <iostream>


typedef double F(double,double); //declaring a new type function with 2 variables


double k, T0, Tk, h;  //introducing our global variables, that define ODEs conditions 

void euler(F f,double y, double a, double b, double w)  //the function , that defines euler methot for ODE

{	

	
	for(double t = a;t <=b;t += (w)){
		printf("%f\t%f\n ",t ,y); //writes the results
		y += w * f(t,y); // euler method
		
	}
	printf("done\n");
}


void read_ex(double *x, double *y, double *z, double *j) //reads and shows us ODEs parametres
{
	FILE *file = fopen("allparams.txt","r");
	fscanf(file,"%lf%lf%lf%lf", x, y, z, j);
	fclose(file);
	printf("k = %f\nT0 = %f\nTk = %f\nh = %f\n" , *x, *y , *z, *j);
}



void read_ex1(double *l,double *n) // reads the data for our new type function 
{
	FILE *file = fopen("k,T0.txt","r");
	fscanf(file,"%lf%lf",l, n);
	fclose(file);
	
}



double newtonLaw(double ,double t) // our typedef function , that returns the f(t,y) value
{	
	return -(k) * (t- T0);

}



int main(){
	read_ex1(&k,&T0);
	read_ex(&k,&T0,&Tk,&h); 
	euler(newtonLaw,100.0,0,Tk,h); //calls the euler function , with chosen parametres
	return 0;
	
}
