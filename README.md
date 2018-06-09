#include <stdio.h>
#include <string.h>
#define N 30
#define M 15 
int ReadScore(long num[],char name[][M],int score[]);    //读入每个学生的学号、姓名、成绩 
void ScoreSort21(int score[],long num[],char[][M],int n);//按成绩由高到低排出名次表 
int main()
{
	long num[N];
	char name[N][M];
	int score[N];
	int n = ReadScore(num,name,score);
	ScoreSort21(score,num,name,n);
	return 0;
}
ReadScore(long num[],char name[][M],int score[])//定义了三个数组分别存放学生的学号姓名成绩 
{
	int i = -1; 
	//定义i = -1使do while循环从下标从0开始存入到对应的数组中
	do{
		i++;
		printf("Input ID、score and name:");
		scanf("%d%ld",&num[i],&score[i]);
    gets(name[i]);
 // 或者用scanf("%s",name[i]);getchar();
 //而使用fgets(name[i],sizeof(name[i]),stdin);不会读走缓冲区的回车符，并且用getchar（）也不行，最后输出的姓名还是会单独占一行
		//用fgets可以限制输入字符串长度不超过name数组的大小 
	}while(score[i] >= 0 && num[i] > 0 && i < 30);//成绩大于等于0，学号大于0，人数不超过30则执行循环 
//	printf("i = %d\n",i);
	return i;//返回学生总数
}
void ScoreSort21(int score[],long num[],char name[][M],int n)
{
	int i,j,a,b,temp1,temp2;
	char temp[M];
	for(i = 0;i < n;i++);
	{
		a = i;
		for(j = i + 1;j < n;j++)
		{
			if(score[j] > score[i])
			a = j;
		}
		if(a != i)
		{
			temp1 = score[a];
			score[a] = score[i];
			score[i] = temp1;
			temp2 = num[a];
			num[a] = num[i];
			num[i] = temp2;
			strcpy(temp,name[a]);
			strcpy(name[a],name[j]);
			strcpy(name[j],temp);
		}
	}
	printf("姓名 学号 成绩\n"); 
	for(b = 0;b < n;b++)
	{
		printf("%s\t%ld\t%4d\n",name[b],num[b],score[b]);
	}
	printf("\n\n");
}
