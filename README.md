#include <stdio.h>
#include <stdlib.h>
#define N 30
typedef struct student
{
    char Name[20];                         //姓名//
    long ID;                           //学号//
    int Score[6];                    //课程分数//
    int total;                            //总分//
}STU;
void inputscore(STU stu[],int num,int subject);
void ScoreSorting(STU stu[],int(*compare)(int a,int b),int num);
void NumSorting(STU stu[],int(*compare)(long int a,long int b),int num);
int Ascending(long int a,long int b);
int ascending(int a,int b);
int Descending(int a,int b);
int Total(STU stu[],int num,int i);
void input1(long int *pa,int limit1,int limit2);
void input2(int *pa,int limit1,int limit2);
void namesearch(STU stu[],int subject,int num);
void IDsearch(STU stu[],int num,int subject);
void namesort(STU stu[],int num,int subject);

int main()
{
    printf("Number:200111105\nSubject No.8\n\n");
    STU stu[N];
    float choice;
    double aver;
    char c;
    int choi,num,sign=0,i,j,sum,subject;
    RE:;                                            //若未选择退出，程序继续进行//
    printf("1.input record\n2.Calculate total and average score of every course\n3.Calculate total and average score of every student\n4.Sort in descending order by total score of every student \n5.Sort in ascending order by total score of every student \n6.Sort in ascending order by number\n7.Sorting in dictionary order by name\n8.Search by number\n9.Search by name\n10.Statistic analysis for every course\n11.List record\n12.Exit\n");
    printf("Please enter you choice:\n");
    scanf("%f",&choice);
    while((int)choice!=choice||choice<=0||choice>12)
    {
        while((c=getchar()!='\n'&&c!=EOF));
        printf("Invalid input!\n");
        printf("1.input record\n2.Calculate total and average score of every course\n3.Calculate total and average score of every student\n4.Sort in descending order by total score of every student \n5.Sort in ascending order by total score of every student \n6.Sort in ascending order by number\n7.Sorting in dictionary order by name\n8.Search by number\n9.Search by name\n10.Statistic analysis for every course\n11.List record\n12.Exit\n");
        printf("Please enter you choice:\n");
        scanf("%f",&choice);
    }
    choi=(int)choice;
    switch(choi)
    {
    case 1:                                                //录入每个学生的学号、姓名和考试成绩//
        {
            printf("The number of people is:\n");
            input2(&num,0,30);
            printf("The number of subject is:\n");
            input2(&subject,0,6);
            inputscore(stu,num,subject);
            sign++;
            break;
        }
    case 2:                                                //计算每门课程的总分和平均分//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            for(i=0;i<subject;i++)
            {
                sum=Total(stu,num,i);
                aver=(double)sum/num;
                printf("The average score of subject%d is %lf\n",i+1,aver);
                printf("The total score of subject%d is %d\n\n\n\n\n",i+1,sum);
            }
            break;
        }
    case 3:                                                //计算每个学生的总分和平均分//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            for(i=0;i<num;i++)
            {
                aver=(double)stu[i].total/subject;
                printf("The total score of ");
                puts(stu[i].Name);
                printf(" is %d\n",stu[i].total);
                printf("The average score of ");
                puts(stu[i].Name);
                printf(" is %lf\n\n",aver);
            }
            break;
        }
    case 4:                                                //按每个学生的总分降序排序//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            ScoreSorting(stu,Descending,num);
            printf("\tname\t\tnumber\t\t");
            for(i=0;i<subject;i++)
            {
                printf("subject%d\t\t",i+1);
            }
            printf("\n");
            for(i=0;i<num;i++)
            {
                printf("%8d. ",i+1);
                puts(stu[i].Name);
                printf("\t\t");
                printf("%8ld\t\t",stu[i].ID);
                for(j=0;j<subject;j++)
                {
                    printf("%8d\t",stu[i].Score[j]);
                }
                printf("\n");
            }
            printf("\n\n\n\n");
            break;
        }
    case 5:                                                 //按每个学生的总分升序排序//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            ScoreSorting(stu,ascending,num);
            printf("\tname\t\tnumber\t\t");
            for(i=0;i<subject;i++)
            {
                printf("subject%d\t\t",i+1);
            }
            printf("\n");
            for(i=0;i<num;i++)
            {
                puts(stu[i].Name);
                printf("\t\t");
                printf("%8ld\t\t",stu[i].ID);
                for(j=0;j<subject;j++)
                {
                    printf("%8d\t",stu[i].Score[j]);
                }
                printf("\n");
            }
            printf("\n\n\n\n");
            break;
        }
    case 6:                                           //按学号升序排序//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            NumSorting(stu,Ascending,num);
            printf("name\t\tnumber\t\t");
            for(i=0;i<subject;i++)
            {
                printf("subject%d\t\t",i+1);
            }
            printf("\n");
            for(i=0;i<num;i++)
            {
                puts(stu[i].Name);
                printf("\t\t");
                printf("%8ld\t\t",stu[i].ID);
                for(j=0;j<subject;j++)
                {
                    printf("%8d\t",stu[i].Score[j]);
                }
                printf("\n");
            }
            printf("\n\n\n\n");
            break;
        }
    case 7:                                //按姓名的字典顺序排出成绩表//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            namesort(stu,num,subject);
            break;
        }
    case 8:                                       //按学号查询学生排名及其考试成绩//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            IDsearch(stu,num,subject);
            break;
        }
    case 9:                                            //按姓名查询学生排名及考试成绩//
        {
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            namesearch(stu,subject,num);
            printf("\n\n");
            break;
        }
    case 10:                                  //按优秀（90-100分）、良好（80-89分）、中等（70-79分）、及格（60-69分）、不及格（0-59分），统计每个类别的人数及占比//
        {
            int a=0,b=0,c=0,d=0,e=0;
            float percent;
            if(sign==0)
            {
                printf("No data!\n\n");
                break;
            }
            for(i=0;i<subject;i++)
            {
                for(j=0;j<num;j++)
                {
                    if(stu[j].Score[i]>=90&&stu[j].Score[i]<=100)
                    {
                        a++;
                    }
                    else if(stu[j].Score[i]>=80&&stu[j].Score[i]<=89)
                    {
                        b++;
                    }
                    else if(stu[j].Score[i]>=70&&stu[j].Score[i]<=79)
                    {
                        c++;
                    }
                    else if(stu[j].Score[i]>=60&&stu[j].Score[i]<=69)
                    {
                        d++;
                    }
                    else e++;
                }
                percent=(float)a/num;
                printf("The number of excellent(90-100) in subject%d is %d\nThe percent is %f\n\n",i+1,a,percent);
                percent=(float)b/num;
                printf("The number of fine (80-89) in subject%d is %d\nThe mpercent is %f\n\n",i+1,b,percent);
                percent=(float)c/num;
                printf("The number of medium(70-79) in subject%d is %d\nThe percent is %f\n\n",i+1,c,percent);
                percent=(float)d/num;
                printf("The number of passing(60-69) in subject%d is %d\nThe percent is %f\n\n",i+1,d,percent);
                percent=(float)e/num;
                printf("The number of falling(0-59) in subject%d is %d\nThe percent is %f\n\n\n\n",i+1,e,percent);
            }
            break;
        }
    case 11:                                           //输出每个学生的学号、姓名、考试成绩以及课程总分和平均分//
        {
            if(sign==0)               //确认是否已录入数据//
            {
                printf("No data!\n");
                break;
            }
            printf("number\t\tscore\t\t");
            for(i=1;i<=subject;i++)
            {
                printf("subject%d\t\t",i);
            }
            printf("\n");
            for(i=0;i<num;i++)
            {
                puts(stu[i].Name);
                printf("\t\t");
                printf("%ld\t\t",stu[i].ID);
                for(j=0;j<subject;j++)
                {
                    printf("%8d\t\t",stu[i].Score[j]);
                }
                printf("\n");
            }
            printf("\n\n\n\n");
            break;
        }
    case 12:                      //结束程序//
        {
            return 0;
        }
    }
    goto RE;                  //程序重新开始//
}


