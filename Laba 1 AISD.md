#include <conio.h>
#include <iostream>

using namespace std;
 
struct element //Структура с инфополями и адресным полем
{
 int x; //Инфополе. значения из x будут передаваться в список
 element *Next; //Адресное поле
};
 
class List //Класс Список
{
 element *Head; //Указатель на последний активный элемент или просто голова списка
 public:
	  int size;
  List() {Head=NULL; size = 0;} //Конструктор и инициализация указателя пустым значением
 ~List(); //Деструктор. Далее он вынесен за класс
 void Add(int x); //Функция для добавления значений в список
 void Show(); //Функция для отображения списка на экране
 void Laba();
};
 
List::~List() //Деструктор вынесен за класс
{
    while (Head!=NULL)  //Пока по адресу не пусто 
     {    
        element *temp=Head->Next; //Временная переменная для хранения адреса следующего элемента
        delete Head; //Освобождаем адрес обозначающий начало
        Head=temp; //Меняем адрес на следующий
     }
}
 
void List::Add(int x) //Функция добавления элементов в список
{
	size++;
 element *temp=new element; //При каждом вызове выделяется память
temp->x=x; //Записываем x в элемент структуры  element (в x структуры element)
temp->Next=Head; //Указываем, что след. элемент это объект по адресу Head
Head=temp; //Указываем, что последний активный элемент это только что введенный
}
 
 
 
void List::Show() //Функция отображения списка на экране
{
  element *temp=Head; //Определяем указатель, который изначально он равен адресу начала списка
 
 
 while (temp!=NULL) //До тех пор пока не встретит пустое значение
 {
  cout<<temp->x<<" "; //Выведет элемент x из списка
  temp=temp->Next; //Указываем, что далее нам нужен следующий элемент
 }

 cout << endl;
}

void List::Laba()
{
	element *temp=Head;
	List mas1;
	for(int i = 1; i < size+1; i++)
	{ 
		if(i != 2){
			  mas1.Add(temp->x); //приравнивает значение нечетного элемента исходного массива новому	 
		}
		temp=temp->Next; //Указываем, что далее нам нужен следующий элемент
	}
	mas1.Show();
}

void main()
{
	setlocale(LC_ALL, "Russian");
	int n = 0;
	List mas;
	cout <<"введите количество элементов" << endl;
	cin >> n;
	for(int i = 0; i < n; i++)
	{
		int znach;
		cout << "Введите элемент "<< i+1 << "-ый элемент: ";
		cin >> znach;
		mas.Add(znach);
	}
	mas.Show();

	mas.Laba();


	system("pause");
}
