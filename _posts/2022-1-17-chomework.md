---
layout: post
title: "c语言程序设计--学生信息管理系统"
date:   2022-1-17
tags: [geek]
comments: true
author: yuexin02
---
这是我的大一上学期C语言程序设计课设。自己编写一个学生信息管理系统
# 运行环境
---
操作系统：Windows 10。
开发工具：Visual C++ 2010。
开发语言：C语言。
---
# 系统功能设计
---
根据分析，可将系统分为六大功能模块，主要包括密码登入模块、录入信息模块、查找记录模块、删除记录模块、记录显示模块、统计显示模块。
# 预处理模块和结构体
---
```
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#define LEN sizeof(struct student)
void mima();//密码系统函数
void save();//储存学生信息函数
void statistical();//统计学生信息函数
void find();//查找学生信息界面函数
void findname();//按名字查找学生信息函数
void findnum();//按学号查找学生信息函数
void clear();//删除学生信息函数
void show();//显示已存储信息函数
struct student//学生信息结构体
{
     int num;//学号
	 char name[10];//姓名
	 int age;//年龄
	 char gender[10];//性别
	 char political[10];//政治面貌
	 float c;//C语言成绩
	 float math;//数学成绩
	 float english;//英语成绩
	 float psychology; //心理成绩
	 float sum;//总分
};
struct student s[100];
```
 （我的结构体里面东西太多了，实际上可以减少点学生信息，接下来的显示函数的排版就可以方便很多。）
 # 主函数
 学生储存系统的主界面，也是与其他功能连接的平台。进入系统时会先调用密码函数，然后通过屏幕的指示对系统进一步操作。
 ```
int main()//主界面
{
	 mima();//调用密码函数，对学生信息进行保护
	 int n=0;
	 while(1)//循环可以进行多次操作
	     {
	                printf("********学生信息存储系统********\n");
			printf("************************************\n");
			printf("************************************\n");
			printf("************************************\n");
			printf("<<<<<<<<QWQ>>>>>>>>\n");
			printf("请按指示进行操作:\n");
			printf("********1.存储学生信息********\n");
			printf("********2.统计学生信息********\n");
			printf("********3.查找学生信息********\n");
			printf("********4.删除学生信息********\n");
			printf("********5.显示学生信息********\n");
			printf("********6.退出当前页面********\n");
			printf("<<<<<<<<QWQ>>>>>>>>\n");
			printf("请输入您的操作：");
			scanf("%d",&n);
			system("cls");
		switch(n)
			{
			      case 1:save();break;//储存学生信息
			      case 2:statistical();break;//统计学生信息
			      case 3:find();break;//查找学生信息
			      case 4:clear();break;//删除学生信息
			      case 5:show();break;//显示学生信息
			      case 6:exit(0);break;//退出程序
			      default:printf("输入错误了呦QAQ，重新试一下吧！\n");break;
			}
		}
			return 0;
}
```
这是一个很简单的主函数，我用了while语句确保可以多次执行操作再推出。
# 密码登入模块
此函数的作用是保护存储的学生信息。当第一次登入学生信息管理系统时，需要手动设置六位数字密码，以后每次登入系统都需要验证密码才可以对学生管理系统进行操作。
```
void mima()//密码系统
{
  	printf("********无敌的安全系统********\n");
printf("************************************\n");
	printf("************************************\n");
	printf("************************************\n");
  	printf("<<<<<<<<QWQ>>>>>>>>\n");
  	int mm=0,a=0;
	FILE *ap;
	ap=fopen("mima.txt","r+");//此文本用于储存密码
	fread(&mm,sizeof(int),1,ap);
	fclose(ap);
	if(mm==0)
   	{
	   	FILE *fp;
		fp=fopen("mima.txt","r+");
		printf("初次登陆，请设置六位数字密码：")
		scanf("%d",&mm);
		fwrite(&mm,sizeof(int),1,fp);
		system("cls");
		fclose(fp);
   	}
		FILE *fp;
		fp=fopen("mima.txt","r+");
		fread(&mm,sizeof(int),1,fp);
		printf("请输入密码:");
		scanf("%d",&a);
	if(a!=mm)
	{
		printf("密码错误!\n");
		exit(0);
	}
		fclose(fp);
}
```
一个很简单的函数，用一个文本文件来存储密码。
# 录入信息模板
 此函数用于存储学生的各项信息。包括学生学号、姓名、性别、政治面貌、年龄、C语言成绩、数学成绩、英语成绩、心理成绩及总分，同时可以选择一次性存储多个学生的信息。
 ```
void save()//存储学生信息
{
	printf("欢迎来到存储界面\n"); 
  	int n=0,i=0;
	FILE *ap;
	ap=fopen("student.txt","a+");
	printf("需要存储的学生人数：");
    scanf("%d",&n);
	system("cls");
	for(i=0;i<n;i++)
	{
		printf("输入第%d名学生的学号:",i+1);
		scanf("%d",&s[i].num );
                printf("输入第%d名学生的名字:",i+1);
		scanf("%s",s[i].name );
		printf("输入第%d名学生的年龄:",i+1);
		scanf("%d",&s[i].age );
		printf("输入第%d名学生的性别:",i+1);
		scanf("%s",s[i].gender );
		printf("输入第%d名学生的政治面貌:",i+1);
		scanf("%s",s[i].political );
		printf("输入第%d名学生的c语言成绩:",i+1);
		scanf("%f",&s[i].c );
		printf("输入第%d名学生的数学成绩:",i+1);
		scanf("%f",&s[i].math );
		printf("输入第%d名学生的英语成绩:",i+1);
		scanf("%f",&s[i].english );
		printf("输入第%d名学生的心理成绩:",i+1);
		scanf("%f",&s[i].psychology );
	        s[i].sum=s[i].c+s[i].math+s[i].english+s[i].psychology;
	}		
	for(i=0;i<n;i++)
	{
		fwrite(&s[i],sizeof(struct student),1,ap);
	}
		fclose(ap);
		printf("输入成功！\n");
}
```
我用了另外一个文本文档来存储学生信息，一个简单的for语句保证可以一次存储多个学生信息，第二个for语句将每个学生的信息写入文本文档。
# 查找学生信息模块
查找记录模块分为三个函数，其中find（）是查找学生信息的界面，输入1可以调用findnum（）函数，按学生的学号进行查找，输入2可以调用findname（）函数，可以按学生名字进行查找。
```
void find()//查找学生信息界面
{
    int n;
	printf("**********欢迎来到查找界面**********\n");
	printf("************************************\n");
	printf("************************************\n");
	printf("************************************\n");
	printf("请选择您想要查找的方式：\n");
	printf("1.按学号查找\n");
	printf("2.按姓名查找\n");
	printf("请输入您的操作:");
	scanf("%d",&n);
 switch(n)
 {
	case 1:findnum();break;//按学号查找
	case 2:findname();break;//按姓名查找
	case 3:exit(0);break;
 }
}
void findnum()//按学号查找
{
	int n=0,i=0,j=0;
	FILE *fp;
	fp=fopen("student.txt","r+");
	printf("请输入学生学号:");
	scanf("%d",&n);
 while(fread(&s[i],sizeof(struct student),1,fp))
	i++;
 for(j=0;j<i;j++)
 if(s[j].num==n)
	printf("学号 %d ,名字 %s ,年龄 %d ,性别 %s ,政治面貌 %s ,c语言成绩 %.2f ,数学成绩 %f ,英语成绩 %.2f ,心理成绩 %.2f ,总分 %.2f\n",
s[j].num,s[j].name,s[j].age,s[j].gender,s[j].political,s[j].c,s[j].math,s[j].english,s[j].psychology,s[j].sum);
	fclose(fp);
 }
void findname()//按名字查找
{
	int i=0,j=0;
	char ch[20];
	FILE *fp;
	fp=fopen("student.txt","r+");
	printf("请输入学生姓名：");
	scanf("%s",ch);
  while(fread(&s[i],sizeof(struct student),1,fp))
        i++;
  for(j=0;j<i;j++)
  if(strcmp(s[j].name,ch)==0)
         printf("学号 %d ,名字 %s ,年龄 %d ,性别 %s ,政治面貌 %s ,c语言成绩 %.2f ,数学成绩 %.2f ,英语成绩 %.2f ,心理成绩 %.2f ,总分 %.2f\n",
         s[j].num,s[j].name,s[j].age,s[j].gender,s[j].political,s[j].c,s[j].math,s[j].english,s[j].psychology,s[j].sum);
      fclose(fp);
}
```
都是采用了读取文件然后将各个学生信息与查找的信息用佛如语句一一比对，然后输出所要找的学生的全部信息。
# 删除记录模块
此函数可以根据输入的学号与存储的学生信息进行比对，如何确认删除学生信息。
```
void clear()//删除学生信息
{
	show();//显示当前已存储的学生信息
	int n=0,i=0,j=0,m=0,k=0;
	FILE *fp;
	fp=fopen("student.txt","r+");
	printf("**********欢迎来到删除界面**********\n");
	printf("************************************\n");
	printf("************************************\n");
	printf("************************************\n");
	printf("请输入您想要删除学生的学号：");
	scanf("%d",&n);
 while(fread(&s[i],sizeof(struct student),1,fp))
       i++;
	fclose(fp);
 for(j=0;j<i;j++)
 if(s[j].num==n)
   {
     printf("学号 %d ,名字 %s ,年龄 %d ,性别 %s ,政治面貌 %s ,c语言成绩 %1.1f ,数学成绩 %1.1f ,英语成绩 %1.1f ,心理成绩 %1.1f ,总分 %1.1f\n",
     s[j].num,s[j].name,s[j].age,s[j].gender,s[j].political,s[j].c,s[j].math,s[j].english,s[j].psychology,s[j].sum);
     k=j;
    }
	printf("是否删除该学生信息\n");
	printf("********(o_0)???********\n");
	printf("1.取消操作\n");
	printf("2.确认删除\n");
	printf("请您选择：");
	scanf("%d",&m);
    if(m==1)
	   exit(0);
 	for(k;k<i-1;k++)
	{
		s[k].num ==s[k+1].num;
		s[k].name==s[k+1].name;
	        s[k].age==s[k+1].age;
		s[k].gender==s[k+1].gender;
		s[k].political==s[k+1].political;
		s[k].c==s[k+1].c;
		s[k].math==s[k+1].math;
		s[k].english==s[k+1].english;
		s[k].psychology==s[k+1].psychology;
		s[k].sum==s[k+1].sum;
	}
		fp=fopen("student.txt","w");
	for(k=0;k<i-1;k++)
		fwrite(&s[k],LEN,1,fp);
		fclose(fp);
		printf("删除成功！\n");
}
原理与查找大致相同，删除实现的方法是找到所要删除学生的位置，用后面的学生挤掉他的位置，从而达到删除的效果。
# 记录显示模块
此函数能显示已记录的学生的全部信息。
void show()//显示已经存储的学生信息
{
	int i=0,j=0; 
	printf("**********欢迎来到显示界面**********\n");
	printf("************************************\n");
	printf("************************************\n");
	FILE *fp;
	fp=fopen("student.txt","r+");
 while(fread(&s[i],sizeof(struct student),1,fp))
       i++;
	printf("%d名学生信息显示如下:\n",i);
 for(j=0;j<i;j++)
     printf(“学号 %d ,名字 %s ,年龄 %d ,性别 %s ,政治面貌 %s ,c语言成绩 %1.1f ,数学成绩 %1.1f ,英语成绩 %1.1f ,心理成绩 %1.1f ,总分 %1.1f\n”,
     s[j].num,s[j].name,s[j].age,s[j].gender,s[j].political,s[j].c,s[j].math,s[j].english,s[j].psychology,s[j].sum);
 fclose(fp); 
}
```
读取文本内容然后将学生信息一一显示。
# 统计显示模块
此函数能统计录入的学生数量，并且显示C语言、数学、英语、心理、语文、总分最高分的分数和姓名。
```
void statistical()//统计学生信息
{ 
	 printf("**********欢迎来到统计界面**********\n");
	 printf("************************************\n");
	 printf("************************************\n");
	 printf("************************************\n");
	 printf("*******(-_-)******\n");
	FILE *fp;
	fp=fopen("student.txt","r+");
	int i=0,j=0,max_num=0,max_c=0,max_english=0,max_math=0,max_psychology=0;
	char n[20],m[20];
	while(fread(&s[i],sizeof(struct student),1,fp))
		  i++;
		  printf("共存储了%d名学生\n",i);
		  fclose(fp);
 for(j=0;j<i;j++)
 if(s[j].sum>max_num)
   {
		max_num=s[j].sum;
		strcpy(n,s[j].name);
   }
	printf("总分最高分为");
	puts(n);
	printf("%d分\n",max_num);
 for(j=0;j<i;j++)
 if(s[j].c >max_c)
   {
		max_c=s[j].c;
		strcpy(n,s[j].name);
   }
	printf("c语言最高分为");
	puts(n);
	printf("%d分\n",max_c);
 for(j=0;j<i;j++)
 if(s[j].english>max_english)
   {
		max_english=s[j].english;
		strcpy(n,s[j].name);
   }
   printf("英语分数最高为");
   puts(n);
   printf("%d分\n",max_english);
 for(j=0;j<i;j++)
 if(s[j].math>max_math)
   {
		max_math=s[j].math;
		strcpy(n,s[j].name);
   }
    printf("数学分数最高为");
    puts(n);
    printf("%d分\n",max_math);
 for(j=0;j<i;j++)
 if(s[j].psychology>max_psychology)
   {
		max_psychology=s[j].psychology;
		strcpy(n,s[j].name);
   }
    printf("心理分数最高为");
    puts(n);
    printf("%d分\n",max_psychology);
}
```
# 心得体会
自主学习获得的知识是刻骨铭心的。独立思考的过程虽然困难但是我仍乐在其中。也在学习交流的过程中结识了许多好友，希望未来能学到更多，收获更多。



