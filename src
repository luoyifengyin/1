#include <iostream>
#include <stdlib.h>
#include <windows.h>
#include <conio.h>
#include <time.h>
#include <ctype.h>
#include <string.h>
#include <algorithm>
using namespace std;
void gotoxy(int x, int y)
{
	CONSOLE_SCREEN_BUFFER_INFO cs;
	HANDLE hConsoleOut = GetStdHandle(STD_OUTPUT_HANDLE);
	GetConsoleScreenBufferInfo(hConsoleOut, &cs);
	cs.dwCursorPosition.X = y;
	cs.dwCursorPosition.Y = x;
	SetConsoleCursorPosition(hConsoleOut,
		cs.dwCursorPosition);
}
typedef struct date
{
	int year;
	int month;
	int day;
}DAT;
typedef struct student
{
	long long studentID;
	char name[13];
	char sex;
	DAT birthday;
	double score[4];
}STUDENT;
STUDENT stu[100];
void Printstu(int num, int n)
{
	printf("学号\t\t姓名\t\t性别\t出生日期\t数学成绩 英语成绩 程序成绩     总分\n");
	for (int i = num; n--; i++)
	{
		printf("%-13lld\t%-13s\t%c\t%4d-%02d-%02d\t", stu[i].studentID,
			stu[i].name, stu[i].sex,
			stu[i].birthday.year, stu[i].birthday.month, stu[i].birthday.day);
		for (int j = 0; j < 4; j++)
			printf("%8g ", stu[i].score[j]);
		putchar('\n');
	}
	return;
}
int Read(STUDENT stu[], FILE *fp, int n)
{
	int i, j;
	char ch;
	for (i = n;;)
	{
		system("cls");
		gotoxy(0, 0);
		if (i >= 100)
		{
			printf("学生学籍信息库人数已满，无法添加\n");
			printf("按任意键返回学生学籍管理系统\n");
			getch();
			return i;
		}
		printf("请输入学号: ");
		int flag = 1;
		while (flag)
		{
			if (!scanf("%lld", &stu[i].studentID) || stu[i].studentID < 0)
			{
				while (getchar() != '\n');
				printf("输入信息错误\n");
				printf("请重新输入学号: ");
				continue;
			}
			for (flag = j = 0; j < i && !flag; j++)
			{
				if (stu[i].studentID == stu[j].studentID)
				{
					printf("此学号已存在\n");
					printf("请重新输入学号: ");
					flag++;
				}
			}
		}
		printf("请输入姓名: ");
		scanf_s("%s", stu[i].name, 13);
		printf("请输入性别(M/F): ");
		scanf(" %c", &stu[i].sex);
		stu[i].sex = toupper(stu[i].sex);
		while (stu[i].sex != 'M' && stu[i].sex != 'F')
		{
			while (getchar() != '\n');
			printf("输入信息错误\n");
			printf("请重新输入性别: ");
			scanf(" %c", &stu[i].sex);
			stu[i].sex = toupper(stu[i].sex);
		}
		printf("请输入出生年月日(XXXX-XX-XX): ");
		while (scanf("%d%*c%d%*c%d", &stu[i].birthday.year, &stu[i].birthday.month, &stu[i].birthday.day) != 3)
		{
			while (getchar() != '\n');
			printf("输入信息错误\n");
			printf("请重新输入出生日期(XXXX-XX-XX): ");
		}
		char subject[3][5] = { "数学","英语","程序" };
		double sum = 0;
		for (j = 0; j < 3; j++)
		{
			printf("请输入%s成绩: ", subject[j]);
			while (!scanf("%lf", &stu[i].score[j]) || stu[i].score[j] < 0)
			{
				while (getchar() != '\n');
				printf("输入信息错误\n");
				printf("请重新输入%s成绩: ", subject[j]);
			}
			sum += stu[i].score[j];
		}
		stu[i].score[3] = sum;
		Printstu(i, 1);
		printf("是否确认添加此学生学籍信息？(Y/N)\n");
		do {
			ch = getch();
			switch (ch)
			{
			case 'Y':
			case 'y': fprintf(fp, "%lld%13s%3c%6d-%02d-%02d", stu[i].studentID,
				stu[i].name, stu[i].sex,
				stu[i].birthday.year, stu[i].birthday.month, stu[i].birthday.day);
				for (int j = 0; j < 4; j++)
					fprintf(fp, " %6g", stu[i].score[j]);
				fputc('\n', fp);
				printf("添加成功\n");
				i++; break;
			case 'N':
			case 'n': printf("添加失败\n"); break;
			default: ch = 0;
			}
		} while (!ch);
		printf("是否继续添加学生学籍信息？\n");
		printf("按空格或回车键继续添加\n");
		printf("按ESC键返回学生学籍管理系统\n");
		while (1)
		{
			ch = getch();
			if (ch == 27) return i;
			else if (ch == ' ' || ch == '\r' || ch == '\n') break;
		}
	}
	return i;
}
bool cmpID(STUDENT a, STUDENT b)
{
	return a.studentID < b.studentID;
}
bool cmpbirth(STUDENT a, STUDENT b)
{
	return a.birthday.year < b.birthday.year ||
		a.birthday.month < b.birthday.month ||
		a.birthday.day < b.birthday.day;
}
bool cmpmath(STUDENT a, STUDENT b)
{
	return a.score[0] > b.score[0];
}
bool cmpENG(STUDENT a, STUDENT b)
{
	return a.score[1] > b.score[1];
}
bool cmppgm(STUDENT a, STUDENT b)
{
	return a.score[2] > b.score[2];
}
bool cmpscore(STUDENT a, STUDENT b)
{
	return a.score[3] > b.score[3];
}
void PrintInfo(STUDENT stu[], int n)
{
	system("cls");
	gotoxy(0, 0);
	if (!n)
	{
		printf("暂没有学生学籍信息进行登记\n\n");
		printf("按任意键返回学生学籍管理系统\n");
		getch();
		return;
	}
	int i;
	char str[6][9] = { "学号","出生日期","数学成绩","英语成绩","程序成绩","总分" };
	for (i = 0; i < 6; i++)
		printf("%d.按%s顺序显示\n", i + 1, str[i]);
	printf("请输入对应数字实现以上功能\n");
	char ch;
	do {
		ch = getch();
		switch (ch)
		{
		case '1': sort(stu, stu + n, cmpID); break;
		case '2': sort(stu, stu + n, cmpbirth); break;
		case '3': sort(stu, stu + n, cmpmath); break;
		case '4': sort(stu, stu + n, cmpENG); break;
		case '5': sort(stu, stu + n, cmppgm); break;
		case '6': sort(stu, stu + n, cmpscore); break;
		default: ch = 0;
		}
	} while (!ch);
	system("cls");
	gotoxy(0, 0);
	Printstu(0, n);
	printf("共有%d条记录\n", n);
	printf("按任意键返回学生学籍管理系统\n");
	getch();
	return;
}
FILE* Modify(FILE *fp, int num, int len)
{
	char ch, str[7][9] = { "学号","姓名","性别","出生日期","数学成绩","英语成绩","程序成绩" }, reply;
	long long ID;
	char name[13], sex;
	int birth[3], i;
	double score = 0, sum;
	printf("是否确认修改该学生学籍信息？\n");
	printf("Y/y:确认\tN/n:取消");
	do {
		reply = getch();
		reply = toupper(reply);
		if (reply == 'N') return fp;
	} while (reply != 'Y');
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("请输入以下需要修改的部分\n");
		for (i = 0; i < 4; i++)
			printf("%d.%s\n", i + 1, str[i]);
		printf("5.成绩\n");
		do ch = getch(); while (!('1' <= ch && ch <= '5'));
		char kb = 0;
		system("cls");
		gotoxy(0, 0);
		ch -= '1';
		if (ch == 4)
		{
			for (i = 4; i <= 6; i++)
				printf("%d.%s\n", i - 3, str[i]);
			do {
				kb = getch();
				kb -= '1';
			} while (!(0 <= kb && kb <= 2));
			system("cls");
			gotoxy(0, 0);
		}
		printf("原%s: ", str[ch + kb]);
		switch (ch)
		{
		case 0: printf("%lld", stu[num].studentID); break;
		case 1: printf("%s", stu[num].name); break;
		case 2: printf("%c", stu[num].sex); break;
		case 3: printf("%d-%02d-%02d\n", stu[num].birthday.year,
			stu[num].birthday.month, stu[num].birthday.day); break;
		case 4: printf("%g", stu[num].score[kb]);
		}
		if (ch != 3) printf("\n请输入新的%s: ", str[ch + kb]);
		switch (ch)
		{
		case 0:
		{
			int flag = 1;
			while (flag)
			{
				if (!scanf("%lld", &ID) || ID < 0)
				{
					while (getchar() != '\n');
					printf("输入信息错误\n");
					printf("请重新输入学号: ");
					continue;
				}
				for (flag = i = 0; i < len && !flag; i++)
				{
					if (ID == stu[i].studentID  && i != num)
					{
						printf("此学号已存在\n");
						printf("请重新输入学号: ");
						flag++;
					}
				}
			}
			break;
		}
		case 1: scanf_s("%s", name, 13); break;
		case 2:
			scanf(" %c", &sex);
			sex = toupper(sex);
			while (sex != 'M' && sex != 'F')
			{
				while (getchar() != '\n');
				printf("输入信息错误\n");
				printf("请重新输入性别(M/F): ");
				scanf(" %c", &sex);
				sex = toupper(sex);
			}
			break;
		case 3:
		{
			char msg[3][5] = { "年份","月份","日" };
			for (i = 0; i < 3; i++)
			{
				printf("请输入新的出生%s: ", msg[i]);
				while (!scanf("%d", &birth[i]))
				{
					while (getchar() != '\n');
					printf("输入信息错误\n");
					printf("请重新输入出生%s: ", msg[i]);
				}
			}
			break;
		}
		case 4:
			for (sum = i = 0; i < 3; i++)
			{
				while (i == kb && (!scanf("%lf", &score) || score < 0))
				{
					while (getchar() != '\n');
					printf("输入信息错误\n");
					printf("请重新输入%s: ", str[ch + kb]);
				}
				if (i != kb) sum += stu[num].score[i];
				else sum += score;
			}
		}
		printf("是否确定修改？(Y/N)\n");
		do {
			reply = getch();
			reply = toupper(reply);
		} while (reply != 'Y' && reply != 'N');
		if (reply == 'Y')
		{
			switch (ch)
			{
			case 0: stu[num].studentID = ID; break;
			case 1: strcpy(stu[num].name, name); break;
			case 2: stu[num].sex = sex; break;
			case 3: stu[num].birthday.year = birth[0];
				stu[num].birthday.month = birth[1];
				stu[num].birthday.day = birth[2];
				break;
			case 4: stu[num].score[kb] = score;
				stu[num].score[3] = sum;
			}
			fclose(fp);
			if ((fp = fopen("Student Status Information.txt", "w")) == NULL)
			{
				printf("Failure to open Student Status Information.txt!\n");
				exit(2);
			}
			for (int i = 0; i < len; i++)
			{
				fprintf(fp, "%lld%13s%3c%6d-%02d-%02d", stu[i].studentID,
					stu[i].name, stu[i].sex,
					stu[i].birthday.year, stu[i].birthday.month, stu[i].birthday.day);
				for (int j = 0; j < 4; j++)
					fprintf(fp, " %6g", stu[i].score[j]);
				fputc('\n', fp);
			}
			printf("修改成功\n");
			Printstu(num, 1);
		}
		else printf("修改失败\n");
		printf("是否继续进行修改？(Y/N)\n");
		do {
			reply = getch();
			reply = toupper(reply);
			if (reply == 'N') return fp;
		} while (reply != 'Y');
	}
}
FILE* Delete(FILE *fp, int num, int &len)
{
	char reply;
	printf("是否确认删除该学生学籍信息？\n");
	printf("Y/y:确认\tN/n:取消");
	do {
		reply = getch();
		reply = toupper(reply);
		if (reply == 'N') return fp;
	} while (reply != 'Y');
	swap(stu[num], stu[len]);
	len--;
	fclose(fp);
	if ((fp = fopen("Student Status Information.txt", "w")) == NULL)
	{
		printf("Failure to open Student Status Information.txt!\n");
		exit(3);
	}
	for (int i = 0; i < len; i++)
	{
		fprintf(fp, "%lld%13s%3c%6d-%02d-%02d", stu[i].studentID,
			stu[i].name, stu[i].sex,
			stu[i].birthday.year, stu[i].birthday.month, stu[i].birthday.day);
		for (int j = 0; j < 4; j++)
			fprintf(fp, " %6g", stu[i].score[j]);
		fputc('\n', fp);
	}
	printf("删除成功\n");
	printf("按任意键返回\n");
	getch();
	return fp;
}
int SearchStudentID(int len)
{
	system("cls");
	gotoxy(0, 0);
	long long ID;
	printf("请输入学号: ");
	while (!scanf("%lld", &ID) || ID < 0)
	{
		while (getchar() != '\n');
		printf("输入信息错误\n");
		printf("请重新输入学号: ");
	}
	int low = 0, high = len - 1, mid;
	while (low <= high)
	{
		mid = low + (high - low) / 2;
		if (ID > stu[mid].studentID) low = mid + 1;
		else if (ID < stu[mid].studentID) high = mid - 1;
		else return mid;
	}
	return -1;
}
int SearchName(int search[], int &n)
{
	system("cls");
	gotoxy(0, 0);
	char name[13];
	printf("请输入姓名: ");
	scanf_s("%s", name, 13);
	int k = 0;
	for (int i = 0; i < n; i++)
	{
		if (!strcmp(name, stu[search[i]].name))
			search[k++] = search[i];
	}
	n = k;
	return 2;
}
int SearchSex(int search[], int &n)
{
	system("cls");
	gotoxy(0, 0);
	char sex;
	printf("请输入性别(M/F): ");
	scanf(" %c", &sex);
	sex = toupper(sex);
	while (sex != 'M' && sex != 'F')
	{
		while (getchar() != '\n');
		printf("输入信息错误\n");
		printf("请重新输入性别: ");
		scanf(" %c", &sex);
		sex = toupper(sex);
	}
	int k = 0;
	for (int i = 0; i < n; i++)
	{
		if (sex == stu[search[i]].sex)
			search[k++] = search[i];
	}
	n = k;
	return 4;
}
int SearchBirth(int search[], int &n, int &m)
{
	system("cls");
	gotoxy(0, 0);
	int i, j, birth;
	char ch, str[3][5] = { "年份","月份","日" };
	for (i = 0, j = 1; i < 3; i++)
	{
		if (!(m & (1 << i)))
			printf("%d.按出生%s查找\n", j++, str[i]);
	}
	printf("请输入对应数字实现以上功能\n");
	do {
		ch = getch(); ch -= '1';
		for (i = 0; i < 3 && ch >= i; i++)
			if (m >> i & 1) ch++;
	} while (!(0 <= ch && ch < 3));
	system("cls");
	gotoxy(0, 0);
	printf("请输入出生%s: ", str[ch]);
	while (!scanf("%d", &birth))
	{
		while (getchar() != '\n');
		printf("输入信息错误\n");
		printf("请重新输入出生%s: ", str[ch]);
	}
	int k = 0;
	for (i = 0; i < n; i++)
	{
		if ((ch == 0 && birth == stu[search[i]].birthday.year) ||
			(ch == 1 && birth == stu[search[i]].birthday.month) ||
			(ch == 2 && birth == stu[search[i]].birthday.day))
			search[k++] = search[i];
	}
	n = k; m += 1 << ch;
	if (m < 7) return 0;
	return 8;
}
int SearchScore(int search[], int &n)
{
	double low, high;
	int i, j, k;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		char ch, str[4][9] = { "数学成绩","英语成绩","程序成绩","总分" };
		for (i = 0; i < 4; i++)
			printf("%d.按%s查找\n", i + 1, str[i]);
		printf("请输入对应数字实现以上功能\n");
		do {
			ch = getch();
			ch -= '1';
		} while (!(0 <= ch && ch < 4));
		system("cls");
		gotoxy(0, 0);
		printf("你选择了%s\n", str[ch]);
		printf("筛选范围大于等于: ");
		while (!scanf("%lf", &low))
		{
			while (getchar() != '\n');
			printf("输入数据错误\n");
			printf("请重新输入%s: ", str[ch]);
		}
		printf("筛选范围小于等于: ");
		while (!scanf("%lf", &high) || high < low)
		{
			while (getchar() != '\n');
			printf("输入数据错误\n");
			printf("请重新输入%s: ", str[ch]);
		}
		for (i = 0; i < n;)
		{
			if (stu[search[i]].score[ch] < low || stu[search[i]].score[ch] > high)
			{
				if (i == n - 1) { n--; break; }
				search[i] = search[n - 1];
				n--; continue;
			}
			i++;
		}
		for (i = 0; i < n - 1; i++)
		{
			for (k = i, j = i - 1; j < n; j++)
			{
				if (stu[search[i]].score[ch] < stu[search[i]].score[ch])
					k = j;
			}
			if (k != i)
				swap(search[i], search[k]);
		}
		if (n)
		{
			system("cls");
			gotoxy(0, 0);
			printf("学号\t\t姓名\t\t性别\t出生日期\t数学成绩 英语成绩 程序成绩     总分\n");
			for (i = 0; i < n; i++)
			{
				printf("%-13lld\t%-13s\t%c\t%4d-%02d-%02d\t", stu[search[i]].studentID,
					stu[search[i]].name, stu[search[i]].sex,
					stu[search[i]].birthday.year, stu[search[i]].birthday.month, stu[search[i]].birthday.day);
				for (j = 0; j < 4; j++)
					printf("%8g ", stu[search[i]].score[j]);
				putchar('\n');
			}
		}
		if (n == 1) return 1;
		if (!n) return 0;
		printf("是否以成绩继续筛选?(Y/N)\n");
		do {
			ch = getch();
			ch = toupper(ch);
			if (ch == 'N') return 1;
		} while (ch != 'Y');
	}
}
void Search(STUDENT stu[], int len, FILE *fp)
{
	sort(stu, stu + len, cmpID);
	int search[100], i, j, n;
	char ch, str[4][9] = { "学号","姓名","性别","出生日期" };
	while (1)
	{
		for (n = 0; n < len; n++) search[n] = n;
		int flag = 0, m = 0, ret = 0;
		system("cls");
		gotoxy(0, 0);
		while (1)
		{
			for (i = 0, j = 1; i < 4; i++)
			{
				if (!(flag & (1 << i)))
					printf("%d.按%s查找\n", j++, str[i]);
			}
			printf("%d.按成绩查找\n", j);
			printf("请输入对应数字实现以上功能\n");
			printf("按ESC键返回学生学籍管理系统\n");
			ret = 0;
			do {
				ch = getch();
				if (ch == 27) return;
				ch -= '0';
				for (i = 0; i < 4 && ch > i; i++)
					if (flag >> i & 1) ch++;
				switch (ch)
				{
				case 1: if ((search[0] = SearchStudentID(len)) < 0) n = 0;
						  else n = 1;
						  break;
				case 2: flag += SearchName(search, n); break;
				case 3: flag += SearchSex(search, n); break;
				case 4: flag += SearchBirth(search, n, m); break;
				case 5: ret = SearchScore(search, n); break;
				default: ch = 0;
				}
			} while (!ch);
			if (n && !ret)
			{
				if (ch == 1) n = 1;
				system("cls");
				gotoxy(0, 0);
				printf("学号\t\t姓名\t\t性别\t出生日期\t数学成绩 英语成绩 程序成绩     总分\n");
				for (i = 0; i < n; i++)
				{
					printf("%-13lld\t%-13s\t%c\t%4d-%02d-%02d\t", stu[search[i]].studentID,
						stu[search[i]].name, stu[search[i]].sex,
						stu[search[i]].birthday.year, stu[search[i]].birthday.month, stu[search[i]].birthday.day);
					for (j = 0; j < 4; j++)
						printf("%8g ", stu[search[i]].score[j]);
					putchar('\n');
				}
			}
			else if (!ret)
			{
				printf("找不到相关信息\n");
				printf("按任意键返回搜索界面\n");
				while (!kbhit()); getch();
				break;
			}
			if (n == 1)
			{
				printf("\n可以输入对应数字实现以下功能\n");
				printf("1.修改该学生学籍信息\n");
				printf("2.删除该学生学籍信息\n");
				printf("按ESC键返回搜索界面\n");
				do ch = getch(); while (ch != '1' && ch != '2' && ch != 27);
				if (ch == '1') Modify(fp, search[0], len);
				else if (ch == '2') Delete(fp, search[0], len);
				break;
			}
			else
			{
				printf("是否在此范围内继续查找？\n");
				printf("Y/y:继续查找\n");
				printf("N/n:返回搜索界面\n\n");
				do {
					ch = getch();
					ch = toupper(ch);
					if (ch != 'Y' && ch != 'N') ch = 0;
				} while (!ch);
				if (ch == 'N') break;
			}
		}
	}
	return;
}
void StudentStatusInformation()
{
	FILE *fp;
	int n = 0;
	fp = fopen("Student Status Information.txt", "r+");
	if (fp == NULL)
	{
		if ((fp = fopen("Student Status Information.txt", "w")) == NULL)
		{
			printf("Failure to open Student Status Information.txt!\n");
			exit(1);
		}
	}
	else
	{
		for (; !feof(fp); n++)
		{
			fscanf(fp, "%lld%s %c%d-%d-%d", &stu[n].studentID,
				stu[n].name, &stu[n].sex,
				&stu[n].birthday.year, &stu[n].birthday.month, &stu[n].birthday.day);
			for (int j = 0; j < 4; j++)
				fscanf(fp, "%lf", &stu[n].score[j]);
		}
		n--;
	}
	char ch, kb;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("学生学籍管理系统\n");
		printf("1.新增学生学籍信息\n");
		printf("2.显示所有学生学籍信息\n");
		printf("3.查询某学生学籍信息\n");
		printf("4.删除/修改某学生学籍信息\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键返回主菜单\n");
		do {
			ch = getch();
			switch (ch)
			{
			case '1': n = Read(stu, fp, n); break;
			case '2': PrintInfo(stu, n); break;
			case '3': Search(stu, n, fp); break;
			case '4':
			{
				system("cls");
				gotoxy(0, 0);
				printf("1.修改某学生学籍信息\n");
				printf("2.删除某学生学籍信息\n");
				printf("请输入对应数字实现以上功能\n");
				printf("按ESC键返回\n");
				do kb = getch(); while (kb != '1' && kb != '2' && kb != 27);
				if (kb == 27) break;
				sort(stu, stu + n, cmpID);
				int ret = SearchStudentID(n);
				if (ret < 0)
				{
					printf("找不到相关信息\n");
					printf("按任意键返回学生学籍管理系统\n");
					while (!kbhit()); getch();
					break;
				}
				Printstu(ret, 1);
				if (kb == '1') fp = Modify(fp, ret, n);
				else fp = Delete(fp, ret, n);
				break;
			}
			case 27: fclose(fp); return;
			default: ch = 0;
			}
		} while (!ch);
	}
	return;
}

