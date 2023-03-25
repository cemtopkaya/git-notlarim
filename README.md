# Git Komutlarına Dair Notlarım

Git komutlarına dair notlarım

---

### git describe
git describe komutu, en son etiketlenmiş commit'in adını veya en son etiketlenmiş commit'e göre bir açıklama yapar. Bu komut aşağıdaki formatta çalışır:

```shell
git describe <commit>
```


Burada <commit> parametresi, etiketin başlangıç noktası olarak kullanılacak olan commit'i belirtir. Eğer <commit> belirtilmezse, HEAD kullanılır.

`git describe` komutu, en yakın etiketi (tag) gösterir. Eğer HEAD, tag commit'inden sonra oluşturulmuş yeni bir commit ise, komut sonraki tag'ı gösterir. Ayrıca `--tags` parametresi kullanılarak sadece tag'lar içinde arama yapılabilir.

`git describe` komutunun örnek kullanımları:

`git describe`: En yakın tag'ı gösterir.
`git describe HEAD~5`: HEAD'den geriye doğru 5. commit'den başlayarak en yakın tag'ı gösterir.
`git describe --tags`: En yakın tag'ı gösterir ama sadece tag'lar arasında arama yapar.
`git describe --abbrev=0`: En yakın tag'ın ismini gösterir (prefix olmadan).

---

### Etiketin Açıklamasını Yazdırmak
Belirli bir etiketin açıklamasını yazdırmak için aşağıdaki komutu kullanabilirsiniz:

```shell
git show etiket_adı --no-patch --format='%B'
```
- `--no-patch` parametresi, değişikliklerin ayrıntılarını göstermeden yalnızca etiket bilgilerini yazdırmak için kullanılır. 
- `--format='%B'` parametresi ise etiket açıklamasını yazdırmak için kullanılır. etiket_adı parametresi, bilgilerini görmek istediğiniz etiketin adını belirtir.

---

### Etiketi Oluşturan Kullanıcı Bilgilerini Yazdırmak
Etiketi oluşturan kullanıcının adı, e-posta adresi ve tarih bilgisini aşağıdaki komut kullanarak alabilirsiniz:

```shell
git for-each-ref --count=10 --sort=taggerdate --format '%(refname:short) %(taggername) <%(taggeremail)> - %(taggerdate:short)' refs/tags
```

Bu komut, `refs/tags` dizinindeki son 10 etiketin adını (`--count=10` dan dolayı), etiketi oluşturan kullanıcının adını ve e-posta adresini, oluşturma tarihini formatlanmış bir şekilde görüntüler. 

`--count=10` parametresi son 10 etiketi alırken, 
`--sort=taggerdate` parametresi etiketlerin oluşturma tarihine göre artan sıralamayı, `--sort=-taggerdate` azalan sıralamayı sağlar. 
`--format` parametresi, etiket adını, etiketi oluşturan kullanıcının adını ve e-posta adresini, oluşturma tarihini gösterir.

