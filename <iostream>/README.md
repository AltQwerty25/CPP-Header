Ringkasan / Sinopsis
```cpp
namespace std {
    extern istream cin;
    extern ostream cout;
    extern ostream cerr;
    extern ostream clog;
    extern wistream wcin;
    extern wostream wcout;
    extern wostream wcerr;
    extern wostream wclog;
}
```

Sertakan header standar iostreams <iostream> untuk mendeklarasikan objek yang mengontrol pembacaan dari dan penulisan ke stream standar. 
Ini seringkali merupakan satu-satunya header yang perlu Anda sertakan untuk melakukan input dan output dari program C++.
  
Obyek terbagi menjadi dua kelompok:
berorientasi byte, melakukan transfer byte-at-a-time konvensional
- cin
- cout
- cerr
- clog
  
berorientasi luas, menerjemahkan juga dan dari karakter luas yang dimanipulasi oleh program secara internal
- wcin
- wcout
- wcerr
- wclog
  
Setelah Anda melakukan operasi tertentu pada aliran, seperti input standar, Anda tidak dapat melakukan operasi dengan orientasi berbeda pada aliran yang sama. 
Oleh karena itu, sebuah program tidak dapat beroperasi secara bergantian pada cin dan wcin, misalnya.
  
Semua objek yang dideklarasikan di header ini memiliki properti yang sama — Anda dapat menganggap objek tersebut dibuat sebelum objek statis apa pun yang Anda tentukan, di unit terjemahan yang menyertakan <iostreams>. 
Sama halnya, Anda dapat mengasumsikan bahwa objek ini tidak dihancurkan sebelum destruktor untuk objek statis apa pun yang Anda tentukan. 
(Namun, aliran keluaran dibilas selama penghentian program.) Oleh karena itu, Anda dapat dengan aman membaca dari atau menulis ke aliran standar sebelum memulai program dan setelah penghentian program.

Namun, jaminan ini tidak universal. Konstruktor statis dapat memanggil fungsi di unit terjemahan lain. 
Fungsi yang dipanggil tidak dapat berasumsi bahwa objek yang dideklarasikan dalam header ini telah dibuat, mengingat urutan yang tidak pasti di mana unit terjemahan berpartisipasi dalam konstruksi statis. 
Untuk menggunakan objek ini dalam konteks seperti itu, Anda harus membuat objek kelas ios_base::Init terlebih dahulu, seperti pada:
  
```cpp
#include <iostream>
void marker()
    {    
        ios_base::Init unused_name;
        cout << “called fun” << endl;
    }
```
  
### contoh:
  
```cpp
#include <iostream>
#include <fstream>

using namespace std;

void TestWide( )
{
   int i = 0;
   wcout << L"Enter a number: ";
   wcin >> i;
   wcerr << L"test for wcerr" << endl;
   wclog << L"test for wclog" << endl;
}

int main( )
{
   int i = 0;
   cout << "Enter a number: ";
   cin >> i;
   cerr << "test for cerr" << endl;
   clog << "test for clog" << endl;
   TestWide( );
}
```

```cpp
#include <iostream>
using namespace std;

int main()
{
   int x;
   cout << "enter choice:";
   cin >> x;
   while (x < 1 || x > 4)
   {
      cout << "Invalid choice, try again:";
      cin >> x;
      // not a numeric character, probably
      // clear the failure and pull off the non-numeric character
      if (cin.fail())
      {
         cin.clear();
         char c;
         cin >> c;
      }
   }
}
```
