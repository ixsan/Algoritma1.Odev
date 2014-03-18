#include "stdio.h"
#include "string.h"
#include "stdlib.h"
#include "ctype.h"
struct telefon{//Ana Struct olarak belirledim.
	char ad[10];
	char soyad[10];
	char ev_tel[12];
	char cep_tel[12];
	char iş_tel[12];
	char email[30];
	char bina[10];
	char daire[10];
}sayilar[100];
struct telefon2{//Kopyalanacak Olan Struct
	char ad[10];
	char soyad[10];
	char ev_tel[12];
	char cep_tel[12];
	char iş_tel[12];
	char email[30];
	char bina[10];
	char daire[10];
}sayilar2;
void goruntule();//Fonksiyonlar
void kisi_ekle();
void kisi_guncelle();
void kisi_sil();
void kisi_ara();
int secim(void);
int secim2(void);
int secim3(void);
int secim4(void);

int main()
{
	int sec;
	printf("1-Goruntule\n2-Kisi Ekle\n3-Kisi Guncelle\n4-Kisi Sil\n5-Kisi Ara\n0-Cikis\nSecim:");
	
	while((sec=secim())!=0){//Secim fonksiyonu ile secim yaptırdım
	
		
			
			switch(sec){
			case 1:system("cls");
				goruntule();
				break;
			case 2:system("cls");
				kisi_ekle();
				break;
			case 3:system("cls");
				kisi_guncelle();
				break;
			case 4:system("cls");
				kisi_sil();
				break;
			case 5:system("cls");
				kisi_ara();
				break;
			default:system("cls");
				printf("Tanimlanmayan Tus");
				main();
				break;
			}
			
			printf("1-Goruntule\n2-Kisi Ekle\n3-Kisi Guncelle\n4-Kisi Sil\n5-Kisi Ara\n0-Cikis\nSecim:");
	
		
	}
	

	return 0;
}

