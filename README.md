/*
Given 6 Integers x1,y1,x2,y2,x3,y3 ,Find what Type of Triangle can be formed from (x1,y1)(x2,y2)(x3,y3)

Input : 0,0,2,0,0,2
Output : "Isosceles Triangle"

Types will be "Scalene","Equilateral","Isosceles","Cannot be a traingle"

Hint : Find 3 sides lengths ,and Find the type .You can use the formula for distance between two points .

Bonus Task : Also print whether its Acute , Obtuse or Right Angled Triangle

Extra Task : Give the example of equilateral traingle, Just write the coordinates of one equilateral traingle
 in the below line.
 (x1,y1),(x2,y2),(x3,y3) // Replace this three points with the example

Optional : Do these with floats, instead of ints.*/


#include<stdio.h>
#include<math.h>

void typeofTraingle(int x1,int y1,int x2,int y2,int x3,int y3)
{

    float side_a,side_b,side_c;
    
    /*finding the lengths of sides. let length between points (x1,y1) and (x2,y2) be 'a'
                                                            (x2,y2) and (x3,y3) be 'b'
                                                            (x3,y3) and (x1,y1) be 'c'*/
    side_a= sqrt( (( x2 - x1 ) * ( x2 - x1 )) + (( y2 - y1 ) * ( y2 - y1 )) );
    side_b= sqrt( (( x3 - x2 ) * ( x3 - x2 )) + (( y3 - y2 ) * ( y3 - y2 )) );
    side_c= sqrt( (( x1 - x3 ) * ( x1 - x3 )) + (( y1 - y3 ) * ( y1 - y3 )) );
    
    if((( side_a + side_b ) < side_c ) || (( side_b + side_c ) < side_a ) || (( side_c + side_a ) < side_b))
        printf("Cannot form a triangle\n");
     else if( side_a == side_b )
     {
            if( side_a == side_c )
                printf("Equilatera\n");
            else
                printf("Isosceles\n");
     }
    else if( side_b == side_c )
            printf("Isosceles\n");
    else if( side_a == side_c )
            printf("Isosceles\n");
    else printf("Scalene\n");

    findslope(x1,y1,x2,y2,x3,y3);
}

void findslope(int x1,int y1,int x2,int y2,int x3,int y3)
{

    float slope_a,slope_b,slope_c;
    //finding the slopes of respective lines a,b,c
    slope_a=( y2 - y1 ) / ( x2 - x1 );

    slope_b=( y3 - y2 ) / ( x3 - x2 );

    slope_c=( y1 - y3 ) / ( x1 - x3 );

    findtypetriangle(slope_a,slope_b,slope_c);
    return 0;
}

void findtypetriangle(float slope_a,float slope_b,float slope_c)
{

    float Theta_1,Theta_2,Theta_3;
    //finding whether the given triangle is obtuse or acute or rightangles triangle
    Theta_1=atan((slope_b-slope_a)/(1+(slope_b*slope_a)));
    if( Theta_1 < 0)
        Theta_1=Theta_1*(-1);

    Theta_2=atan((slope_c-slope_b)/(1+(slope_c*slope_b)));
    if( Theta_2 < 0)
        Theta_2=Theta_2*(-1);

    Theta_3=atan((slope_a-slope_c)/(1+(slope_a*slope_c)));
    if(Theta_3<0)
        Theta_3=Theta_3*(-1);

    if(Theta_1>90 || Theta_2>90 || Theta_3>90)
            printf("Obtuse angles triangle");
    else if(Theta_1==90 || Theta_2==90 || Theta_3==90)
            printf("Right angles triangle");
    else if(Theta_1<90 && Theta_2<90 && Theta_3<90)
            printf("AcuteS angles triangle");

}

int main()
{

    typeofTraingle(0,0,2,0,0,2); //Should print "Iscosceles"

    typeofTraingle(0,0,0,2,2,7); //Should print "Scalene"

    return 0;
}