void inputscore(STU stu[],int num,int subject)
{
    int i,j,k;
    char c;
    for(i=0;i<num;i++)
    {
        printf("Input the name:\n");
        c=getchar();
        fgets(stu[i].Name,sizeof(stu[i].Name),stdin);
        for(j=0;j<20;j++)                         //去掉回车//
        {
            if(stu[i].Name[j]=='\n')
            {
                stu[i].Name[j]='\0';
                break;
            }
        }
        printf("The ID is:\n");
        input1(&stu[i].ID,0,1000000);
        for(k=0;k<i;k++)              //防止输入相同学号//
        {
            while(stu[i].ID==stu[k].ID)
            {
                printf("Repititive number!\n");
                input1(&stu[i].ID,0,1000000);
                k--;
            }
        }
        for(j=0;j<subject;j++)
        {
            printf("The score of subject%d is:\n",j+1);
            input2(&stu[i].Score[j],0,100);
        }
        stu[i].total=0;
        for(j=0;j<subject;j++)
        {
            stu[i].total=stu[i].total+stu[i].Score[j];
        }
    }
    printf("All the data has ben input!\n\n\n\n");
}


void ScoreSorting(STU stu[],int(*compare)(int a,int b),int num)
{                                                  //根据总分对学生进行排序//
    int i,sign=1;
    STU temp;
    while(sign!=0)
    {
        sign=0;
        for(i=0;i<num-1;i++)
        {
            if((*compare)(stu[i].total,stu[i+1].total))
            {
                temp=stu[i];
                stu[i]=stu[i+1];
                stu[i+1]=temp;
                sign++;
            }
        }
    }
}
void NumSorting(STU stu[],int(*compare)(long int a,long int b),int num)
{                                                                 //根据学号进行排序//
    int i,sign=1;
    STU temp;
    while(sign!=0)
    {
        sign=0;
        for(i=0;i<num-1;i++)
        {
            if((*compare)(stu[i].ID,stu[i+1].ID))
            {
                temp=stu[i];
                stu[i]=stu[i+1];
                stu[i+1]=temp;
                sign++;
            }
        }
    }
}