void goruntule()
{
	int i=0,a=0;
	FILE *bPtr;
	printf("AD\tSoyad\tEv Telefon\tCep Telefon\tIs Telefon\t\tEmail\t\t\tAdres\n");
	printf("--\t-----\t----------\t-----------\t----------\t\t-----\t\t\t-----");
	fopen_s(&bPtr,"ihsan.txt","r");//Dosyayı okuma modunda açtım
	
	while(!feof(bPtr)){
		//Dosyayı sonuna kadar okutup dizilere atadım
		fscanf(bPtr,"%s%s%s%s%s%s%s%s",sayilar[i].ad,sayilar[i].soyad,sayilar[i].ev_tel,sayilar[i].cep_tel,sayilar[i].iş_tel,sayilar[i].email,sayilar[i].bina,sayilar[i].daire);
		
		i++;
	}
	fclose(bPtr);
	
	for(int b=0;b<(i-1);b++)//Dosyadaki dizi sayısı kadar döndürdüm
	{
		for(int j=0;j<(i-2-b);j++)
		{
			if(strcmp(sayilar[j].ad,sayilar[j+1].ad)>=0)//Ondemi arkadamı kontrolü yaptım
			{

				memcpy(&sayilar2,&sayilar[j+1],sizeof(telefon));//Burada ana struct ı kopya structa kopyalayıp yer değiştirme fonksiyonu uyguladım.
				memcpy(&sayilar[j+1],&sayilar[j],sizeof(telefon));
				memcpy(&sayilar[j],&sayilar2,sizeof(telefon));

			}
		}
	}
	fopen_s(&bPtr,"ihsan.txt","w");//Sıralamayı yaptıktan sonra dosyayı boş bir şekilde açtım
	for(a=0;a<(i-1);a++)// Döngü ile hepsini tekrar dosyaya sıralı şekilde yazdım
		fprintf(bPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\t\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
	for(int z=0;z<(i-1);z++)// Sıralı şekilde bilgileri ekrana yazdırdım
		printf("\n%s\t%s\t%s\t%s\t%s\t%s\t\t%s/%s\t\n",sayilar[z].ad,sayilar[z].soyad,sayilar[z].ev_tel,sayilar[z].cep_tel,sayilar[z].iş_tel,sayilar[z].email,sayilar[z].bina,sayilar[z].daire);
	
	getchar();
	fclose(bPtr);// Dosyayı Kapattım
	
}

void kisi_ekle()
{
	int i=0;
	char secim;
	FILE *bPtr;
	fopen_s(&bPtr,"ihsan.txt","a");//Dosyayı Yazma modunda açtım
	
	do{//Şart devam ettiği sürece yeni üye kaydı devam ediyor
	printf("Yeni Kisinin\n------------\nAd:");
	fflush(stdin);
	gets_s(sayilar[i].ad);
	printf("\nSoyad:");
	gets_s(sayilar[i].soyad);
	printf("\nEv Telefon<0>:");
	gets_s(sayilar[i].ev_tel);
	printf("\nCep Telefon<0>:");
	gets_s(sayilar[i].cep_tel);
	printf("\nIs Telefon<0>:");
	gets_s(sayilar[i].iş_tel);
	printf("\nEmail:");
	gets_s(sayilar[i].email);
	printf("\nAdres Bilgileri");
	printf("\nBina:");
	gets_s(sayilar[i].bina);
	printf("\nDaire:");
	gets_s(sayilar[i].daire);
	fprintf(bPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[i].ad,sayilar[i].soyad,sayilar[i].ev_tel,sayilar[i].cep_tel,sayilar[i].iş_tel,sayilar[i].email,sayilar[i].bina,sayilar[i].daire);
	i++;}while((secim=secim2())!='H');//Fonksiyonda H || h tuşuna basılmadığı sürece döngü devam ediyor
	system("CLS");//Ekranı temizledim
	
	fclose(bPtr);	
	goruntule();// Yeni durum için goruntule fonksiyonuna yolladım
}

void kisi_guncelle()
{
	FILE *bPtr,*cPtr;
	int i=0,secim;
	goruntule();//ilk önce rehberi görüntüledim 
	char aranan_isim[10],aranan_soy[10];//aranacak olan kişinin isim ve soyismi
	fopen_s(&bPtr,"ihsan.txt","r");//Ana dosyayı okuma modunda açtım
	fopen_s(&cPtr,"ihsan3.txt","w");//Aktarılacak olan dosyayı 0'dan yazma modunda açtım
	

	printf("\nDegistirilecek Isim:");//ismi ve soyismi aldım
	_flushall();
	gets_s(aranan_isim);
	printf("Soyisim:");
	_flushall();
	gets_s(aranan_soy);

	while(!feof(bPtr))
	{
		//dosyayı sonuna kadar okutup diziye atadım
		fscanf(bPtr,"%s%s%s%s%s%s%s%s",sayilar[i].ad,sayilar[i].soyad,sayilar[i].ev_tel,sayilar[i].cep_tel,sayilar[i].iş_tel,sayilar[i].email);
		i++;
	}
	for(int a=0;a<(i-1);a++)//dizideki eleman sayısı kadar döndürdüm
	{
		if(strstr(sayilar[a].ad,aranan_isim))//aranan isim ile dizideki ad aynımı kontrolü
		{
			if(strstr(sayilar[a].soyad,aranan_soy))//adanan soyad ile dizideki soyad aynımı kontrolü
			{
				secim=secim3();//aynı ile secim fonksiyonuna yolladım
				if(secim==1)//isim değişikliği
				{
					printf("\nYeni Ad:");
					fflush(stdin);
					gets_s(sayilar[a].ad);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
				
				}
				if(secim==2)//soyad değişikliği
				{
					printf("\nYeni Soyad:");
					fflush(stdin);
					gets_s(sayilar[a].soyad);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==3)//ev telefonu değişikliği
				{
					printf("\nYeni Ev Telefon<0>:");
					fflush(stdin);
					gets_s(sayilar[a].ev_tel);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==4)//cep telefonu değişikliği
				{
					printf("\nYeni Cep Telefon<0>:");
					fflush(stdin);
					gets_s(sayilar[a].cep_tel);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==5)//iş telefonu değişikliği
				{
					printf("\nYeni Is Telefon<0>:");
					fflush(stdin);
					gets_s(sayilar[a].iş_tel);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==6)//email değişikliği
				{
					printf("\nYeni Email:");
					fflush(stdin);
					gets_s(sayilar[a].email);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==7)//adres değişikliği
				{
					printf("\nYeni Bina:");
					fflush(stdin);
					gets_s(sayilar[a].bina);
					printf("\nYeni Daire:");
					gets_s(sayilar[a].daire);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
					
				}
				if(secim==8)//tüm bilgilerin değişikliği
				{
					printf("\nYeni Ad:");
					fflush(stdin);
					gets_s(sayilar[a].ad);
					printf("\nYeni Soyad:");
					gets_s(sayilar[a].soyad);
					printf("\nYeni Ev Telefon<0>:");
					gets_s(sayilar[a].ev_tel);
					printf("\nYeni Cep Telefon<0>:");
					gets_s(sayilar[a].cep_tel);
					printf("\nYeni Is Telefon<0>:");
					gets_s(sayilar[a].iş_tel);
					printf("\nYeni Email:");
					gets_s(sayilar[a].email);
					printf("\nYeni Bina:");
					gets_s(sayilar[a].bina);
					printf("\nYeni Daire:");
					gets_s(sayilar[a].daire);
					fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
				}
			}
			else
				fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
	
		}
		else
			fprintf(cPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
	
	}
	
	fclose(bPtr);//Dosyaları kapattım
	fclose(cPtr);
	remove("ihsan.txt");//Ana dosyayı sildim
	rename("ihsan3.txt","ihsan.txt");//Kopyalanan dosyanın adını ana dosyanın adı yaptım
	system("cls");//Ekranı temizleyip görüntüledim
	printf("YENI  DURUM\n");
	goruntule();

}

void kisi_sil()
{
	FILE *bPtr,*yeniPtr;
	char silinecek_isim[10],silinecek_soy[10],secim;//Silinecek isim ve soyisim
	int i=0;
	goruntule();//ik önce rehberi görüntüledim
	printf("\nSilinecek Olan Isim:");//isim ve soyismi aldım
	_flushall();
	gets_s(silinecek_isim);
	printf("Soyisim:");
	_flushall();
	gets_s(silinecek_soy);

	fopen_s(&bPtr,"ihsan.txt","r");//ana dosyayı okuma modunda açtım
	fopen_s(&yeniPtr,"ihsan2.txt","w");//kopyalanacak dosyayı 0'dan yazma modunda açtım

	while(!feof(bPtr))
	{
		//dosyayı sonuna kadar taratıp diziye atadım
		fscanf(bPtr,"%s%s%s%s%s%s%s%s",sayilar[i].ad,sayilar[i].soyad,sayilar[i].ev_tel,sayilar[i].cep_tel,sayilar[i].iş_tel,sayilar[i].email,sayilar[i].bina,sayilar[i].daire);
		i++;
	}

	for(int a=0;a<i;a++)//dizi eleman sayısı kadar döndürdüm
	{
		if(strstr(sayilar[a].ad,silinecek_isim) && strstr(sayilar[a].soyad,silinecek_soy))//isim ve soyisim karşılaştırmalarının ikiside sağlanırsa
		{//sec,m fonksiyonuna girip emin mi değilmi kontrolü yaptırdım
			secim=secim2();
			if(secim=='H')//emin değilse(H) yazdırıyor 
				fprintf(yeniPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
		
		}
		else
			fprintf(yeniPtr,"%s\t%s\t%s\t%s\t%s\t%s\t%s\t%s\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
	
	}
	fclose(bPtr);//dosyaları kapattım
	fclose(yeniPtr);

	remove("ihsan.txt");//ana dosyayı sildim
	rename("ihsan2.txt","ihsan.txt");//Kopyalanan dosyayı ana dosyayla aynı ada çevirdim
	system("cls");// Ekranı temizleyip Goruntuledim
	printf("YENI DURUM\n");
	goruntule();
}

void kisi_ara()
{
	int i=0,secim;
	char ara[20],bina[20];
	FILE *bPtr;

	fopen_s(&bPtr,"ihsan.txt","r");//Dosyayı okuma modunda açtım
	while(!feof(bPtr))
	{//Dosyayı sonuna kadar taratıp dizi elemanlarına atadım
		fscanf(bPtr,"%s%s%s%s%s%s%s%s",sayilar[i].ad,sayilar[i].soyad,sayilar[i].ev_tel,sayilar[i].cep_tel,sayilar[i].iş_tel,sayilar[i].email,sayilar[i].bina,sayilar[i].daire);
		i++;
	}

	secim=secim4();
	if(secim==1){
		printf("Aranan Isim:");//Aranan ismi aldım
		_flushall();
		gets_s(ara);
		
		printf("AD\tSoyad\tEv Telefon\tCep Telefon\tIs Telefon\t\tEmail\t\t\tAdres\n");
		printf("--\t-----\t----------\t-----------\t----------\t\t-----\t\t\t-----");
	
		for(int a=0;a<(i-1);a++)//dizi sonuna kadar döndürdüm
		{
			if(strstr(sayilar[a].ad,ara))//aranan kelime ad kelimesinde varsa Yazdırdım
			{		
				printf("\n%s\t%s\t%s\t%s\t%s\t%s\t\t%s/%s\t\n",sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email,sayilar[a].bina,sayilar[a].daire);
			}

		}
	}
	if(secim==2){
		printf("Aranan Bina:");//Aranan adres aldım
		_flushall();
		gets_s(bina);

			printf("Adres\tAD\tSoyad\tEv Telefon\tCep Telefon\tIs Telefon\tEmail\t\n");
			printf("-----\t--\t-----\t----------\t-----------\t----------\t-----\t\n");
		for(int a=0;a<(i-1);a++)//dizi sonuna kadar döndürdüm
		{
			if(strstr(sayilar[a].bina,bina))//aranan kelime bina kelimesinde varsa Yazdırdım
			{
				printf("\n%s/%s\t%s\t%s\t%s\t%s\t%s\t%s\t\n",sayilar[a].bina,sayilar[a].daire,sayilar[a].ad,sayilar[a].soyad,sayilar[a].ev_tel,sayilar[a].cep_tel,sayilar[a].iş_tel,sayilar[a].email);
	
			}

		}
	}
	
	fclose(bPtr);//Dosyayı kapattım
}

int secim(void)
{
	int secim;
	scanf_s("%d",&secim);
	return secim;
}

int secim2(void)
{
	char secim;
	printf("Devam Etmek Icin E/H");
	scanf_s("%c",&secim);
	secim=toupper(secim);
	return secim;
}

int secim3(void)
{
	int secim;
	printf("1-Isim Degisikligi\n2-Soyad Degisikligi\n3-EvTel Degisikligi\n4-Ceptel Degisikligi\n5-IsTel Degisikligi\n6-EmailDegisikligi\n7-Adres Degisikligi\n8-Tum Bilgilerin Degisikligi\nSecim:");
	scanf_s("%d",&secim);

	return secim;
}

int secim4(void)
{
	int secim;
	printf("1-Isme Gore Ara:\n2-Adrese Gore Ara:\nSecim:");
	scanf_s("%d",&secim);
	system("CLS");
	return secim;
}
