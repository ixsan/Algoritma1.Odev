Algoritma1.Odev
===============

12253051_Ihsan_ONAL

#include <stdio.h>
#include <conio.h>
#include <string.h>
int main()
{/*Sifreleme Kismı*/
	int sifre1,sifre=1234;
	int x, sonuc;
	

		printf("Kullanici Sifren:");
		scanf("%d",&sifre1);
		if(sifre==sifre1){
			printf("Sifre Dogru\n");
		/*Menu Kismi*/
		int secim , Sonuc , x=500 , y , z , a ,b=500,c=500,d=500 , sonuc, sonuc1, sonuc2,sonuc3;
			printf("1-Hesap Durumu\n2-Para Cekme\n3-Para Yatirma\n4-Para Gonderme\n\n");
			scanf("%d",&secim);


			switch (secim)
			{

				case 1:
					sonuc=x;
						printf("Hesap Bakiyeniz=%d\n",sonuc);
						break;
				case 2:
					
					
					
						printf("Cekmek Istediginiz Tutar=\n");
						scanf("%d",&y);
						sonuc1=b-y;
						
						printf("Kalan Tutar=%d\n",sonuc1);
						break;
				case 3:
				
					
						printf("Yatırmak Istediginiz Tutar=\n");
						scanf("%d",&z);
							sonuc2=c+z;
							printf("Bakiyeniz %d TL oldu",sonuc2);
						break;
				case 4:
					
					
					
						printf("Gondermek Isteginiz Tutar=");
						scanf("%d",&a);
						sonuc3=d-a;
						
						printf("Kalan tutar =%d\n",sonuc3);
						break;
				default:
					printf("Yanlis Secim Yaptiniz!!");
			}


		}else{

			printf("Sifre Yanlis\n");
			
		}
		getche();
		

}
