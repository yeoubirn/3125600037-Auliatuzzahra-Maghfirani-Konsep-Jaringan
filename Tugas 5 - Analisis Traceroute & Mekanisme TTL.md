# Laporan Tugas Konsep Jaringan: Analisis Cara Kerja Traceroute dan Mekanisme TTL

## A. Topologi dan Alokasi IP

Topologi menggunakan konfigurasi segitiga dengan 3 router + 2 PC.

![Topologi segitiga 3 router dan 2 PC](images/tracert-topologi.png)

| Perangkat | Port | IP | Mask | Keterangan |
|---|---|---|---|---|
| PC 0 | Fa0 | 172.16.10.10 | 255.255.255.0 | GW 172.16.10.1 |
| PC 1 | Fa0 | 172.16.20.10 | 255.255.255.0 | GW 172.16.20.1 |
| Router0 | Gig0/0 | 172.16.10.1 | 255.255.255.0 | PC0 |
| Router0 | Gig0/1 | 10.1.20.2 | 255.255.255.252 | Router Atas Gig0/0 |
| Router0 | Gig0/2 | 10.1.10.2 | 255.255.255.252 | ke Router2 Gig0/2 |
| Router Atas | Gig0/0 | 10.1.20.1 | 255.255.255.252 | ke Router0 Gig0/1 |
| Router Atas | Gig0/1 | 10.1.30.1 | 255.255.255.252 | ke Router2 Gig0/0 |
| Router 2 | Gig0/0 | 10.1.30.2 | 255.255.255.252 | Router Atas Gig0/1 |
| Router 2 | Gig0/1 | 172.16.20.1 | 255.255.255.0 | PC1 |
| Router 2 | Gig0/2 | 10.1.10.1 | 255.255.255.252 | Router0 Gig0/2 |

---

## B. Hasil Pengujian Traceroute

### 1. Skenario Jalur Langsung Bawah (3 Hops)

![Hasil tracert skenario 1](images/tracert-skenario1.png)

Penjelasan:

| Hop | IP | Yang membalas | Pesan ICMP |
|---|---|---|---|
| 1 | 172.16.10.1 | Router0 (gateway PC0) | Time Exceeded (Type 11) saat TTL=1 habis |
| 2 | 10.1.10.1 | Router2 (interface Gig0/2, sisi link bawah) | Time Exceeded (Type 11) saat TTL=2 habis |
| 3 | 172.16.20.10 | PC1 (tujuan) | Echo Reply (Type 0) |

### 2. Skenario Jalur Memutar Atas

Pengujian kedua dilakukan dengan mengubah rute statis agar lalu lintas data dari PC0 menuju PC1 melewati Router Atas terlebih dahulu. Pada Router0 rute lama via 10.1.10.1 dihapus dan diganti via 10.1.20.1. Pada Router Atas ditambahkan rute menuju 172.16.20.0/24 via 10.1.30.2 dan menuju 172.16.10.0/24 via 10.1.20.2. Pada Router2 rute balik diganti menjadi via 10.1.30.1.

![Hasil tracert skenario 2](images/tracert-skenario2.png)

- **Hop 1 (172.16.10.1):** PC0 mengirim paket dengan TTL = 1. Router0 mengurangi TTL menjadi 0, membuang paket, dan membalas dengan ICMP Time Exceeded (Type 11).
- **Hop 2 (10.1.20.1):** Paket dengan TTL = 2 lolos dari Router0, lalu TTL habis di Router Atas. Router Atas membalas dengan ICMP Time Exceeded (Type 11) dari interface Gig0/0 tempat paket masuk.
- **Hop 3 (10.1.30.2):** Paket dengan TTL = 3 melewati Router0 dan Router Atas, lalu TTL habis di Router2. Router2 membalas dengan ICMP Time Exceeded (Type 11) dari interface Gig0/0 tempat paket masuk.
- **Hop 4 (172.16.20.10):** Paket dengan TTL = 4 melewati ketiga router dan sampai di PC1. PC1 membalas dengan ICMP Echo Reply (Type 0) sehingga traceroute berhenti (*Trace complete*).

---

## C. Analisis dan Pembahasan

1. **Manipulasi TTL hop-by-hop.** Traceroute mengirim paket dengan TTL yang dinaikkan bertahap (1, 2, 3, dan seterusnya). Setiap router mengurangi TTL sebanyak 1, dan router yang menerima paket dengan TTL menjadi 0 membuang paket tersebut lalu mengirim ICMP Time Exceeded (Type 11) ke pengirim. Alamat sumber pesan inilah yang ditampilkan sebagai hop, sehingga seluruh router di jalur dapat dipetakan satu per satu.
2. **Perbedaan respon router transit dan tujuan.** Router transit membalas dengan ICMP Type 11, sedangkan perangkat tujuan membalas dengan ICMP Echo Reply (Type 0). Perbedaan ini yang membuat traceroute tahu kapan harus berhenti.
3. **Alamat hop adalah interface masuk.** Router membalas menggunakan IP interface tempat paket diterima. Pada skenario 1, hop 2 tampil sebagai 10.1.10.1 (interface link bawah Router2), sedangkan pada skenario 2 tampil sebagai 10.1.30.2 (interface link dari Router Atas). Perbedaan alamat ini menunjukkan jalur yang dilewati paket.
4. **Perubahan rute statis tercermin pada hasil tracert.** Hasil berubah dari 3 hop (jalur bawah) menjadi 4 hop (jalur memutar atas) hanya karena rute statis diubah. Ini membuktikan traceroute mampu menggambarkan jalur sebenarnya yang dilalui paket.
5. **Pentingnya konsistensi rute pergi dan pulang.** Jika rute lama tidak dihapus (*dual route*), pelacakan dapat mengalami *Request timed out* karena balasan tidak kembali lewat jalur yang diharapkan. Rute lama perlu dihapus dengan `no ip route` saat mengganti jalur.
6. **Peran TTL dalam mencegah routing loop.** TTL berkurang di setiap router, sehingga paket yang terjebak dalam loop akan dibuang saat TTL mencapai 0 dan tidak berputar selamanya.
