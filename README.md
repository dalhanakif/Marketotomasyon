# Marketotomasyon
Market otomasyon
#include <iostream>
#include <Windows.h>
#include <fstream>
using namespace std;

int al = 0, sat = 0, uruns, ts = 0, ta = 0;

struct urun {
	float kod, alis, satis;
	string isim;
};
void adet(urun);

urun ekmek, su, camasirs, kola;

void liste() {
	cout << endl << "Ekmek(1)\nSu(2)\nCamasir Suyu(3)\nKola(4)\n";
}

void alisveris() {
	int kod;
kod1:
	cout << "\nUrun kodunu giriniz:";
	cin >> kod;
	switch (kod)
	{
	case 1:
		adet(ekmek);
		break;
	case 2:
		adet(su);
		break;
	case 3:
		adet(camasirs);
		break;
	case 4:
		adet(kola);
		break;
	default:
		cout << "\nBu urun kodunda urunumuz yoktur\n";
		goto kod1;
		break;
	}
}

void adet(urun urun1) {
	int adet;
	cout << "\nKac tane " << urun1.isim << " alacaksiniz:";
	cin >> adet;
	sat += adet * urun1.satis;
	al += adet * urun1.alis;
}

void bilanco(int gun) {
	cout << endl << endl << gun << ". gunun bilancosu:\nAlinan mallarin fiyati:" << al
		<< "\nSatilan mallarin fiyati:" << sat << "\nKar:" << sat - al << endl;
}

void bilanco(int ts, int ta, int gun) {
	cout << "\n\nTOPLAM " << "BILANCO\nToplam alinan mal : " << ta << "\nToplam satilan mal : " << ts
		<< "\nKar:" << ts - ta;
}

int main() {
	system("color 71");
	Beep(2502, 308);
	char l = 12;
	cout << "Sistem aciliyor lutfen bekleyiniz" << endl;
	for (int i = 0; i < 10; i++) {
		Beep(2502, 308);
		cout << l;
	}
	int secim, gun = 1, ay = 1, aa = 0, as = 0;
	ekmek = { 1,2.1,2.5,"Ekmek" };
	su = { 2,1,1.5,"Su" };
	camasirs = { 3,15,20,"Camasir Suyu" };
	kola = { 4,10,15,"Kola" };
	cout << endl;
	cout << "----Markete Hosgeldiniz----\n\n1.GUN\n\n";
basa:
	cout << "\n1-Liste\n2-Alisveris\n3-Bilanco\n4-Gunu Bitir\n5-Isi birak\n:";
	cin >> secim;

	switch (secim)
	{
	case 1:
		liste();
		goto basa;
		break;
	case 2:
		alisveris();
		goto basa;
		break;
	case 3:
		bilanco(gun);
		void gunlukbilanco(); {
			ofstream gunB;
			gunB.open("gunB.txt", ios::app);
			gunB << gun << ".gunun bilancosu:" << sat-al<<endl;
			gunB.close();

		}
		if (gun >= 30)
		{
			cout << "\n\n" << ay << ". AY BILANCOSU\nAlinan mallar:" << aa << "\nSatilan mallar:" << as
				<< "\nKar:" << as - aa << "\n\n";
			void aylikbilanco();
			{
				ofstream aylik;
				aylik.open("aylik.txt", ios::app);
				aylik << ay<<".ayın bilancosu: " << as - aa<<endl;
				aylik.close();
			}
			gun = 0;
			as = 0;
			aa = 0;
		}
		goto basa;
		break;
	case 4:
		cout << "\n\n" << ++gun << ".GUN\n\n";
		ts += sat;
		as += sat;
		sat = 0;
		ta += al;
		aa += al;
		al = 0;
		if (gun == 1)
		{
			as = 0;
			aa = 0;
			ay++;
		}
		goto basa;
		break;
	case 5:
		break;
	default:
		cout << "\n\nOyle bir secenek yok efendim\n\n";
		goto basa;
	}
}
