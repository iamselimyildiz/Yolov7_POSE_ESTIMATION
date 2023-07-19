![yt2_thumbnail](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/79a079c8-d244-4a93-9c20-d759f284e846)
# Yolov7_POSE_ESTIMATION

Bu repo da kendi projeleriniz için Yolov7 pose estimation kullanmayı öğreneceksin. Kolay gelsin !

1- Öncelikle Visual studio'nun bilgisayararınızda kurulu olması gerekiyor. Visual studio/installer/workload(işyükü) kısmından "Desktop devolopment with C++" eklentisini seçin ve kurmaya başlayın.(Linux kullanıyorsanız bu aşamayı atlayın)
Visual studio: `https://visualstudio.microsoft.com/tr/downloads/`
![1](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/75a2fb2f-a52a-46db-969e-1ad90debf75d)  


2-Masa üstüne bir `yolov7 pose est` adında  bir klasör açalım. Adresteki `https://github.com/WongKinYiu/yolov7/tree/pose` repository i zip dosyası olarak indirelim ve masaüstündeki `yolov7 pose est` dosyasına kayıt edelim.  
![2](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/84606bca-9f00-4dbe-baf2-65926d3c0841)  


3- Bu klasörün içine indirdiğimiz zip dosyasını ayıklayacağız. Şöyle görünecek  
![3](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/09241b63-eadc-46ff-a554-39eba0c9e678)  


4-Şimdi Anaconda promtu açalım. Ve altta verilen komut ile masaüstüne açtığımız yolov7-pose yönlendirelim.
`cd Desktop\yolov7 pose est\yolov7-pose`----> `cd Desktop\masaüstünde açtığımız dosya adı\yolov7-pose`  
![4](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/c2abd94d-9aa8-40a8-9234-e914748c5d93)  



5-Şimdi sanal ortam oluşturalım `conda create -n yolov7_pose python=3.9` yazıp Enter'a bas. İndirmek için izin isteyecek `y`  e basıp enter'a bas.İndirme işlemi bitene kadar bekle.  


6-Şimdi anaconda promt daki (base)'i (yolov7_pose)'a çevirmeliyiz.`conda activate yolov7_pose` yaz enter'a bas.  
![5](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/0ed6cecd-c26e-4eb2-b364-768793331ced)  


7-Şimdi indirmiş olduğumuz dosyalardan `requirements.txt` dosyasına girip `torch>=1.7.0
torchvision>=0.8.1` yazan satırları silelim ve kaydedip kapatalım. çünkü biz grafik kartını kullanmak istiyoruz işlemciyi değil.  
![6](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/c07b4b53-e2fe-48c1-8968-bc8dba5dc1cb)  


8-Şimdi 'anaconda prompt' a `pip install -r requirements.txt` yazıp enter'a basalım. Bu requirements dekileri indirecek.  


9-Sonra pytorch sitesine girip CUDA 11.3' ün 1.11 versiyonunu bulup kopyalayalım.      
Site:`[pytorch.org](https://pytorch.org/get-started/previous-versions/)https://pytorch.org/get-started/previous-versions/`  
Kopyalanacak versiyon:`pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113`  
![7](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/047f6de3-0146-440d-969d-d232ed4daa65)  


10-Kopyaladığımız versiyonu anaconda prompt'ta çalıştıralım.Bu gpu destekli pytorch indirecek  
![8](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/9e217933-c08a-4a6f-9762-79d654fcdb90)   


11-Pytorch u kontrol etmek için sırasıyla verilenleri çalıştıralım `python`, `import torch`, `torch.cuda.is_available()`. True döndürmesi gerek False gelirse lütfen 10. adımı tekrarla.  
![9](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/580711f9-b8f6-4c87-800e-368f51025e83)  


