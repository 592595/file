#include<iostream>
#include<fstream>
#include<string>
#include<cstring>
#include<conio.h>
#include<ctime>
using namespace std;
class Event{

public:
	string thing;
	Event *next;
	friend void input();
	friend void showAll();
	friend void showpart();
	friend void del();
	friend void change();
	friend void save();
	friend void show();
};


Event *head = NULL;
void input();
void showAll();
void showpart();
void del();
void change();
void save();
void show();


int main()
{
	cout << "输入数字请选择(按其他键退出)：" << endl;
	cout << "1.新建 2.查看 3.编辑 4.保存并退出 " << endl;
	int k;
	while (1)
	{
		k = _getch();
		system("cls");
		if (k == '1')
		{
			input();
			system("cls");
			cout << "输入数字请选择(按其他键退出)：" << endl;
			cout << "1.新建 2.查看 3.编辑 4.保存并退出 " << endl;
		}
		else if (k == '2')
		{ 
			show();
			system("cls");
			cout << "输入数字请选择(按其他键退出)：" << endl;
			cout << "1.新建 2.查看 3.编辑 4.保存并退出 " << endl;
		}
		else if (k == '4')
		{
			return 0;
		}

	}
}


void input()
{
	ofstream outstuf("d:\\note.txt",ios::app);
	Event *s;
	s = new Event;
	cout << "请输入事件：" << endl;
	cin.ignore();//把回车（包括回车）之前的所以字符从输入缓冲（流）中清除出去
	getline(cin, s->thing);
	outstuf << s->thing << endl;
	s->next = head;
	head = s;
	outstuf.close();
	return;
}


void show()
{
	cout << "输入数字选择操作：\n";
	cout << "1.查看全部  2.指定时间内容查看  3.返回上一级" << endl;
	int k;
	while (1)
	{
		k = _getch();
		if (k == '1')
		{
			showAll();
			cout << "输入数字选择操作：\n";
			cout << "1.查看全部  2.指定时间内容查看  3.返回上一级" << endl;
		}
		/*else if (k == '2')
		{
			showpart();
			system("cls");
			cout << "输入数字选择操作：\n";
			cout << "1.查看全部  2.指定时间内容查看  3.返回上一级" << endl;
		}*/
		else if (k == '3')
		{
			return ;
		}
	}

}

void showAll()
{
	ifstream instuf("d:\\note.txt",ios::in);//打开文件
	//instuf.seekg(0, ios::beg);//流指针置在文件头
	Event *p;
	p = head;
	while (p)
	{
		while (instuf >> p->thing)
		{
			cout << p->thing << endl;
		}		
		p = p->next;
	}
}
