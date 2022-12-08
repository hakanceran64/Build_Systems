# CMake Dökümantasyon

## CMAKE_AUTO

*CMake 2.8.8 sürümü* ile birlikte **CMAKE_AUTO** özelliğini kazanmıştır. Bu değişken ile CMake tarafından otomatik olarak oluşturulacak dosyaların türlerini belirtilir. `ON` veya `OFF` değerlerini alabilir. `ON` değeri, CMake'in dosya oluşturma işlemini otomatik olarak yapmasını sağlar. `OFF` değeri ise otomatik dosya oluşturma işlemini devre dışı bırakır. Bunlar şu şekildedir:

- **moc dosyaları:** CMake, Q_OBJECT ve Q_GADGET ile tanımlanmış sınıflar için moc (Meta-Object Compiler) dosyalarını otomatik oluşturabilir. Bu dosyalar, sinyal-slot mekanizmasının çalışmasını sağlar.

- **rcc dosyaları:** CMake, Qt Resource System kullanılarak tanımlanmış kaynak dosyaları için rcc (Resource Compiler) dosyalarını otomatik oluşturabilir. Bu dosyalar, uygulamaların kaynak dosyalarına erişimini sağlar.

- **ui dosyaları:** CMake, Qt Designer kullanılarak oluşturulmuş arayüz dosyaları için ui (User Interface) dosyalarını otomatik oluşturabilir. Bu dosyalar, kullanıcı arayüzlerini tanımlayan dosyalardır.

Örnek kod parçacığı:

~~~CMake

    set(CMAKE_AUTOMOC ON)
    set(CMAKE_AUTORCC ON)
    set(CMAKE_AUTOUIC ON)

~~~

## CMAKE_PREFIX_PATH

**CMAKE_PREFIX_PATH** değişkeni, CMake tarafından aranacak dizinleri belirtir. Bu değişken, bir uygulamanın gerekli kütüphanelerini bulabilmesi için kullanılır. Örneğin, eğer bir uygulamanın Qt kütüphanelerini kullanıyorsa ve Qt'nin kurulu olduğu dizin bilinmiyorsa, *CMAKE_PREFIX_PATH* değişkeni ile Qt'nin kurulu olduğu dizin belirtilebilir. Böylece CMake, uygulamanın gerekli Qt kütüphanelerini bu dizinde arayarak bulabilir.

`CMAKE_PREFIX_PATH` değişkeninin kullanımı şu şekildedir:

~~~CMake

    set(CMAKE_PREFIX_PATH <dizin>)

~~~

Yukarıdaki kodda, `<dizin>` yerine aranacak dizinin tam adresi yazılmalıdır. Örneğin, Qt'nin kurulu olduğu dizin `C:/Qt/6.4.1/mingw_64/lib/cmake` ise aşağıdaki gibi bir kod yazılabilir:

~~~CMake

    set(CMAKE_PREFIX_PATH "C:/Qt/6.4.1/mingw_64/lib/cmake")

~~~

> **Not:** *CMAKE_PREFIX_PATH* değişkeni, sadece bir uygulamanın gerekli kütüphaneleri bulabilmesi için kullanılmaz. Aynı zamanda bir uygulamanın gerekli bağımlıklarını da bulabilmesi için bu değişken kullanılabilir. Örneğin, bir uygulama `QtCore` ve `QtGui` kütüphanelerini kullanıyorsa, bu uygulamanın gerekli bağımlıkları `QtCore` ve `QtGui` kütüphaneleridir. Eğer bu bağımlıkların bulunmadığı bir sistemde bu uygulama çalıştırılmaya çalışılırsa, uygulama çalışmayacaktır.

## find_package()

CMake, bir uygulamanın gerekli bağımlılıklarını bulabilmek için `find_package()` fonksiyonunu kullanır. Bu fonksiyon ile uygulamanın gerekli kütüphaneleri belirtilir ve CMake bu kütüphaneleri bulmaya çalışır. Eğer kütüphaneler bulunursa CMake uygulamanın gerekli bağımlılıklarını otomatik olarak ekler.

`find_package()` fonksiyonu, en basit anlamda aşağıdaki gibi kullanılabilir.

> **Not:** Tam imzanın çok daha karmaşık olduğunu unutmayın!

~~~CMake

    find_package(<paket> [COMPONENTS <bileşenler>...] [REQUIRED])

~~~

Yukarıdaki kodda, `<paket>` yerine aranacak paketin adı yazılır. **COMPONENTS** anahtar kelimesi ile aranacak paketin bileşenleri belirtir. **REQUIRED** anahtar kelimesi ise paketin bulunmaması durumunda CMake'in bir hata mesajı üretmesini sağlar.

Örnek olarak, bir uygulamanın `QtCore` ve `QtGui` kütüphanelerini kullandığını varsayalım. Bu uygulamanın gerekli bağımlıklarını bulabilmesi için aşağıdaki gibi bir kod yazılabilir:

~~~CMake

    find_package(Qt6 COMPONENTS Core Gui REQUIRED)

~~~

Bu kodda, `find_package()` fonksiyonu kullanılarak Qt6 paketi aranır ve **Core** ve **Gui** bileşenleri bulunmaya çalışılır. Eğer bu bileşenler bulunursa, CMake uygulamanın gerekli bağımlıklarını otomatik olarak ekler. Eğer bileşenler bulunamazsa, CMake bir hata mesajı üretir ve uygulama derlenmez.

> Not: find_package() fonksiyonunun birinci parametresi olarak aranacak paketin adı değil de adresi de verilebilir. Bu durumda, paketin bulunup bulunmadığı kontrol edilmez ve sadece verilen adreste bulunan paket kullanılır ve paketin bulunacağı dizin doğrudan belirtildiği için arama işlemi daha hızlı olacaktır.

## CMake Örnekleri

- [Example 1](Example_1.md)
