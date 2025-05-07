# Diary_2

<pre>
#include<iostream>
#include<fstream>
#include<string.h>
using namespace std;
class dnode{
	public:
		int id;
		char date[20];
		char info[100];
		char mixture[125];
		dnode *next;
	};

class DDiary{
	public:
	fstream file;
	char info[100], name[100], date[100];
	int code;
	size_t num=strlen(info);

	int Diary()
	{
		cout << "請輸入存入日記名稱:\n";
		cin >> name;
		cout << "請輸入記事日期:(XXXX-XX-XX)\n";
		cin >> date;
		cout << "請輸入日記內容:\n";
		cin >> info;
	}
	
	int writein()
	{		
		strcat(date,"\n"); //要在算之前插入這個 
		strcat(info,"\n");
		size_t diary = strlen(info); //轉換成長度了 strlen不能直接用 
		size_t date1 = strlen(date);
		file.open(name,ios::app);
		file.write(date,date1);
		file.write(info,diary);
		file.close();
	}
	
	int coding()
	{
		int ans;
		strcat(info,"\n");
		cout<<"請輸入密碼\n";
		cin>>ans;	
		for(int i=0;i<num;i++)
		{
			info[i]=info[i]+ans;
		}
		cout << "完成\n";
	}
	
	int read()
	{
		fstream file;
		int anw;
	
		cout<<"請輸入檔案名稱\n";
		cin>>name;
	
		cout<<"請輸入正確密碼\n";
		cin>>anw;
		
		file.open(name,ios::in);
		file.read(info,sizeof(info));	
		size_t num=strlen(info);
		file.close();
		
		while( file.getline(info,sizeof(info), ':') )
		{
		cout << info << endl;
		}
		
		for(int i=0;i<num;i++)
		{
			info[i]=info[i]-anw;
		}

	
		exit(1);
	}
	
	int again()
	{
		cout << "請問是否繼續輸入日記?(輸入:Y/N):\n";
		char YN;
		cin >> YN;
		if(YN == 'Y' ||YN == 'y')
		{
			return 1;
		}
		else if(YN == 'N' || YN == 'n')
		{
			exit(1);
		}
		else
		{
			cout << "錯誤";
		}
	}
	
	int catalog()
	{
		cout << "請選擇:\n";
		cout << "(1)寫日記 (2)讀日記 (3)離開\n";
		char choose;
		cin >> choose;
		
		if(choose == '1')
		{
			do{
				Diary();
				writein();
				coding();
			}
			while(again());
		}
		
		else if(choose == '2')
		{
			do{
				read();
			}
			while(again());
		}
		
		else if(choose == '3')
		{
			exit(1);
		}
	}
};

int main()
	{
		DDiary A;
		do
		{
			A.catalog();
			A.Diary();
			A.writein();
			A.coding();
			A.read();
		}
		while(A.again());
	} 
</pre>
