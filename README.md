# OOP-Project-Decision-Maker with Cost Benefit Analysis
Program berbasis Java ini dibuat bedasarkan *problem* yang terjadi ketika bingung mengambil sebuah keputusan di kehidupannya. Metode ini membantu *user* bisa mempertimbangkan keputusannya secara rasional dengan metode **Cost Benefit Analysis**.Metode ini dari referensi buku "Makanya, Mikir!" karya Cania Citta dan Abigail Limuria yang membuat kesan yang kuat saat saya membacanya.

## Deskripsi Kasus
Dalam kehidupan sehari-hari, kita sering dihadapkan pada pilihan yang sulit, misalnya memilih antara tetap di kampus saat ini atau pindah kampus, membeli motor atau mobil, dan sebagainya. Program ini membantu pengguna menganalisis setiap pilihan secara objektif berdasarkan keuntungan (Benefit) dan kerugian (Cost) yang dimiliki masing-masing pilihan.
 
Setiap Benefit dan Cost memiliki:
- **Value (1-5)** — seberapa menguntungkan atau merugikan faktor tersebut
- **Probability (0.0-1.0)** — seberapa besar kemungkinan faktor tersebut terjadi
 
Skor akhir tiap pilihan dihitung dari: `Σ(value × probability)` untuk Benefit dikurangi `Σ(value × probability)` untuk Cost. Pilihan dengan skor tertinggi akan direkomendasikan oleh sistem.
 
---
## Class Diagram