typedef struct type
{
	char ch;
	int x, y;
}TYPE;
void Typegame2_Rule()
{
	system("cls");
	gotoxy(0, 0);
	printf("游戏中会有随机字符下落，玩家要从键盘中输入对应字符使相应字符消去(区分大小写)，");
	printf("若字符落到屏幕下方的线则会减去1点HP。玩家一开始共有5点HP，HP归0时游戏结束。\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
char Randomalpha()
{
	char c = rand() % 26 + 'a';
	return c;
}
char RandomALPHA()
{
	char c = rand() % 26 + 'A';
	return c;
}
char RandomNumber()
{
	char c = rand() % 10 + '0';
	return c;
}
bool cmpx(TYPE a, TYPE b)
{
	return a.x > b.x;
}
void randomcreate(TYPE ch[], int i, int level)
{
	int j, random, range;
	if (level == 1)
		range = 13;
	else if (level == 2)
		range = 18;
	else range = 31;
	do {
		random = rand() % range;
		if (0 <= random && random < 13)
			ch[i].ch = RandomALPHA();
		else if (13 <= random && random < 18)
			ch[i].ch = RandomNumber();
		else ch[i].ch = Randomalpha();
		for (j = 0; j < i; j++)
			if (ch[i].x == ch[j].x && ch[i].ch == ch[j].ch) break;
	} while (i != j);
	ch[i].x = 1;
	do {
		ch[i].y = rand() % 80;
		for (j = 0; j < i; j++)
			if (ch[i].x == ch[j].x && ch[i].y == ch[j].y) break;
	} while (j != i);
}
int Typegame2_Record(int score, int level)
{
	FILE *fp;
	int bestscore = 0;
	char mode[3][7] = { "easy","normal","hard" };
	if (level == 1)
		fp = fopen("TypeGameII_easy.txt", "r+");
	else if (level == 2)
		fp = fopen("TypeGameII_normal.txt", "r+");
	else fp = fopen("TypeGameII_hard.txt", "r+");
	if (fp == NULL)
	{
		if (level == 1)
			fp = fopen("TypeGameII_easy.txt", "w");
		else if (level == 2)
			fp = fopen("TypeGameII_normal.txt", "w");
		else fp = fopen("TypeGameII_hard.txt", "w");
		if (fp == NULL)
		{
			printf("Failure to open TypeGameII_%s.txt!\n", mode[level - 1]);
			exit(4);
		}
	}
	else
	{
		fscanf(fp, "%d", &bestscore);
		rewind(fp);
	}
	if (score > bestscore)
	{
		fprintf(fp, "%d", score);
	}
	fclose(fp);
	return bestscore;
}
void Typegame2_Start(double speed, int N, int level)
{
	srand((unsigned)time(NULL));
	TYPE ch[24];
	int Type_N;
	for (Type_N = 0; Type_N < N; Type_N++)
		randomcreate(ch, Type_N, level);
	int i = 80, score = 0, point = 10, HP = 5;
	int combo = 0, times = 0, line = 500, t = 1000, a = 1, b = 1;
	char input, mode[3][7] = { "Easy","Normal","Hard" };
	bool gameover = false;
	system("cls");
	gotoxy(0, 0);
	printf("按ESC键暂停/继续游戏");
	gotoxy(0, 28);
	printf("%s Mode", mode[level - 1]);
	gotoxy(0, 53);
	printf("HP: %-3d", HP);
	gotoxy(0, 63);
	printf("Score: %-10d", score);
	gotoxy(1, 0);
	while (i--)
		putchar('-');
	gotoxy(24, 0);
	for (i = 80; i--;)
		putchar('-');
	while (1)
	{
		while (!kbhit())
		{
			for (i = 0; i < Type_N;)
			{
				if (ch[i].x != 1)
				{
					gotoxy(ch[i].x, ch[i].y);
					putchar(' ');
				}
				ch[i].x++;
				if (ch[i].x == 24)
				{
					HP--;
					gotoxy(0, 57);
					printf("%-3d", HP);
					if (HP)
					{
						randomcreate(ch, i, level);
						sort(ch, ch + Type_N, cmpx);
					}
					else
					{
						gameover = true;
						goto GameOver;
					}
				}
				else
				{
					gotoxy(ch[i].x, ch[i].y);
					putchar(ch[i].ch);
					i++;
				}
			}
			gotoxy(0, 79);
			Sleep(1000 / speed);
			if (times) combo = 0;
			times = 1;
		}
		input = getch();
		if (input == 27)
		{
			do input = getch(); while (input != 27);
		}
		for (i = 0; i < Type_N; i++)
		{
			if (input == ch[i].ch)
			{
				gotoxy(ch[i].x, ch[i].y);
				printf(" "); times = 0;
				score += point + (point / 5 * combo++);
				gotoxy(0, 70);
				printf("%-10d", score);
				if (score >= line)
				{
					speed *= 1.15 + level * 0.05 + a * 0.01;
					point += 5 * a++;
					line += point * 15 * Type_N;
				}
				if (score >= t)
				{
					int temp = t;
					for (; temp >= 10; temp /= 10);
					if (temp == 1)
					{
						HP++;
						t *= 5;
					}
					else t *= 2;
					gotoxy(0, 57);
					printf("%-3d", HP);
					randomcreate(ch, Type_N++, level);
					point += 10 * b++;
				}
				randomcreate(ch, i, level);
				sort(ch, ch + Type_N, cmpx);
				break;
			}
		}
	}
GameOver:
	int bestscore = Typegame2_Record(score, level);
	gotoxy(10, 26);
	for (i = 26; i--;)
		putchar(' ');
	gotoxy(11, 26);
	printf("        Game Over!        ");
	gotoxy(12, 26);
	printf("  Score: %-8d", score);
	if (score > bestscore)
	{
		bestscore = score;
		printf("New Best ");
	}
	gotoxy(13, 26);
	printf("  Best Score: %-10d  ", bestscore);
	gotoxy(14, 26);
	for (i = 26; i--;)
		putchar(' ');
	Sleep(1000);
	gotoxy(14, 26);
	printf("  按空格键返回游戏主界面  ");
	gotoxy(15, 26);
	for (i = 26; i--;)
		putchar(' ');
	char reply;
	do reply = getch(); while (reply != ' ');
	return;
}
void Typegame2_Set(int &speed, int &N)
{
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("请选择需要进行修改的设置\n");
		printf("1.字符下降速度\n");
		printf("2.字符密度\n");
		printf("按ESC键返回游戏主界面\n");
		char ch;
		do {
			ch = getch();
			if (ch == 27) return;
		} while (ch != '1' && ch != '2');
		system("cls");
		gotoxy(0, 0);
		if (ch == '1')
		{
			printf("目前字符下降速度: %d\n", speed);
			printf("请输入你想要的速度(0~10): ");
			while (!scanf("%d", &speed) || speed < 0 || speed > 10)
			{
				while (getchar() != '\n');
				printf("输入速度有误\n");
				printf("请重新输入速度(0~10): ");
			}
		}
		else
		{
			printf("目前游戏开始时屏幕中可同时存在的字符个数: %d\n", N);
			printf("请输入你想要的字符密度(5~10): ");
			while (!scanf("%d", &N) || N < 5 || N > 10)
			{
				while (getchar() != '\n');
				printf("输入字符密度有误\n");
				printf("请重新输入字符密度(5~10): ");
			}
		}
		printf("修改成功\n");
		printf("按任意键返回设置界面\n");
		getch();
	}
}
void Typegame2()
{
	int speed = 2;
	int N = 5;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("打字游戏II\n");
		printf("1.开始游戏\n");
		printf("2.游戏规则\n");
		printf("3.设置\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键退出游戏\n");
		char ch;
		do {
			ch = getch();
			switch (ch)
			{
			case '1':
				system("cls");
				gotoxy(0, 0);
				printf("1.简单\n");
				printf("2.普通\n");
				printf("3.困难\n");
				char level;
				do level = getch(); while (level < '1' || level > '3');
				Typegame2_Start(speed * 0.1 + 1, N, level - '0'); break;
			case '2': Typegame2_Rule(); break;
			case '3': Typegame2_Set(speed, N); break;
			case 27: return;
			default: ch = 0;
			}
		} while (!ch);
	}
}

