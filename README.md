# sunum
huzurevindeki ilaç takip sistemi
#include <stdio.h>

#define MAX_ILAC_SAATI 50
#define kalacakMaksimumkisi 15

struct kisi {
    char isim[50];
    char soyisim[50];
    int yas;
    float kilo;
    float boy;
    float ilacsaatleri[MAX_ILAC_SAATI]; // ilaç saatlerini tutacak dizi
    int ilacSayisi; // Kullanıcının girdiği ilaç saati sayısı
};


struct kisi bilgilerial(struct kisi kisi) {
    printf("Kişinin ismini giriniz :\n ");
    scanf("%s", kisi.isim);
    printf("Kişinin soy ismini giriniz :\n ");
    scanf("%s", kisi.soyisim);
    printf("Kişinin yaşını giriniz : \n");
    scanf("%d", &kisi.yas);
    printf("Kişinin kilosunu giriniz:");
    scanf("%f",&kisi.kilo);
    printf("Kişinin boyunu giriniz:");
    scanf("%f",&kisi.boy);
    printf("İlaç saati sayısını giriniz (maksimum %d ilaç saati): ", MAX_ILAC_SAATI);
    scanf("%d", &kisi.ilacSayisi);

    // Kullanıcı 50'den fazla ilaç saati girmesini engelliyoruz
    if (kisi.ilacSayisi > MAX_ILAC_SAATI) {
        printf("Maksimum %d ilaç saati girebilirsiniz. Bu değeri %d olarak kabul ediyoruz.\n", MAX_ILAC_SAATI, MAX_ILAC_SAATI);
      
        
        kisi.ilacSayisi = MAX_ILAC_SAATI;
    }

    // İlaç saatlerini kullanıcıdan alıyoruz
    printf("İlaç saatlerini giriniz:\n");
    for (int i = 0; i < kisi.ilacSayisi; i++) {
        printf("İlaç saati %d: ", i + 1);
        scanf("%f", &kisi.ilacsaatleri[i]);
    }

    return kisi;
}

void bilgileriYazdir(struct kisi kisi) {
    printf("Kişinin bilgileri:\n");
    printf("Adı: %s\n", kisi.isim);
    printf("Soyadı: %s\n", kisi.soyisim);
    printf("Yaşı: %d\n", kisi.yas);
    printf("kilosu: %f\n",kisi.kilo);
    printf("Boyu: %f\n",kisi.boy);
    printf("İlaç saatleri: ");
    for (int i = 0; i < kisi.ilacSayisi; i++) {
        printf("%f ", kisi.ilacsaatleri[i]);
    }
    printf("\n");
}

void ilacSaatiBildirim(struct kisi kisi, int ilacsaati) {
    // İlaç saati geldiğinde bildirim yapalım
    for (int i = 0; i < kisi.ilacSayisi; i++) {
        if (kisi.ilacsaatleri[i] == ilacsaati) {
            printf("Dikkat! %s %s, ilaç saatiniz geldi! Saat: %d\n", kisi.isim, kisi.soyisim, ilacsaati);
        }
    }
}

int main() {
    int n;
    float ilacsaati;
    
    // Kullanıcıdan saat bilgisi alalım
    printf("Şu anki saati giriniz (0-23 arası): ");
    scanf("%f", &ilacsaati);

    if (ilacsaati < 0 || ilacsaati > 23) {
        printf("Geçersiz saat girişi!\n");
        return 1;
    }

    printf("Huzurevinde kalan kişi sayısını giriniz (maksimum %d kişi): ", kalacakMaksimumkisi);
    scanf("%d", &n);

    if (n > kalacakMaksimumkisi) {
        printf("Maksimum %d kişi girebilirsiniz.\n", kalacakMaksimumkisi);
        return 1;
    }

    struct kisi kisi[kalacakMaksimumkisi]; // En fazla 15 kişi alabiliriz

    for (int i = 0; i < n; i++) {
        printf("Kişi %d'nin bilgilerini giriniz:\n", i + 1);
        kisi[i] = bilgilerial(kisi[i]);
    }

    printf("\nGirdiğiniz kişilerin bilgileri:\n");
    for (int i = 0; i < n; i++) {
        bilgileriYazdir(kisi[i]);
        // İlaç saati bildirimlerini kontrol edelim
        ilacSaatiBildirim(kisi[i], ilacsaati);
    }

    return 0;
}
