# Sürücüsüz Metro Simülasyonu (Rota Optimizasyonu)

Bu proje, bir metro ağında iki istasyon arasındaki en hızlı ve en az aktarmalı rotayı bulan bir simülasyon uygulamasıdır. Projede BFS ve A\* algoritmaları kullanılarak kullanıcılara optimum rota seçenekleri sunulmaktadır.

## Proje Hakkında

Bu uygulamada, graf veri yapısı kullanılarak gerçek bir metro ağı modellenmiştir. Kullanıcılar başlangıç ve bitiş istasyonlarını belirleyerek iki farklı optimizasyon kriteri üzerinden rota bulabilirler:

1. **En Az Aktarmalı Rota:** BFS algoritması kullanılarak, istasyonlar arası en az hat değişimi gerektiren rota bulunur.
2. **En Hızlı Rota:** A\* algoritması kullanılarak, istasyonlar arası seyahat süresini minimize eden rota hesaplanır.

## Kullanılan Teknolojiler ve Kütüphaneler

- **Python 3.9**: Uygulamanın geliştirildiği programlama dili
- **collections.defaultdict**: Varsayılan değerlerle sözlük oluşturmak için kullanılmıştır
- **collections.deque**: BFS algoritmasında kuyruk veri yapısı olarak kullanılmıştır
- **heapq**: A\* algoritmasında öncelik kuyruğu için kullanılmıştır
- **typing**: Tip tanımlamaları için kullanılan kütüphane

## Algoritmaların Çalışma Mantığı

### BFS (Breadth-First Search) Algoritması

BFS algoritması, bir grafta başlangıç noktasından başlayarak aynı seviyedeki tüm düğümleri ziyaret eden, sonra bir sonraki seviyeye geçen bir arama algoritmasıdır. Bu projede BFS algoritması şu şekilde çalışır:

1. Başlangıç istasyonunu bir kuyruğa ekler
2. Kuyruktan bir istasyon çıkarır
3. Bu istasyonun komşularını kontrol eder ve daha önce ziyaret edilmemiş olanları kuyruğa ekler
4. Hedef istasyona ulaşılana kadar veya kuyruk boşalana kadar bu işlemi tekrarlar

Bu algoritma, en az kenar sayısına sahip yolu bulduğu için, metro ağımızda en az aktarma yapılan rotayı bulmak için idealdir. Her istasyon geçişi bir kenar olarak düşünülürse, BFS en az istasyon geçişi olan rotayı garanti eder.

### A\* (A-Star) Algoritması

A* algoritması, hedefe ulaşmak için en düşük maliyeti tahmin ederek çalışan bir arama algoritmasıdır. Bu projede A* algoritması şu şekilde çalışır:

1. Algoritma, her düğüm için iki maliyet hesaplar:
   - g(n): Başlangıç noktasından mevcut düğüme kadar olan gerçek maliyet (seyahat süresi)
   - h(n): Mevcut düğümden hedefe olan tahmini maliyet (bu projede 0 olarak alınmıştır)
   - f(n) = g(n) + h(n): Toplam maliyet
2. Öncelik kuyruğu kullanarak, her adımda en düşük f(n) değerine sahip düğümü seçer
3. Seçilen düğümün komşularını keşfeder ve her biri için g(n) değerini hesaplar
4. Bir düğüme daha iyi bir yoldan ulaşıldığında, değerlerini günceller
5. Hedef düğüme ulaşılana kadar veya kuyruk boşalana kadar bu işlemi tekrarlar

Bu algoritma, her istasyon arasındaki seyahat süresini dikkate aldığı için en hızlı rotayı bulmak için kullanılmıştır.

### Neden Bu Algoritmaları Kullandık?

- **BFS Algoritması**: Aktarma sayısını minimize etmek istediğimizde, her hat değişimini bir adım olarak düşünürsek, BFS en az adımlı yolu bulmak için en uygun algoritmadır.
- **A\* Algoritması**: İstasyonlar arası geçiş sürelerini dikkate alarak en hızlı rotayı bulmak için A* algoritması idealdir. A*, BFS'den farklı olarak kenar ağırlıklarını (geçiş sürelerini) hesaba katar ve hedef odaklı çalışır.

## Örnek Kullanım ve Test Sonuçları

Uygulama, üç farklı metro hattından oluşan (Kırmızı, Mavi ve Turuncu) bir metro ağı üzerinde test edilmiştir. Her hat farklı istasyonlardan oluşur ve belirli noktalarda aktarma istasyonları bulunur.

### Test Senaryoları:

#### 1. AŞTİ'den OSB'ye:

- **En az aktarmalı rota:** AŞTİ -> Kızılay -> Ulus -> Demetevler -> OSB
- **En hızlı rota (21 dakika):** AŞTİ -> Kızılay -> Ulus -> Demetevler -> OSB

#### 2. Batıkent'ten Keçiören'e:

- **En az aktarmalı rota:** Batıkent -> Demetevler -> Gar -> Keçiören
- **En hızlı rota (21 dakika):** Batıkent -> Demetevler -> Gar -> Keçiören

#### 3. Keçiören'den AŞTİ'ye:

- **En az aktarmalı rota:** Keçiören -> Gar -> Kızılay -> AŞTİ
- **En hızlı rota (19 dakika):** Keçiören -> Gar -> Kızılay -> AŞTİ

## Projeyi Geliştirme Fikirleri

1. **Gerçek Zamanlı Veri Entegrasyonu**: Trenlerin gerçek zamanlı konum ve yoğunluk verilerini kullanarak daha doğru seyahat süreleri hesaplanabilir.

2. **Çok Kriterli Optimizasyon**: Seyahat süresi, aktarma sayısı ve yoğunluk gibi birden fazla kriteri dikkate alan yeni algoritmalar eklenebilir.

3. **Web veya Mobil Uygulama**: Kullanıcı dostu bir arayüz ile uygulamanın web veya mobil platforma taşınması.

4. **Zenginleştirilmiş Görselleştirme**: Metro ağının interaktif görselleştirilmesi, rota animasyonları eklenebilir.

5. **Çoklu Seçenek Sunma**: Kullanıcıya en hızlı, en az aktarmalı ve bu ikisinin farklı kombinasyonları şeklinde alternatif rotalar sunulabilir.

6. **Yoğunluk Analizi**: Belirli saatlerdeki istasyon ve hat yoğunluklarını analiz edip, yoğunluğun az olduğu rotalara öncelik veren bir algoritma eklenebilir.

7. **Engelli Erişimi Optimizasyonu**: Asansör, yürüyen merdiven gibi erişilebilirlik özelliklerine göre rota optimizasyonu yapılabilir.

## Kurulum ve Çalıştırma

1. Projeyi klonlayın:

```
git clone https://github.com/username/metro-simulation.git
```


2. Uygulamayı çalıştırın:

```
python HalilErdogan_metro_simulation.py
```
