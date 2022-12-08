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

## CMake Örnekleri

- [Example 1](Example_1.md)