int Ascending(long int a,long int b)          //升序排序//
{
    return a>b;
}


int ascending(int a,int b)                      //升序排序//
{
    return a>b;
}

int Descending(int a,int b)          //降序排序//
{
    return a<b;
}


int Total(STU stu[],int num,int i)             //总分求和//
{
    int n;
    long int sum=0;
    for(n=0;n<num;n++)
    {
        if(stu[n].Score[i]<0)
            break;
        sum=sum+stu[n].Score[i];
    }
    return sum;
}


void input1(long int *pa,int limit1,int limit2)          //输入函数,防护性措施，防止错误的输入引发程序运行异常，结果为长整型//
{
    char c;
    float algebra;
    scanf("%f",&algebra);
    while((int)algebra!=algebra||algebra<limit1||algebra>limit2)
    {
        printf("Wrong input!\n");
        while((c=getchar()!='\n'&&c!=EOF));
        scanf("%f",&algebra);
    }
    *pa=(long)algebra;
}


void input2(int *pa,int limit1,int limit2)          //输入函数,防护性措施，防止错误的输入引发程序运行异常,结果为整型//
{
    char c;
    float algebra;
    scanf("%f",&algebra);
    while((int)algebra!=algebra||algebra<limit1||algebra>limit2)
    {
        printf("Wrong input!\n");
        while((c=getchar()!='\n'&&c!=EOF));
        scanf("%f",&algebra);
    }
    *pa=(int)algebra;
}


void namesearch(STU stu[],int subject,int num)        //根据姓名搜索成绩//
{
    int i,j,sign=0;
    char name[20];
    char c;
    printf("Please input the name of student:\n");
    while((c=getchar()!='\n'&&c!=EOF));
    fgets(name,sizeof(name),stdin);
    for(i=0;name[i]!='\n'&&name[i]!='\0';i++)
    {
        if(name[i+1]=='\n')
        {
            name[i+1]='\0';
            break;
        }
    }
    for(i=0;i<num;i++)
    {
        if(strcmp(name,stu[i].Name)==0)
        {
            sign++;
            printf("The ID is %ld\n",stu[i].ID);
            for(j=0;j<subject;j++)
            {
                printf("The score of subject%d is %d\n",j+1,stu[i].Score[j]);
            }
        }
    }
    if(sign==0)
    {
        printf("The people do not exist!\n");
    }
}


void IDsearch(STU stu[],int num,int subject)                //根据学号查找个人成绩//
{
    int i,j,sign=0;
    long cod;
    char c;
    double code;
    printf("Please input the number of people:");
    scanf("%lf",&code);
    while((int)code!=code||code<0||code>10000000)
    {
        while((c=getchar()!='\n'&&c!=EOF));
        printf("Invalid input!\n");
        scanf("%lf",&code);
    }
    cod=(long)code;
    for(i=0;i<num;i++)
    {
        if(cod==stu[i].ID)
        {
            sign++;
            puts(stu[i].Name);
            printf("\n");
            for(j=0;j<subject;j++)
            {
                printf("The score of subject%d is %d\n",j+1,stu[i].Score[j]);
            }
            printf("\n\n");
            break;
        }
    }
    if(sign==0)
    {
        printf("Invalid ID!\n\n\n\n");
    }
}


void namesort(STU stu[],int num,int subject)          //根据姓名在字典里的顺序排序//
{
    int i,j,sign=1;
    STU temp;
    while(sign!=0)
    {
        sign=0;
        for(i=0;i<num-1;i++)
        {
            if(strcmp(stu[i+1].Name,stu[i].Name)<0)
            {
                temp=stu[i];
                stu[i]=stu[i+1];
                stu[i+1]=temp;
                sign++;
            }
        }
    }
    printf("name\t\tnumber\t\t");
    for(i=0;i<subject;i++)
    {
        printf("subject%d\t\t",i+1);
    }
    printf("\n\n");
    for(i=0;i<num;i++)
    {
        puts(stu[i].Name);
        printf("\t\t%8ld",stu[i].ID);
        for(j=0;j<subject;j++)
        {
            printf("\t\t%8d",stu[i].Score[j]);
        }
        printf("\n");
    }
}
