# Egyptian-Fraction-https-www.cs.scranton.edu-mccloske-hs_prog_contest-contest_problems-probs_07_h

//Egyptian Fraction
#include<stdio.h>
typedef struct Egyptian_Number
{
int len;
int den[100];
int sum_num;
int sum_den;
}eg_num;
int input_number()
{
int n = 0;
while(n < 1)
{
printf("Enter a positive value :");
scanf("%d",&n);
}
return n;
}
void input_n(int n,eg_num arr[n])
{
for(int i=0;i<n;i++)
{
printf("Enter the number of unit fractions :\n");
arr[i].len = input_number();
printf("Enter %d positive integers :\n",arr[i].len);
for(int j=0;j<arr[i].len;j++)
{
arr[i].den[j] = input_number();
}
arr[i].sum_num = 0;
arr[i].sum_den = 1;
}
}
eg_num input_one()
{
eg_num instance;
printf("Enter the number of unit fractions :\n");
instance.len = input_number();
printf("Enter %d positive integers : \n",instance.len);
for(int i=0;i<instance.len;i++)
{
instance.den[i] = input_number();
}
instance.sum_num = 0;
instance.sum_den = 1;
return instance;
}
int gcd(int a, int b)
{
if(a == 0)
return b;
return gcd(b%a, a);
}
void Compute_n(int n, eg_num arr[n])
{
int g;
for(int i=0;i<n;i++)
{
for(int j=0;j<arr[i].len;j++)
{
arr[i].sum_num = arr[i].den[j] * arr[i].sum_num + arr[i].sum_den;
arr[i].sum_den *= arr[i].den[j];
g = gcd(arr[i].sum_num,arr[i].sum_den);
arr[i].sum_num /= g;
arr[i].sum_den /= g;
}
}
}
eg_num Compute_one(eg_num instance)
{
int g;
for(int i=0;i<instance.len;i++)
{
instance.sum_num = instance.den[i] * instance.sum_num +
instance.sum_den;
instance.sum_den *= instance.den[i];
g = gcd( instance.sum_num, instance.sum_den );
instance.sum_num /= g;
instance.sum_den /= g;
}
return instance;
}
void Display_n(int n, eg_num arr[n])
{
for(int i=0;i<n;i++)
{
printf("1/%d ",arr[i].den[0]);
for(int j=1;j<arr[i].len;j++)
{
printf(" + 1/%d ",arr[i].den[j]);
}
printf("= %d/%d \n",arr[i].sum_num,arr[i].sum_den);
}
}
void Display_one( eg_num instance )
{
printf(" 1/%d ",instance.den[0]);
for(int i=1;i<instance.len;i++)
{
printf("+ 1/%d ",instance.den[i]);
}
printf(" = %d/%d \n",instance.sum_num,instance.sum_den);
}
int menu()
{
int choice = 0;
while(choice != 1 && choice != 2)
{
printf("Enter 1 or 2 :\n");
printf("Enter 1 for one Egyptian Number\n");
printf("Enter 2 for 'n' number of Egyptian Numbers\n");
scanf("%d",&choice);
}
return choice;
}
int main()
{
int n;
int choice = 0;
choice = menu();
if(choice == 1)
{
eg_num instance;
instance = input_one();
instance = Compute_one(instance);
Display_one(instance);
}
else if ( choice == 2)
{
printf("Enter the number of instances :");
n = input_number();
eg_num arr[n];
input_n(n,arr);
Compute_n(n,arr);
Display_n(n, arr);
}
return 0;
}
