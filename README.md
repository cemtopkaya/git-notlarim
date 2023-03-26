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

---

### Etiketin bilgilerini formatlı olarak getirmek
  
```shell
$ git tag -n --sort=taggerdate --format '%(refname:short) %(contents) %(taggername) %(taggeremail) - %(taggerdate:short)' cnrupf-1.0.0.350
cnrupf-1.0.0.350 cnrupf new version is 1.0.0.350
 jenkins.user <jenkins.user@ulakhaberlesme.com.tr> - 2022-04-26
```

---

### Sıralayarak (sort) günlükleri göstermek

`git log` komutunda `--sort` seçeneği ile kullanılabilecek anahtar değerleri şunlardır:

*   `commit`: commit id'ye göre sıralama (varsayılan)
*   `author`: yazarın adı, soyadı veya e-posta adresine göre sıralama
*   `committer`: committer'ın adı, soyadı veya e-posta adresine göre sıralama
*   `authordate`: commit zamanına göre yazar adına göre sıralama
*   `committerdate`: commit zamanına göre committer adına göre sıralama
*   `subject`: commit başlığına göre sıralama
*   `refname`: branch veya tag isimlerine göre sıralama
*   `taggerdate`: tagger'ın tarihine göre sıralama
*   `tagger`: tagger'ın adına göre sıralama
*   `topo-order`: topolojik sıralama
*   `reverse`: ters sıralama

Örneğin, `git log --sort=author` şeklinde kullanarak commitleri yazarlarına göre sıralayabilirsiniz.

---

### Anahttarların Listesi

https://github.com/git/git/blob/master/ref-filter.c#L619
https://git-scm.com/docs/git-rev-list#Documentation/git-rev-list.txt---dateltformatgt

```
} valid_atom[] = {
    { "refname" },
    { "objecttype" },
    { "objectsize", FIELD_ULONG },
    { "objectname" },
    { "tree" },
    { "parent" },
    { "numparent", FIELD_ULONG },
    { "object" },
    { "type" },
    { "tag" },
    { "author" },
    { "authorname" },
    { "authoremail" },
    { "authordate", FIELD_TIME },
    { "committer" },
    { "committername" },
    { "committeremail" },
    { "committerdate", FIELD_TIME },
    { "tagger" },
    { "taggername" },
    { "taggeremail" },
    { "taggerdate", FIELD_TIME },
    { "creator" },
    { "creatordate", FIELD_TIME },
    { "subject" },
    { "body" },
    { "contents" },
    { "contents:subject" },
    { "contents:body" },
    { "contents:signature" },
    { "upstream" },
    { "symref" },
    { "flag" },
    { "HEAD" },
    { "color" },
};
```
