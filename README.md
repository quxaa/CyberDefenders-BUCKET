# CyberDefenders-BUCKET
 BUCKET - CLOUDSECURITY | WALKTHROUGH
 ----------------------------------------
 
 ![image](https://user-images.githubusercontent.com/71214341/150339012-28e9f714-728f-4428-b2ef-a02655a8fb8e.png)
 
 https://cyberdefenders.org/labs/84
  Merhaba dostlar, bugün "BUCKET" adlı bulut güvenliği laboratuvarını birlikte inceleyeceğiz! Bu labda, AWS S3 ve olay günlükleri üzerinden analiz yaparak bazı önemli soruları yanıtlayacağız. Haydi başlayalım!
 
 
 
 #1
 --------------------------
Soru: What is the full AWS CLI command used to configure credentials?

Bu soru, AWS kimlik bilgilerini yapılandırmak için hangi komutun kullanıldığını soruyor. AWS CLI kullanımına aşina olanlar için oldukça basit bir soru.

Cevap:

aws configure
Bu komut, kimlik bilgilerinizi (Access Key ve Secret Key) AWS CLI üzerinden ayarlamanıza olanak tanır.
 
 
 
 #2
 --------------------------

Soru: What is the 'last-modified' date of the directory 'flaws2-logs' present in the s3 bucket?

AWS S3'te bulunan 'flaws2-logs' dizininin son değişiklik tarihini bulmamız isteniyor. Bunun için aşağıdaki komutu kullanabiliriz:

aws s3 ls s3://flaws2-logs
Bu komutu çalıştırdığınızda, dizinin son değişiklik tarihini doğrudan görebilirsiniz.
 
 
 #3
 --------------------------

Soru: What is the name of the first generated event - according to time?

Olayları zamana göre inceleyerek ilk oluşturulan olayı bulmamız gerekiyor.

Adımlar:

Gerekli günlükleri AWS S3'ten indirin:

aws s3 sync s3://flaws2-logs .
Gzip ile sıkıştırılmış JSON dosyalarını açın:

gzip -d filename.json.gz
İlk oluşan olayı bulmak için zaman damgasına göre araştırma yapın:

grep "eventTime" *.json | sort
Bulduğumuza göre, ilk olay:

"eventTime":"2018-11-28 / 22:31:59", "eventName":"AssumeRole"
Cevap:

AssumeRole
 
 #4
 --------------------------

Soru: What source IP address generated the event dated 2018-11-28 at 23:03:20 UTC?

Adımlar:

Olay günlüklerinde belirtilen tarihi arayın:

grep "2018-11-28T23:03:20" *.json
İlgili olayın kaynağı olan IP adresini bulun.

Cevap:

34.234.236.212
 
 
 #5
 --------------------------

Soru: Which IP address does not belong to Amazon AWS infrastructure?

Tüm olayları analiz edip AWS'ye ait olmayan IP adresini tespit etmeliyiz. Daha önce bulunan IP adresleri ile AWS'ye ait olmayanı karşılaştırırsaı:

Cevap:

104.102.221.250
Bu IP adresi AWS altyapısına ait değil.
 
 #6
 --------------------------

 Soru: Which user issued the 'ListBuckets' request?

Adımlar:

JSON günlüklerinde 'ListBuckets' olayını araştırın:

grep "ListBuckets" *.json
Bulunan olaylarda "userName" değerini belirleyin.

Cevap:

level3
 
 #7
 --------------------------
Soru: What was the first request issued by the user 'level1'?

Adımlar:

'level1' kullanıcısının olay günlüklerinde geçtiği satırları bulalım:

grep "level1" *.json
Zamana göre ilk isteği belirleyelim.

Cevap:

CreateLogStream

