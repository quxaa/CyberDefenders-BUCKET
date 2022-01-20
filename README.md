# CyberDefenders-BUCKET
BUCKET - CLOUDSECURITY | WALKTHROUGH
----------------------------------------

![image](https://user-images.githubusercontent.com/71214341/150339012-28e9f714-728f-4428-b2ef-a02655a8fb8e.png)

https://cyberdefenders.org/labs/84
 Merhaba dostlar, bugün "BUCKET" adlı bulut güvenliği konusunu ele alacağız!



#1
--------------------------
What is the full AWS CLI command used to configure credentials?

kimlik bilgilerini yapılandırmak için kullanılan komutu soruyor, zaten bu sorunun kolay olduğunu anlayabilirsiniz size verilen kimlik bilgilerini yapılandırırken yazılan AWS CLI komutunu istiyor.

 aws configure



#2
--------------------------
What is the 'last-modified' date of the directory 'flaws2-logs' present in the s3 bucket?

flaws2-logs dizininin son değiştirilme tarihini bulmak için terminalde "aws s3 ls" komutunu çalıştırmamız gerekiyor zaten tarih direk karşınıza çıkacak!

#3
--------------------------
What is the name of the first generated event -according to time?


zamana göre ilk oluşturulan olay nedir? evet bu soru için biraz uğraşmamız gerekiyor!

1- verilen paketleri incelememiz gerek. paketleri indirmek için: aws s3 sync s3://flaws2-logs .
2-verilen json.gz dosyalarının hepsini gzip ile çıkarmamız gerekiyor | gzip -d filename.json.gz

bütün paketleri incelemek zor olacak, burada olayın adını soruyor paketlere ctrl + f yapıp olayın adını arayabiliriz 

zamana göre bakarsak sonuç:
"eventTime":"2018-11-28 / 22:31:59"
"eventName":"AssumeRole"

AssumeRole

#4
--------------------------
What source IP address generated the event dated 2018-11-28 at 23:03:20 UTC?


verilen tarih ve saatteki etkinliği hangi ip adresinin oluşturduğunu soruyor, paketlerde bu tarihi arattığınızda ip adresini bulacaksınız.

34.234.236.212

#5
--------------------------
Which IP address does not belong to Amazon AWS infrastructure?

paketlerde 1 ip adresi amazonun aws alt yapısına ait değil bunu bulmamız gerek!
yukarıda 1 ip adresi bulmuştuk şimdi ise farklı olan ip adresini buluyoruz ve cevap:

104.102.221.250

#6
--------------------------
Which user issued the 'ListBuckets' request?

ListBuckets adlı isteği hangi kullanıcının yayınladını bulalım.
ctrl + f ile paketlerde ListBuckets ismini aratın!
ve bulduğunuzda username kısmında hangi kullanıcının yayınladığını göreceksiniz :)




"userName":"level3"
level3

#7
--------------------------
What was the first request issued by the user 'level1'?


level1 kullanıcısının  verdiği ilk isteği bulalım
paketlerde "level1" kullanıcısını arayalım ve isteği sorduğu için direk cevabı buluyoruz!



"eventName":"CreateLogStream"
CreateLogStream