void MemoryCardGame_Rule()
{
	system("cls");
	gotoxy(0, 0);
	printf("说明：玩家可以从一堆牌中将背面朝上的任意2张牌翻开，若2张牌的图案相同，则将其消去；");
	printf("若2张牌图案不同，则将这2张牌翻回背面朝上。当玩家成功消去所有牌或剩下一张单独的牌时，游戏结束。\n");
	printf("操作：W、A、S、D键移动，空格翻开牌，ESC键退出游戏\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
void RandomArray(int* b, int total)
{
	for (int i = 0; i < total; i++)
	{
		int index = rand() % total;
		swap(b[index], b[i]);
	}
	return;
}
void MemoryCardGame_RandomArray(char a[][16], int m, int n, int differ)
{
	srand((unsigned)time(NULL));
	//char pic[50] = { 2, 3, 4, 5, 6, 11, 12, 14, 15 };
	//char pic[50] = { 'A','2','3','4','5','6','7','8','9','0','J','Q','K' };
	int pic[83] = { 33 }, i, x = 1;
	for (i = 35; i <= 125; i++)
		if (i != 39 && i != 42 && i != 44 && i != 46 && i != 79 && !(94 <= i && i <= 96) && i != 108)
			pic[x++] = i;
	RandomArray(pic, 83);
	int total = m * n;
	int* b = (int *)calloc(total, sizeof(int));
	for (i = 0; i < total; i++)
		*(b + i) = i;
	RandomArray(b, total);
	int count = 0, same = total / differ;
	if (same % 2) same--;
	for (i = 0; count < differ; i++)
	{
		a[b[i] / n][b[i] % n] = pic[count];
		if (i % same == same - 1) count++;
	}
	for (count = 0; i < total - (total % 2); i++)
	{
		a[b[i] / n][b[i] % n] = pic[count];
		if (i % 2) count++;
	}
	if (total % 2) a[b[i] / n][b[i] % n] = pic[differ];
	free(b);
	return;
}
void MemoryCardGame_Start(int m, int n, int card, double sleep)
{
	char a[10][16];
	bool open[10][16];
	int openX[2], openY[2];
	MemoryCardGame_RandomArray(a, m, n, card);
	memset(open, 0, sizeof(open));
	int p = 0, x = 3, y = 2, i, j, count = 0;
	int match = m * n / 2;
	system("cls");
	gotoxy(0, 0);
	printf("剩余%2d对牌    ", match);
	printf("翻牌次数: %-10d", count);
	printf("WASD键移动，空格翻牌，ESC键退出游戏");
	gotoxy(3, 1);
	for (i = 0; i < m; i++)
	{
		for (j = 0; j < n; j++)
			printf(" *");
		printf("\n ");
	}
	gotoxy(x, y);
	while (match)
	{
		char c = getch();
		c = tolower(c);
		switch (c)
		{
		case 'a':
			if (y > 2) y -= 2; break;
		case 's':
			if (x < m + 2) x += 1; break;
		case 'd':
			if (y < n * 2) y += 2; break;
		case 'w':
			if (x > 3) x -= 1; break;
		case ' ':
			if (!open[x - 3][y / 2 - 1])
			{
				printf("%c", a[x - 3][y / 2 - 1]);
				gotoxy(x, y);
				open[x - 3][y / 2 - 1] = true;
				openX[p] = x - 3; openY[p] = y / 2 - 1;
				p++; count++;
				gotoxy(0, 24);
				printf("%d", count);
				if (p == 2)
				{
					if (a[openX[0]][openY[0]] == a[openX[1]][openY[1]])
					{
						match--;
						gotoxy(0, 4);
						printf("%2d", match);
					}
					else
					{
						gotoxy(x, y);
						Sleep(sleep);
						for (int j = 2; j--;)
						{
							gotoxy(openX[j] + 3, openY[j] * 2 + 2);
							putchar('*');
							open[openX[j]][openY[j]] = false;
						}
					}
					p = 0;
				}
			}
			break;
		case 27: gotoxy(m + 4, 0);
			printf("是否确定要退出游戏？\n");
			printf("Y:确定\tN:取消");
			char reply;
			do {
				reply = getch();
				reply = toupper(reply);
				if (reply == 'Y') return;
			} while (reply != 'N');
			gotoxy(m + 4, 0);
			printf("                    \n");
			printf("      \t      ");
		}
		gotoxy(x, y);
	}
	gotoxy(m + 4, 0);
	printf("Congratulations!You Win!\n");
	printf("翻牌次数: %d\n", count);
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
void MemoryCardGame_Set(int &m, int &n, int &pic, double &sleep)
{
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("请选择需要进行修改的设置\n");
		printf("1.行列数和不同的可配对图案数\n");
		printf("2.翻开2张不相同的牌的停顿时间\n");
		printf("按ESC键返回游戏主界面\n");
		char ch;
		do {
			ch = getch();
			if (ch == 27) return;
		} while (ch != '1' && ch != '2');
		system("cls");
		gotoxy(0, 0);
		if (ch == '1')
		{
			printf("请输入需要修改的数据\n");
			printf("行(2~10): %2d  ->  \n", m);
			printf("列(2~16): %2d  ->  \n", n);
			printf("不同的图案数目(2~行*列/2): %d  ->  \n", pic);
			gotoxy(1, 18);
			int line, row, dif;
			if (!scanf("%d", &line) || line < 2 || line > 10)
				goto InfoError;
			gotoxy(2, 18);
			if (!scanf("%d", &row) || row < 2 || row > 16)
				goto InfoError;
			gotoxy(3, 35);
			if (!scanf("%d", &dif) || dif < 2 || dif > line * row / 2)
				goto InfoError;
			m = line, n = row, pic = dif;
		}
		else
		{
			printf("目前停顿时间: %gs\n", sleep);
			printf("请输入需要修改的停顿时间(0.5~2): ");
			if (!scanf("%lf", &sleep) || sleep < 0.5 || sleep > 2)
			{
				while (getchar() != '\n');
				printf("输入数据有误\n");
				printf("请重新输入停顿时间(0.5~2): ");
			}
		}
		printf("修改成功\n");
	re:printf("按任意键返回设置界面\n");
		getch();
		continue;
	InfoError:
		while (getchar() != '\n');
		gotoxy(4, 0);
		printf("输入数据有误，修改失败\n");
		goto re;
	}
}
void MemoryCardGame()
{
	int m = 6, n = 6, pic = 9;
	double sleep = 1.5;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("记忆翻牌游戏\n");
		printf("1.开始游戏\n");
		printf("2.游戏规则\n");
		printf("3.设置\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键退出游戏\n");
		char ch;
		do {
			ch = getch();
			switch (ch)
			{
			case '1': MemoryCardGame_Start(m, n, pic, sleep * 1000); break;
			case '2': MemoryCardGame_Rule(); break;
			case '3': MemoryCardGame_Set(m, n, pic, sleep); break;
			case 27: return;
			default: ch = 0;
			}
		} while (!ch);
	}
}

typedef struct node
{
	int x, y;
}NODE;
NODE snake[1716], food, shit[1714];
void GluttonousSnake_Rule()
{
	system("cls");
	gotoxy(0, 0);
	printf("操作：WASD移动，P键暂停\n");
	printf("简单模式：移动贪食蛇吃水果(@)，碰到墙或自身就GameOver\n");
	printf("困难模式：在简单模式的基础上，吃掉的水果在蛇身离开时会在相同的位置上变成粪便(&)，碰到便会GameOver\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
int GluttonousSnake_Record(int score, int level)
{
	FILE *fp;
	int bestscore = 0;
	char mode[2][5] = { "easy","hard" };
	if (level == 0)
		fp = fopen("GluttonousSnake_easy.txt", "r+");
	else if (level == 1)
		fp = fopen("GluttonousSnake_hard.txt", "r+");
	if (fp == NULL)
	{
		if (level == 0)
			fp = fopen("GluttonousSnake_easy.txt", "w");
		else if (level == 1)
			fp = fopen("GluttonousSnake_hard.txt", "w");
		if (fp == NULL)
		{
			printf("Failure to open GluttonousSnake_%s.txt!\n", mode[level]);
			exit(5);
		}
	}
	else
	{
		fscanf(fp, "%d", &bestscore);
		rewind(fp);
	}
	if (score > bestscore)
	{
		bestscore = score;
		fprintf(fp, "%d", bestscore);
	}
	fclose(fp);
	return bestscore;
}
void GameMap()
{
	int i = 78;
	gotoxy(1, 0);
	printf("+");
	while (i--)
		printf("-");
	printf("+");
	gotoxy(2, 0);
	for (i = 22; i--;)
		printf("|\n");
	printf("+");
	for (i = 2; i < 24; i++)
	{
		gotoxy(i, 79);
		putchar('|');
	}
	gotoxy(i, 79);
	putchar('+');
	gotoxy(24, 1);
	for (i = 78; i--;)
		putchar('-');
	return;
}
void CreateFood(int len, int count)
{
	int randomx, randomy, flag;
	do {
		flag = 0;
		randomx = rand() % 22 + 2;
		randomy = rand() % 78 + 1;
		for (int i = 0; i < len; i++)
		{
			if (randomx == snake[i].x && randomy == snake[i].y)
			{
				flag = 1;
				break;
			}
		}
		for (int i = 0;!flag && i < count; i++)
		{
			if (randomx == shit[i].x && randomy == shit[i].y)
				flag = 1;
		}
	} while (flag);
	food.x = randomx;
	food.y = randomy;
	gotoxy(food.x, food.y);
	putchar('@');
	return;
}
int SnakeMove(int len, char direct, int count)
{
	NODE move = { snake[len - 1].x ,snake[len - 1].y };
	int i, eat, flag = 1;
	switch (direct)
	{
	case 'w': move.x--; break;
	case 's': move.x++; break;
	case 'a': move.y--; break;
	default: move.y++;
	}
	if (move.x == 1 || move.x == 24 || move.y == 0 || move.y == 79)
		return -1;
	for (i = 1; i < len; i++)
	{
		if (move.x == snake[i].x && move.y == snake[i].y)
			return -1;
	}
	gotoxy(snake[len - 1].x, snake[len - 1].y);
	putchar('*');
	for (i = 0; i < count; i++)
	{
		if (move.x == shit[i].x && move.y == shit[i].y)
			return -1;
		if (shit[i].x == snake[len - 1].x && shit[i].y == snake[len - 1].y)
		{
			gotoxy(snake[len - 1].x, snake[len - 1].y);
			putchar('$');
		}
		if (shit[i].x == snake[0].x && shit[i].y == snake[0].y)
			flag = 0;
	}
	snake[len].x = move.x;
	snake[len].y = move.y;
	if (move.x == food.x && move.y == food.y)
		eat = 1;
	else
	{
		gotoxy(snake[0].x, snake[0].y);
		if (flag)
			putchar(' ');
		else putchar('&');
		for (int i = 0; i < len; i++)
		{
			snake[i].x = snake[i + 1].x;
			snake[i].y = snake[i + 1].y;
		}
		eat = 0;
	}
	gotoxy(move.x, move.y);
	putchar('#');
	return eat;
}
void GluttonousSnake_GameStart(double speed, int level)
{
	srand((unsigned)time(NULL));
	int i, len = 0, score = 0, times = 0, count = 0, kb = 1, s = speed;
	char mode[2][5] = { "Easy","Hard" };
	system("cls");
	gotoxy(0, 0);
	printf("按P暂停/继续游戏");
	gotoxy(0, 35);
	printf("%s Mode", mode[level]);
	gotoxy(0, 62);
	printf("吃掉的水果数: %-4d", score);
	GameMap();
	char direct = 'd', ch;
	snake[len].x = 9;
	snake[len++].y = 8;
	snake[len].x = 9;
	snake[len++].y = 9;
	gotoxy(9, 8);
	printf("*#");
	CreateFood(len, count);
	gotoxy(0, 79);
	Sleep(450 / speed);
	while (1)
	{
		while (!kbhit())
		{
			int ret;
			ret = SnakeMove(len, direct, count);
			if (ret == -1)
				goto GameOver;
			if (ret)
			{
				score++; times++;
				gotoxy(0, 76);
				printf("%-4d", score);
				if (level)
				{
					shit[count].x = food.x;
					shit[count++].y = food.y;
				}
				CreateFood(++len, count);
				if (times == 2)
				{
					speed *= 1 + 0.07 * s;
					times = 0;
				}
			}
			gotoxy(0, 79);
			Sleep(450 / speed);
			kb = 1;
		}
		ch = getch();
		ch = tolower(ch);
		if (kb && ((ch == 'w' && direct != 's') ||
			(ch == 'a' && direct != 'd') ||
			(ch == 's' && direct != 'w') ||
			(ch == 'd' && direct != 'a')))
		{
			direct = ch;
			kb = 0;
		}
		else if (ch == 'p')
		{
			do ch = getch(); while (ch != 'p');
		}
	}
GameOver:
	int bestscore = GluttonousSnake_Record(score, level);
	gotoxy(10, 27);
	for (i = 24; i--;)
		putchar(' ');
	gotoxy(11, 27);
	printf("       Game Over!       ");
	gotoxy(12, 27);
	printf("   一共吃了%4d个水果   ", score);
	gotoxy(13, 27);
	printf("     最高记录: %-4d     ", bestscore);
	gotoxy(14, 27);
	for (i = 24; i--;)
		putchar(' ');
	Sleep(1000);
	gotoxy(14, 27);
	printf(" 按空格键返回游戏主界面 ");
	gotoxy(15, 27);
	for (i = 24; i--;)
		putchar(' ');
	char reply;
	do reply = getch(); while (reply != ' ');
	return;
}
void GluttonousSnake_Set(int& speed)
{
	system("cls");
	gotoxy(0, 0);
	printf("是否要更改速度？\n");
	printf("Y/y:是    N/n:否\n");
	char reply;
	do {
		reply = getch();
		reply = toupper(reply);
		if (reply == 'N') return;
	} while (reply != 'Y');
	printf("请输入要改变的速度\n");
	printf("速度(1~10): %d  ->  ", speed);
	while (!scanf("%d", &speed) || speed < 1 || speed > 10)
	{
		while (getchar() != '\n');
		printf("输入数据无效\n");
		printf("请重新输入速度(1~10): ");
	}
	printf("修改成功\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
void GluttonousSnake()
{
	int speed = 3;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("贪食蛇\n");
		printf("1.开始游戏\n");
		printf("2.游戏说明\n");
		printf("3.设置\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键退出游戏\n");
		char ch;
		do {
			ch = getch();
			switch (ch)
			{
			case '1':
				system("cls");
				gotoxy(0, 0);
				printf("1.简单\n");
				printf("2.困难\n");
				char level;
				do level = getch(); while (level < '1' || level > '2');
				GluttonousSnake_GameStart(speed * 0.17 + 1.34, level - '1');
				break;
			case '2': GluttonousSnake_Rule(); break;
			case '3': GluttonousSnake_Set(speed); break;
			case 27: return;
			default: ch = 0;
			}
		} while (!ch);
	}
}

int MineSweeper_map[23][30], MS_m, MS_n;
short map_open[23][30];
void MineSweeper_Rule()
{
	system("cls");
	gotoxy(0, 0);
	printf("规则: 方块上的数字表示其周围方圆一格，即3x3区域的8个格子中的地雷数目\n");
	printf("操作: WASD移动光标，J打开方块，K标记地雷，空格/回车相当于鼠标左右键双击展开\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return;
}
void CreateMap(int mine, int x, int y)
{
	srand(time(NULL));
	memset(MineSweeper_map, 0, sizeof(MineSweeper_map));
	int i, j, total = MS_m * MS_n, count = mine;
	int* b = (int*)calloc(total, sizeof(int));
	for (i = 0; i < total; i++)
		*(b + i) = i;
	RandomArray(b, total);
	for (i = 0; count; i++)
	{
		if (b[i] / MS_n != x || b[i] % MS_n != y)
		{
			MineSweeper_map[b[i] / MS_n][b[i] % MS_n] = -1;
			count--;
		}
	}
	for (i = 0; i < MS_m; i++)
	{
		for (j = 0; j < MS_n; j++)
		{
			if (MineSweeper_map[i][j] != -1)
			{
				count = 0;
				if (i > 0 && j > 0 && MineSweeper_map[i - 1][j - 1] == -1)
					count++;
				if (i > 0 && MineSweeper_map[i - 1][j] == -1)
					count++;
				if (i > 0 && j < MS_n - 1 && MineSweeper_map[i - 1][j + 1] == -1)
					count++;
				if (j > 0 && MineSweeper_map[i][j - 1] == -1)
					count++;
				if (j < MS_n - 1 && MineSweeper_map[i][j + 1] == -1)
					count++;
				if (i < MS_m - 1 && j > 0 && MineSweeper_map[i + 1][j - 1] == -1)
					count++;
				if (i < MS_m - 1 && MineSweeper_map[i + 1][j] == -1)
					count++;
				if (i < MS_m - 1 && j < MS_n - 1 && MineSweeper_map[i + 1][j + 1] == -1)
					count++;
				MineSweeper_map[i][j] = count;
			}
		}
	}
	free(b);
	return;
}
void ShowMap()
{
	for (int i = 0; i < MS_m; i++)
	{
		for (int j = 0; j < MS_n; j++)
		{
			if (MineSweeper_map[i][j] == -1)
			{
				gotoxy(i + 2, (j + 1) * 2);
				putchar('*');
			}
			else if (map_open[i][j] == -1)
			{
				gotoxy(i + 2, (j + 1) * 2);
				putchar('X');
			}
		}
	}
	gotoxy(4, (MS_n + 2) * 2);
	printf("Game Over!");
	return;
}
int MineSweeper_Record(int score, int level)
{
	FILE* fp;
	int bestscore;
	char mode[3][7] = { "easy","normal","hard" };
	if (level == 1)
		fp = fopen("MineSweeper_easy.txt", "r+");
	else if (level == 2)
		fp = fopen("MineSweeper_normal.txt", "r+");
	else
		fp = fopen("MineSweeper_hard.txt", "r+");
	if (fp == NULL)
	{
		if (level == 1)
			fp = fopen("MineSweeper_easy.txt", "w");
		else if (level == 2)
			fp = fopen("MineSweeper_normal.txt", "w");
		else fp = fopen("MineSweeper_hard.txt", "w");
		if (fp == NULL)
		{
			printf("Failure to open MineSweeper_%s.txt!\n", mode[level - 1]);
			exit(6);
		}
		fprintf(fp, "%d", score);
		fclose(fp);
		return score;
	}
	else fscanf(fp, "%d", &bestscore);
	if (score < bestscore)
	{
		bestscore = score;
		rewind(fp);
		fprintf(fp, "%10d", bestscore);
	}
	fclose(fp);
	return bestscore;
}
int MineSweeper_Spread(int x, int y);
int ShowValue(int x, int y)
{
	int count = 0;
	if (MineSweeper_map[x][y] != -1)
	{
		map_open[x][y] = 1;
		if (MineSweeper_map[x][y] > 0)
			printf("%d", MineSweeper_map[x][y]);
		else
		{
			putchar(' ');
			count = MineSweeper_Spread(x + 2, (y + 1) * 2);
		}
	}
	else return 0;
	return count + 1;
}
int MineSweeper_Spread(int x, int y)
{
	int i = x - 2, j = y / 2 - 1, count = 0;
	if (i > 0 && j > 0 && map_open[i - 1][j - 1] == 0)
	{
		gotoxy(x - 1, y - 2);
		count += ShowValue(i - 1, j - 1);
	}
	if (i > 0 && map_open[i - 1][j] == 0)
	{
		gotoxy(x - 1, y);
		count += ShowValue(i - 1, j);
	}
	if (i > 0 && j < MS_n - 1 && map_open[i - 1][j + 1] == 0)
	{
		gotoxy(x - 1, y + 2);
		count += ShowValue(i - 1, j + 1);
	}
	if (j > 0 && map_open[i][j - 1] == 0)
	{
		gotoxy(x, y - 2);
		count += ShowValue(i, j - 1);
	}
	if (j < MS_n - 1 && map_open[i][j + 1] == 0)
	{
		gotoxy(x, y + 2);
		count += ShowValue(i, j + 1);
	}
	if (i < MS_m - 1 && j > 0 && map_open[i + 1][j - 1] == 0)
	{
		gotoxy(x + 1, y - 2);
		count += ShowValue(i + 1, j - 1);
	}
	if (i < MS_m - 1 && map_open[i + 1][j] == 0)
	{
		gotoxy(x + 1, y);
		count += ShowValue(i + 1, j);
	}
	if (i < MS_m - 1 && j < MS_n - 1 && map_open[i + 1][j + 1] == 0)
	{
		gotoxy(x + 1, y + 2);
		count += ShowValue(i + 1, j + 1);
	}
	return count;
}
char MineSweeper_op(int &x, int &y, int &mine)
{
	int i = x - 2, j = y / 2 - 1;
	char c = getch();
	c = tolower(c);
	switch (c)
	{
	case 'a':
		if (y > 2) y -= 2; break;
	case 's':
		if (x < MS_m + 1) x++; break;
	case 'd':
		if (y < MS_n * 2) y += 2; break;
	case 'w':
		if (x > 2) x--; break;
	case 'k':
		if (map_open[i][j] != 1)
		{
			if (map_open[i][j] == 0)
			{
				putchar('!');
				map_open[i][j] = -1;
				mine--;
			}
			else if (map_open[i][j] == -1)
			{
				putchar('O');
				map_open[i][j] = 0;
				mine++;
			}
			gotoxy(0, 10);
			printf("%03d", mine);
		}
		break;
	case '\r':
	case '\n': c = ' ';
	}
	gotoxy(x, y);
	return c;
}
void MineSweeper_GameStart(int mine, int level)
{
	memset(map_open, 0, sizeof(map_open));
	int count = mine, timekeeping = 0, i, j, match = MS_m * MS_n - mine, ret, m = 5;
	system("cls");
	gotoxy(0, 0);
	printf("剩余地雷: %03d\t游戏时间: %-10d\t", count, timekeeping);
	printf("按ESC键退出游戏");
	gotoxy(2, 1);
	for (i = 0; i < MS_m; i++)
	{
		for (j = 0; j < MS_n; j++)
		{
			printf(" O");
		}
		printf("\n ");
	}
	int x = 2, y = 2;
	gotoxy(x, y);
	char ch;
	do {
		ch = MineSweeper_op(x, y, count);
		if (ch == 27)
			return;
	} while (ch != 'j');
	CreateMap(mine, x - 2, y / 2 - 1);
	match -= ShowValue(x - 2, y / 2 - 1);
	gotoxy(x, y);
	time_t starttime = time(NULL);
	while (match)
	{
		while (!kbhit())
		{
			if (time(NULL) - starttime - timekeeping > 0)
			{
				gotoxy(0, 26);
				printf("%-d", ++timekeeping);
				gotoxy(x, y);
			}
		}
		ch = MineSweeper_op(x, y, count);
		int i = x - 2, j = y / 2 - 1;
		if (ch == 'j' && map_open[i][j] == 0)
		{
			ret = ShowValue(i, j);
			if (ret == 0)
			{
				ShowMap();
				goto replay;
			}
			match -= ret;
		}
		else if (ch == ' ' && map_open[i][j] == 1)
		{
			int flag = 0;
			bool wrong = false;
			if (i > 0 && j > 0 && map_open[i - 1][j - 1] == -1)
			{
				if (MineSweeper_map[i - 1][j - 1] != -1)
					wrong = true;
				flag++;
			}
			if (i > 0 && map_open[i - 1][j] == -1)
			{
				if (MineSweeper_map[i - 1][j] != -1)
					wrong = true;
				flag++;
			}
			if (i > 0 && j < MS_n - 1 && map_open[i - 1][j + 1] == -1)
			{
				if (MineSweeper_map[i - 1][j + 1] != -1)
					wrong = true;
				flag++;
			}
			if (j > 0 && map_open[i][j - 1] == -1)
			{
				if (MineSweeper_map[i][j - 1] != -1)
					wrong = true;
				flag++;
			}
			if (j < MS_n - 1 && map_open[i][j + 1] == -1)
			{
				if (MineSweeper_map[i][j + 1] != -1)
					wrong = true;
				flag++;
			}
			if (i < MS_m - 1 && j > 0 && map_open[i + 1][j - 1] == -1)
			{
				if (MineSweeper_map[i + 1][j - 1] != -1)
					wrong = true;
				flag++;
			}
			if (i < MS_m - 1 && map_open[i + 1][j] == -1)
			{
				if (MineSweeper_map[i + 1][j] != -1)
					wrong = true;
				flag++;
			}
			if (i < MS_m - 1 && j < MS_n - 1 && map_open[i + 1][j + 1] == -1)
			{
				if (MineSweeper_map[i + 1][j + 1] != -1)
					wrong = true;
				flag++;
			}
			if (MineSweeper_map[i][j] == flag)
			{
				if (wrong)
				{
					ShowMap();
					goto replay;
				}
				else match -= MineSweeper_Spread(x, y);
			}
		}
		else if (ch == 27)
			return;
		gotoxy(x, y);
	}
	gotoxy(4, (MS_n + 2) * 2);
	printf("You Win!");
	int bestscore;
	if (level)
		bestscore = MineSweeper_Record(timekeeping,level);
	gotoxy(m++, (MS_n + 2) * 2);
	printf("游戏时间: %ds", timekeeping);
	if (level)
	{
		gotoxy(m++, (MS_n + 2) * 2);
		printf("最高纪录: %ds", bestscore);
	}
replay:
	gotoxy(m++, (MS_n + 2) * 2);
	printf("按R重新开始");
	gotoxy(m++, (MS_n + 2) * 2);
	printf("按ESC键返回游戏主界面");
	do {
		ch = getch();
		if (toupper(ch) == 'R')
		{
			MineSweeper_GameStart(mine, level);
			return;
		}
	} while (ch != 27);
	return;
}
bool MineSweeper_Set(int &mine)
{
	system("cls");
	gotoxy(0, 0);
	printf("请输入自定义游戏版参数\n");
	printf("宽度n(9~30): %2d  ->  \n", MS_n);
	printf("高度m(9~23): %2d  ->  \n", MS_m);
	printf("地雷(10~(m-1)*(n-1): %3d  ->  ", mine);
	gotoxy(1, 21);
	int m, n, quantity;
	if (!scanf("%d", &n) || n < 9 || n > 30)
		goto InfoError;
	gotoxy(2, 21);
	if (!scanf("%d", &m) || m < 9 || m > 23)
		goto InfoError;
	gotoxy(3, 30);
	if (!scanf("%d", &quantity) || quantity < 10 || quantity >(m - 1) * (n - 1))
		goto InfoError;
	MS_m = m, MS_n = n, mine = quantity;
	printf("修改成功\n");
	printf("按任意键开始游戏\n");
	getch();
	return true;
InfoError:
	while (getchar() != '\n');
	gotoxy(4, 0);
	printf("输入数据有误\n");
	printf("按任意键返回游戏主界面\n");
	getch();
	return false;
}
void MineSweeper()
{
	MS_m = 9, MS_n = 9;
	int mine = 10;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("扫雷\n");
		printf("1.开始游戏\n");
		printf("2.游戏规则\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键退出游戏\n");
		char ch;
		do {
			ch = getch();
			switch (ch)
			{
			case '1':
				system("cls");
				gotoxy(0, 0);
				printf("1.初级\n");
				printf("2.中级\n");
				printf("3.高级\n");
				printf("4.自定义\n");
				char level;
				do level = getch(); while (level < '1' || level > '4');
				if (level == '1')
				{
					MS_m = MS_n = 9;
					mine = 10;
				}
				else if (level == '2')
				{
					MS_m = MS_n = 16;
					mine = 40;
				}
				else if (level == '3')
				{
					MS_m = 16;
					MS_n = 30;
					mine = 99;
				}
				else
				{
					if (MineSweeper_Set(mine) == 0)
						break;
					level = '0';
				}
				MineSweeper_GameStart(mine, level - '0');
				break;
			case '2': MineSweeper_Rule(); break;
			case 27: return;
			default: ch = 0;
			}
		} while (!ch);
	}
}

int main()
{
	char ch;
	while (1)
	{
		system("cls");
		gotoxy(0, 0);
		printf("1.学生学籍管理系统\n");
		printf("2.打字游戏I(此功能暂未实现)\n");
		printf("3.打字游戏II\n");
		printf("4.翻牌游戏\n");
		printf("5.贪食蛇\n");
		printf("6.扫雷\n");
		printf("请输入对应数字实现以上功能\n");
		printf("按ESC键退出程序\n");
		do {
			ch = getch();
			switch (ch)
			{
			case '1': StudentStatusInformation(); break;
			case '3': Typegame2(); break;
			case '4': MemoryCardGame(); break;
			case '5': GluttonousSnake(); break;
			case '6': MineSweeper(); break;
			case '2':
				system("cls");
				gotoxy(0, 0);
				printf("此功能暂未实现\n");
				printf("按任意键返回主菜单\n");
				getch(); break;
			case 27: exit(0);
			default: ch = 0;
			}
		} while (!ch);
	}
	return 0;
}
