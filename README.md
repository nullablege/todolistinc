# 📝 Bağlı Liste Tabanlı To-Do List Uygulaması (C ile)

![C Programlama Dili Logosu](https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/C_Programming_Language.svg/1200px-C_Programming_Language.svg.png)
![Veri Yapıları İkonu](https://static.thenounproject.com/png/1326874-200.png) <!-- Genel bir veri yapıları ikonu -->

Bu **To-Do List uygulaması**, görevlerinizi etkin bir şekilde yönetmenize yardımcı olmak için tasarlanmıştır. Tamamen **C programlama dili** kullanılarak geliştirilmiş olup, görevleri saklamak ve yönetmek için temel bir veri yapısı olan **bağlı listeler (linked lists)** üzerine kuruludur. Bağlı listeler, verimli ekleme ve silme işlemleri için bilgisayar bilimlerinde hayati öneme sahiptir ve bu uygulama, bu işlemlerin pratik bir gösterimini sunar.

Bu projenin temel amacı, **veri yapıları ve algoritmalar** konusundaki bilgi ve yeterliliği kanıtlamaktır. Uygulama, komut satırı arayüzü (CLI) üzerinden kullanıcıyla etkileşim kurar ve görevlerin oluşturulması, görüntülenmesi, silinmesi, aranması, filtrelenmesi ve kalıcı olarak bir dosyaya kaydedilmesi gibi temel işlevleri sunar.

---

## 🌟 Temel Özellikler ve Fonksiyonlar

*   **Görev Oluşturma (`gorevolustur`):**
    *   Her bir görev için Başlık, Açıklama, Son Tarih, Durum (örn: "Başlamadı", "Devam Ediyor", "Tamamlandı"), İlerleme Yüzdesi (%) ve Öncelik durumu gibi detaylı bilgilerle yeni görevler ekleyebilirsiniz.
    *   Oluşturulan her göreve, o anki sistem zamanı kullanılarak otomatik bir `yapilistarihi` (oluşturulma tarihi) atanır (`time(NULL)`).
*   **Görev Görüntüleme (`listegoruntule`, `sirayagoregoster`):**
    *   Mevcut tüm görevlerin başlıklarını numaralandırılmış bir liste halinde görüntüleyebilirsiniz.
    *   Belirli bir sıradaki görevin tüm detaylarını (başlık, açıklama, son tarih, durum, ilerleme, öncelik) görüntüleyebilirsiniz.
*   **Görev Silme (`sil`):**
    *   Listeden, sıra numarasını belirterek belirli bir görevi kalıcı olarak silebilirsiniz.
    *   Silme işlemi, bağlı listenin başından, ortasından veya sonundan eleman çıkarma mantığını doğru bir şekilde uygular.
*   **Arama ve Filtreleme (`arama`, `tariharama`, `oncelikarama`):**
    *   Görevleri **başlıklarına göre** arayabilirsiniz. Eşleşen tüm görevler detaylarıyla listelenir.
    *   Görevleri **son tarihlerine göre** filtreleyebilirsiniz.
    *   Görevleri **öncelik durumlarına göre** filtreleyebilirsiniz.
*   **Otomatik Temizleme (`otosil` - Konsept):**
    *   Belirli bir zaman eşiğini (örneğin, 1 saniye - kodda bu şekilde ayarlanmış, ancak gerçekçi bir süre için daha uzun olmalıdır) aşan görevleri otomatik olarak listeden kaldırır. **Not:** Bu fonksiyonun mevcut implementasyonunda `free(gecici); free(onceki);` satırları döngü dışında ve potansiyel olarak hatalı bir mantıkla yerleştirilmiştir. Listenin başından silme ve diğer durumlar için dikkatli bir bellek yönetimi ve işaretçi güncellemesi gereklidir.
*   **Veri Kalıcılığı (Dosya İşlemleri - `listeyikaydet`, `listeoku`):**
    *   Mevcut görev listesini `213ToDoList.txt` adlı bir metin dosyasına **virgülle ayrılmış değerler (CSV benzeri format)** olarak kaydeder.
    *   Uygulama her başladığında, `213ToDoList.txt` dosyasını okuyarak daha önce kaydedilmiş görevleri bellekteki bağlı listeye yükler.
    *   Dosya işlemleri sırasında (`fopen`, `fprintf`, `fscanf`, `fclose`) temel hata kontrolleri (dosya açılamazsa) yapılır.
*   **Dinamik Bellek Yönetimi:**
    *   Yeni görevler oluşturulurken `malloc()` fonksiyonu ile dinamik olarak bellek ayrılır.
    *   Görevler silindiğinde veya otomatik temizleme yapıldığında ayrılan belleğin `free()` ile serbest bırakılması (mevcut `otosil` fonksiyonunda dikkatli olunması gereken nokta).
*   **Bağlı Liste Veri Yapısı Kullanımı:**
    *   Uygulamanın kalbinde `struct liste` yapısı ve bu yapıdan oluşan tek yönlü bir bağlı liste (`kafa` işaretçisi ile yönetilen) bulunur.
    *   Her bir düğüm (görev), veri alanlarını (başlık, açıklama vb.) ve bir sonraki düğüme bir işaretçi (`sonraki`) içerir.
    *   Bu yapı, görevlerin eklenmesi ve silinmesi sırasında verimli dinamik bellek kullanımı ve kolay düğüm manipülasyonu sağlar.
*   **Kullanıcı Etkileşimli Menü:**
    *   Komut satırı üzerinden kullanıcıya sunulan basit ve anlaşılır bir menü aracılığıyla tüm işlemler gerçekleştirilir.
    *   Kullanıcı girdileri `scanf` ve `gets` (dikkat: `gets` güvenli değildir, buffer overflow riski taşır, `fgets` tercih edilmelidir) ile alınır.
*   **Hata Yönetimi (Temel):**
    *   Dosya açma hataları (`kayitliliste==NULL`).
    *   Listede olmayan bir görevi silmeye veya görüntülemeye çalışırken bilgilendirme mesajları.
    *   Geçersiz kullanıcı girdilerine karşı temel yönlendirmeler.

---

## 🛠️ Kullanılan Teknolojiler ve Kavramlar

*   **Programlama Dili:** C
*   **Temel Veri Yapısı:** Tek Yönlü Bağlı Liste (Singly Linked List)
*   **Temel Algoritmalar:**
    *   Bağlı listeye eleman ekleme (sona ekleme).
    *   Bağlı listeden eleman silme (belirli bir pozisyondaki elemanı silme).
    *   Bağlı listede arama (doğrusal arama).
    *   Bağlı listeyi dolaşma (traversal).
*   **C Standart Kütüphaneleri:**
    *   `stdio.h`: Standart giriş/çıkış işlemleri için (`printf`, `scanf`, `fopen`, `fprintf`, `fscanf`, `fclose`, `gets`, `getchar`).
    *   `stdlib.h`: Bellek yönetimi (`malloc`, `free`), program sonlandırma (`exit`) gibi genel yardımcı fonksiyonlar için.
    *   `string.h`: String manipülasyonu için (`strcpy`, `strcmp`).
    *   `time.h`: Zamanla ilgili işlemler için (`time_t`, `time`).
*   **Bellek Yönetimi:** Dinamik bellek ayırma (`malloc`) ve serbest bırakma (`free`).
*   **Dosya G/Ç:** Metin dosyalarına veri yazma ve okuma.

---

## 📁 Proje Dosya Yapısı

```
todolistinc/
├── README.md # Bu dosya
└── TodoList.c # Ana C kaynak kodu (main fonksiyonu ve tüm listeleme işlemleri)
└── 213ToDoList.txt # Program çalıştırıldığında görevlerin kaydedileceği/okunacağı dosya (otomatik oluşur)
```


---

## ⚙️ Derleme ve Çalıştırma

Bu C uygulamasını derlemek ve çalıştırmak için aşağıdaki adımları izleyebilirsiniz:

1.  **C Derleyicisi:**
    *   Sisteminizde bir C derleyicisinin (örneğin, GCC - GNU Compiler Collection) kurulu olduğundan emin olun. Linux ve macOS sistemlerinde genellikle varsayılan olarak gelir. Windows için MinGW veya Cygwin gibi ortamları kurabilirsiniz.

2.  **Kaynak Kodunu Kaydetme:**
    *   Yukarıda paylaşılan C kodunu `TodoList.c` (veya farklı bir `.c` uzantılı dosya) olarak bilgisayarınıza kaydedin.

3.  **Derleme:**
    *   Bir terminal veya komut istemcisi açın.
    *   Kaynak kodunun kaydedildiği dizine gidin (`cd path/to/your/code`).
    *   Aşağıdaki komutu kullanarak kodu derleyin (GCC için örnek):
        ```bash
        gcc TodoList.c -o todolist
        ```
        Bu komut, `TodoList.c` dosyasını derleyerek `todolist` (veya Windows'ta `todolist.exe`) adında çalıştırılabilir bir dosya oluşturacaktır.

4.  **Uygulamamayı Çalıştırma:**
    *   Derleme işlemi başarıyla tamamlandıktan sonra, uygulamayı aşağıdaki komutla çalıştırın:
        *   Linux/macOS için:
            ```bash
            ./todolist
            ```
        *   Windows için:
            ```bash
            todolist.exe
            ```
    *   Uygulama başlayacak ve size komut satırında bir menü sunacaktır. Bu menü üzerinden görevlerinizi yönetebilirsiniz.

---

## 💻 Uygulama ile Etkileşim

Uygulama başlatıldığında size aşağıdaki gibi bir ana menü sunulacaktır:

1.  **Listenizi Goruntuleyin:** Mevcut tüm görevlerin başlıklarını listeler.
2.  **Yeni Gorev Olusturun:** Yeni bir görev eklemek için sizden başlık, açıklama, son tarih, durum, ilerleme yüzdesi ve öncelik bilgilerini girmenizi ister.
3.  **Gorev Silin:** Mevcut görevleri listeler ve silmek istediğiniz görevin sıra numarasını girmenizi ister.
4.  **Arama / Filtreleme Yapin:** Alt menü sunar:
    *   Başlığa Göre Arama
    *   Son Tarihe Göre Arama
    *   Önceliğe Göre Filtreleme
5.  **Kaydedip Cikis Yapin:** Mevcut görev listesini `213ToDoList.txt` dosyasına kaydeder ve uygulamadan çıkar.

---

## 🧠 Kodun Teknik Detayları ve Veri Yapısı

*   **`struct liste` Yapısı:**
    *   Her bir görevi temsil eder. İçerisinde görevin başlığı, açıklaması, son tarihi, durumu, ilerleme yüzdesi, önceliği, oluşturulma tarihi (`time_t yapilistarihi`) ve bir sonraki göreve işaret eden bir gösterici (`struct liste* sonraki`) bulunur. Bu, tek yönlü bir bağlı listenin temel düğüm yapısıdır.
*   **`kafa` (Head) İşaretçisi:**
    *   `struct liste* kafa = NULL;` global değişkeni, bağlı listenin başlangıcını (ilk düğümü) işaret eder. Başlangıçta `NULL` olması listenin boş olduğunu gösterir.
*   **Fonksiyonlar:**
    *   **`listeyikaydet(FILE *kayitliliste)`:** Bağlı listedeki tüm görevleri dolaşır ve her bir görevin bilgilerini belirtilen dosyaya virgülle ayırarak yazar.
    *   **`listeoku(FILE* kayitliliste)`:** Uygulama başladığında dosyadan görev bilgilerini okur (`fscanf`), her bir satırı ayrıştırır ve bu bilgilerle yeni görevler oluşturarak (`gorevolustur` çağrısıyla) bağlı listeyi yeniden inşa eder.
    *   **`listegoruntule()`:** Listenin başından sonuna kadar tüm görevleri dolaşır ve başlıklarını ekrana yazdırır.
    *   **`gorevolustur(...)`:** Yeni bir görev için `malloc` ile bellek ayırır, gelen parametrelerle görev bilgilerini doldurur ve bu yeni görevi bağlı listenin **sonuna** ekler.
    *   **`sil(int silinecek)`:** Belirtilen sıra numarasındaki görevi listeden siler. İlk elemanı silme, aradan bir elemanı silme gibi durumları doğru şekilde ele alır.
    *   **`sirayagoregoster(int sira)`:** Belirtilen sıra numarasındaki görevin tüm detaylarını ekrana yazdırır.
    *   **`arama(char *baslik)`, `tariharama(char *tarih)`, `oncelikarama(char *oncelik)`:** İlgili kritere göre listeyi dolaşır ve eşleşen görev(ler)in detaylarını gösterir. `strcmp` ile string karşılaştırması yapar.
    *   **`otosil()`:** (Kritik not: Bu fonksiyonun mevcut implementasyonunda mantıksal hatalar ve bellek sızıntısı/çift serbest bırakma riski bulunmaktadır. Özellikle `free(gecici); free(onceki);` satırları döngü dışında ve yanlış bir şekilde yer almaktadır. Düğüm silme işlemi yapılırken, bir sonraki düğüme geçmeden önce `gecici` düğümü `free` edilmeli ve `onceki->sonraki` doğru şekilde ayarlanmalıdır. Baştan silme (`kafa` düğümü) ayrı ele alınmalıdır.)

---

## ⚠️ Önemli Notlar ve Güvenlik Hususları

*   **`gets()` Fonksiyonu Tehlikesi (Çok Önemli):** `main` fonksiyonu içinde ve diğer bazı yerlerde kullanıcıdan string girdisi almak için `gets()` fonksiyonu kullanılmıştır. **`gets()` fonksiyonu buffer overflow (tampon taşması) zafiyetine yol açtığı için son derece tehlikelidir ve asla kullanılmamalıdır.** Bunun yerine, girdi alınacak maksimum karakter sayısını belirtebilen `fgets(buffer, sizeof(buffer), stdin);` fonksiyonu kullanılmalıdır. `fgets` ile alınan stringin sonundaki newline karakteri (`\n`) de ayrıca temizlenmelidir.
*   **Bellek Yönetimi:**
    *   `malloc` ile ayrılan belleğin, görev silindiğinde veya uygulama sonlandığında (liste kaydedildikten sonra) `free` ile düzgün bir şekilde serbest bırakılması kritik öneme sahiptir. Mevcut `otosil()` fonksiyonundaki bellek yönetimi hatalıdır ve düzeltilmelidir. Uygulama kapanırken tüm liste `free` edilmelidir.
    *   `fopen` ile açılan dosyaların `fclose` ile kapatılması önemlidir, bu genellikle yapılmış görünüyor.
*   **Hata Kontrolleri:** `malloc` başarısız olursa `NULL` döner; bu durum kontrol edilmelidir. `scanf` gibi fonksiyonların dönüş değerleri kontrol edilerek kullanıcının geçerli bir giriş yapıp yapmadığı teyit edilebilir.
*   **String Alan Boyutları:** `struct liste` içindeki `char` dizilerinin (baslik, aciklama vb.) boyutları sabittir. Kullanıcı bu boyutlardan daha uzun bir girdi yapmaya çalışırsa buffer overflow oluşabilir. `fgets` ile kontrollü okuma bu riski azaltır.
*   **Kullanıcı Deneyimi:** Komut satırı arayüzü temel düzeydedir. Tarih formatları, durum seçenekleri gibi konularda kullanıcıya daha fazla rehberlik sağlanabilir.

---

## 🚀 Gelecekteki Geliştirmeler İçin Fikirler

*   **`fgets()` Kullanımı:** Tüm `gets()` ve potansiyel olarak güvensiz `scanf` kullanımlarını `fgets()` ile değiştirmek ve girdi temizliği yapmak (en öncelikli).
*   **Robust Bellek Yönetimi:** Özellikle `otosil()` fonksiyonunu düzeltmek ve uygulama kapanırken tüm dinamik belleği serbest bırakmak.
*   **Görev Güncelleme İşlevi:** Mevcut bir görevin detaylarını (başlık, açıklama, durum vb.) değiştirebilme özelliği.
*   **Görevleri Sıralama:** Görevleri son tarihe, önceliğe veya başlığa göre sıralayabilme.
*   **Gelişmiş Filtreleme:** Birden fazla kriteri birleştirerek (örn: "Yüksek öncelikli VE son tarihi bu hafta olan" görevler) filtreleme.
*   **Tarih Doğrulaması:** Son tarih için girilen formatın (örn: GG/AA/YYYY) doğrulanması.
*   **Daha İyi Kullanıcı Arayüzü:** ncurses gibi bir kütüphane ile daha interaktif bir TUI (Text User Interface) oluşturma veya GUI (GTK+, Qt) seçeneklerini değerlendirme.
*   **Veri Yapısı Optimizasyonları:** Çok büyük görev listeleri için daha performanslı arama/sıralama algoritmaları veya farklı veri yapıları (örn: ikili arama ağacı) düşünülebilir.
*   **Geri Al/Yinele (Undo/Redo) İşlevselliği.**

---

Bu **Bağlı Liste Tabanlı To-Do List Uygulaması**, C programlama dilinin temellerini, dinamik bellek yönetimini ve özellikle **bağlı liste veri yapısının pratik uygulamasını göstermesi açısından değerli bir projedir.** Temel CRUD (Create, Read, Update, Delete - güncelleme hariç) işlemlerini ve dosya kalıcılığını başarıyla implemente etmektedir. Önerilen güvenlik ve mantık iyileştirmeleriyle daha da sağlam ve kullanıcı dostu bir hale getirilebilir. Veri yapıları ve algoritmalar konusundaki yetkinliğinizi göstermek için **harika bir başlangıç noktası!**