12-Şimdi yolov7 repository/releases/assets bölümünden `yolov7-w6-pose.pt` dosyasını bul ve masaüstündeki `yolov7 pose est` klasörüne kopyala. Şöyle  
![10](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/3a3718af-ff1b-4ff7-9c54-dfe7ea01b6c9)  


13-Ardından `detect.py` dosyasını açıp 66. satıra yeni satır ekleyip `startTime=0` yaz.  
Şimdi videolara FPS yazmak için 137. satıra gidip bu kodu yaz:  
# calculate fps  
            if dataset.mode != 'image':
                currentTime = time.time()

                fps=1/(currentTime - startTime)
                startTime = currentTime
                cv2.putText(im0, "FPS : " + str(int(fps)),(20,70),cv2.FONT_HERSHEY_PLAIN, 2, (0,255,0),2)  

14- Şimdi bulunduğumuz `detect.py` dosyasında 178. satırdan başlayan flaglerin en sonuna --nobbox flag i ekliyoruz. Şöyle:  `parser.add_argument('--nobbox', action='store_true', help='do not show bbox around person')`    
![11](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/00479b50-b8a2-41f1-8959-910492a05991)  



15- 121. satırdaki satırı şununla değiştir.  
`plot_one_box(xyxy, im0, label=label, color=colors(c, True), line_thickness=opt.line_thickness, kpt_label=kpt_label, kpts=kpts, steps=3, orig_shape=im0.shape[:2],nobbox= opt.nobbox)` basitçe bunu `nobbox= opt.nobbox` eklemiş olduk.  
![12](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/2bb3dbf2-3c30-4c36-9173-df2c3596ac9c)  


16- Masaüstü/yolov7 pose est/yolov7-pose/Utils/plots.py dosyası açılır. 68. satırdaki `def plot_one_box` fonksiyonu şununla değiştirilir.  
`def plot_one_box(x, im, color=None, label=None, line_thickness=3, kpt_label=False, kpts=None, steps=2, orig_shape=None, nobbox = True):`  
Ardından 74. satırdaki kod parçacığı şöyle olacak şekilde değiştirilir.  
`if not nobbox:`    
`  cv2.rectangle(im, c1, c2, (255,0,0), thickness=tl*1//3, lineType=cv2.LINE_AA)`


17-Artık `yolov7 pose est` klasörümüze ilk denememizi yapmak için bir video ve fotoğraf yükleyelim. Yüklediklerimizin içinde özellikle insan olmasını tavsiye ederim.  
Örnek:  
![tennis](https://github.com/iamselimyildiz/Yolov7_POSE_ESTIMATION/assets/94224409/01ac4f01-3ba9-4e0f-be02-d3f073f1f3aa)  


18-Artık bu kodu anaconda prompt da çalıştırarak istenilen video ve fotoğraf medyasına pose estimation uygulayabiliriz.  
İşlenen foto/videolar yolov7 pose est/yolov7_pose/runs klasörü içinde depolanacak.
`python detect.py --weights yolov7-w6-pose.pt --kpt-label --hide-labels --hide-conf --source tennis.jpg --nobbox`  


19- Ayrıca bu kod webcamde çalıştırmanı sağlar.  
`python detect.py --weights yolov7-w6-pose.pt --kpt-label --hide-labels --hide-conf --source 0 --device 0 --nobbox`  


20-Ne ne işe yarıyor:  
`python= çalıştırma yapar`  
`detect.py= dosyası pose estimation yapan ana dosyadır`  
`--weights yolov7-w6-pose.pt=  Her sinir hücresi (nöron), giriş katmanındaki verileri alır, bu verileri ağırlıklarla çarpar ve ardından bir aktivasyon fonksiyonuna gönderir. `  
`--kpt-label= keypoint label eklem noktaları`  
`--hide-labels=etiketleri saklar`    
`--hide-conf=doğruluk oranını saklar`   
`--source tennis.jpg= kaynak medya`  
`--nobbox= nesneyi kutucuk içine almaz`    




