# Laporan Tugas Konsep Jaringan: Jawaban Soal Bab 2

## Level A: Ingatan dan Pemahaman

### 1. Jelaskan alasan komunikasi jaringan disusun berlapis.

Komunikasi jaringan disusun berlapis karena melibatkan masalah yang sangat beragam: mengubah bit menjadi sinyal, mengatur penggunaan media, mengenali tujuan lokal, menentukan jalur antarsubnet, membedakan proses aplikasi, menangani kehilangan data, menyepakati format informasi, hingga menyediakan layanan yang dapat digunakan manusia. Apabila seluruh fungsi tersebut dirancang sebagai satu mekanisme besar, sistem akan sulit dikembangkan, diuji, dan diperbaiki.

### 2. Bedakan layanan, antarmuka, dan protokol.

- **Layanan:** menjelaskan apa yang disediakan atau diberikan oleh sebuah lapisan kepada lapisan di atasnya.
- **Antarmuka:** menjelaskan bagaimana lapisan di atas mengakses layanan dari lapisan di bawahnya pada sistem/host yang sama.
- **Protokol:** aturan, format, dan tata cara komunikasi antara entitas sejawat (*peer entities*) pada lapisan yang sama di sistem yang berbeda.

### 3. Sebutkan tujuh lapisan OSI dari bawah ke atas beserta fungsi utamanya.

- **Lapisan 1 – Physical:** mengirim bit mentah melalui media fisik; mengatur sinyal listrik/optik/radio, konektor, modulasi, dan sinkronisasi.
- **Lapisan 2 – Data Link:** mengirim frame pada satu tautan/jaringan lokal; menangani pengalamatan fisik (MAC), akses media (MAC), dan deteksi error (CRC).
- **Lapisan 3 – Network:** menangani pengalamatan logis (IP) dan penentuan rute (*routing*) paket antarjaringan.
- **Lapisan 4 – Transport:** menyediakan komunikasi logis antarsoket/proses aplikasi (*end-to-end*) via nomor port, keandalan data, serta kontrol aliran.
- **Lapisan 5 – Session:** membuka, memelihara, menyinkronkan (*checkpoints*), dan menutup sesi dialog antardua aplikasi.
- **Lapisan 6 – Presentation:** menstandarkan format data; menangani konversi sintaksis, pengodean karakter, enkripsi, dan kompresi data.
- **Lapisan 7 – Application:** menyediakan antarmuka langsung dan protokol jaringan (seperti HTTP, DNS) untuk proses aplikasi pengguna.

### 4. Sebutkan empat lapisan model TCP/IP.

- **Application:** menyediakan layanan dan protokol jaringan tingkat tinggi bagi aplikasi pengguna (menggabungkan fungsi Application, Presentation, dan Session pada OSI).
- **Transport:** menyediakan komunikasi logis antarsoket/proses aplikasi pada host yang berbeda (misalnya via TCP atau UDP).
- **Internet:** mengatur pengalamatan logis (IP) serta pengantaran paket datagram melintasi berbagai jaringan/subnet.
- **Network Access / Link:** menangani *framing* data, pengalamatan fisik lokal (MAC), serta transmisi bit pada media fisik jaringan lokal.

### 5. Mengapa model TCP/IP kadang disajikan sebagai lima lapisan?

Model TCP/IP kadang disajikan sebagai lima lapisan karena banyak literatur memisahkan lapisan Network Access menjadi Data Link dan Physical. Pemisahan ini bertujuan mempermudah pembelajaran teknis, sehingga analisis transmisi bit dan karakteristik sinyal pada media fisik dapat dibedakan secara tegas dari mekanisme pembentukan frame, pengalamatan lokal, dan *switching*.

### 6. Apa perbedaan frame, IP packet, TCP segment, dan UDP datagram?

- **Frame:** PDU pada Lapisan 2 berfungsi mengirim data pada satu tautan/jaringan lokal fisik menggunakan alamat perangkat keras lokal, serta umumnya diakhiri dengan *trailer* untuk deteksi eror transmisi.
- **IP Packet:** PDU pada Lapisan 3 mengatur pengalamatan logis global (Source dan Destination IP) serta penentuan rute (*routing*) agar data dapat berpindah melintasi berbagai subnet/jaringan heterogen.
- **TCP Segment:** PDU pada Lapisan 4 untuk protokol TCP. Bersifat berorientasi koneksi dan andal, memuat nomor port, Sequence Number, Acknowledgment Number, serta kendali aliran.
- **UDP Datagram:** PDU pada Lapisan 4 untuk protokol UDP. Bersifat nir-koneksi dan tanpa jaminan pengantaran/urutan, dengan format header ringkas.

### 7. Definisikan header, trailer, dan payload.

- **Header:** informasi kendali yang disisipkan di awal sebelum payload, memuat metadata seperti alamat asal, alamat tujuan, panjang data, dan tipe protokol.
- **Trailer:** informasi kendali tambahan yang diletakkan di akhir setelah payload, umumnya difungsikan untuk verifikasi keutuhan data dan deteksi kesalahan transmisi.
- **Payload:** data atau muatan inti yang dibawa oleh suatu paket/PDU, yang biasanya merupakan PDU dari lapisan tepat di atasnya.

### 8. Jelaskan enkapsulasi dan dekapsulasi.

- **Enkapsulasi:** proses penambahan informasi kendali pada data saat bergerak turun dari lapisan atas ke lapisan bawah pada sisi pengirim. Misalnya, data HTTP dibungkus dengan TCP header, kemudian dibungkus IP header, dan terakhir dibungkus Ethernet header beserta FCS trailer.
- **Dekapsulasi:** proses pemeriksaan dan pelepasan informasi kendali lapis demi lapis saat data bergerak naik dari lapisan bawah menuju aplikasi pada sisi penerima.

### 9. Apa fungsi multiplexing dan demultiplexing?

- **Multiplexing:** menggabungkan beberapa aliran data dari berbagai proses/aplikasi yang berbeda agar dapat dikirim bersamaan melalui satu antarmuka jaringan dan protokol lapisan bawah yang sama (misalnya penambahan nomor port sumber pada Transport layer).
- **Demultiplexing:** menguraikan dan mengarahkan data yang diterima dari lapisan bawah ke proses/aplikasi tujuan yang tepat berdasarkan identitas tertentu (seperti nomor port tujuan pada Transport layer atau EtherType pada Data Link layer).

### 10. Mengapa OSI tidak boleh dianggap sebagai spesifikasi implementasi?

- **Bersifat kerangka teoretis/konseptual:** model referensi OSI dirancang sebagai arsitektur acuan konseptual untuk mendefinisikan apa fungsi yang harus ada pada setiap lapisan, bukan bagaimana fungsi tersebut harus diprogram atau diimplementasikan dalam bentuk perangkat lunak/keras secara nyata.
- **Tidak efisien jika diterapkan kaku:** jika ketujuh lapisan OSI dipisahkan secara kaku dalam tumpukan sistem operasi, terjadi *overhead* kinerja dan pemrosesan yang sangat tinggi. Kenyataannya, protokol praktis seperti TCP/IP menggabungkan fungsi lapisan sesi, presentasi, dan aplikasi ke dalam satu lapisan aplikasi yang fleksibel di *user space* dengan prinsip berbasis pengujian nyata.

---

## Level B: Penerapan dan Analisis

### 11. Petakan HTTP, TLS, TCP, UDP, QUIC, IPv6, ICMP, Ethernet, Wi-Fi, dan DNS ke model TCP/IP. Tandai protokol yang pemetaannya memerlukan penjelasan.

- **Application Layer:**
  - HTTP, DNS
  - TLS\* (perlu penjelasan)
  - QUIC\* (perlu penjelasan)
- **Transport Layer:**
  - TCP, UDP
- **Internet Layer:**
  - IPv6
  - ICMP\* (perlu penjelasan)
- **Network Access / Link Layer:**
  - Ethernet, Wi-Fi (IEEE 802.11)

**Penjelasan protokol bertanda khusus:**

- **TLS:** berada di antara Transport dan Application; menyediakan enkripsi di ruang aplikasi sebelum data diserahkan ke TCP.
- **QUIC:** berjalan di atas UDP, namun bertindak mandiri sebagai protokol transport modern (menyediakan kontrol kemacetan, retransmisi, dan *multiplexing*) sekaligus mengintegrasikan TLS 1.3.
- **ICMP:** dienkapsulasi di dalam paket IP layaknya protokol transport, tetapi fungsinya adalah kendali, diagnosis, dan pelaporan eror untuk Lapisan Internet itu sendiri.

### 12. Gambarkan enkapsulasi permintaan DNS melalui UDP, IPv4, dan Ethernet. Sebutkan pengenal yang digunakan pada setiap batas.

```
[Ethernet Header] [IPv4 Header] [UDP Header] [DNS Query Payload] [Ethernet Trailer (FCS)]
```

**Pengenal (demultiplexing keys) pada setiap batas:**

- **Batas Ethernet → IPv4:** kolom EtherType pada header Ethernet bernilai `0x0800` (menandai muatan adalah IPv4).
- **Batas IPv4 → UDP:** kolom Protocol pada header IPv4 bernilai `17` (menandai muatan adalah UDP).
- **Batas UDP → DNS:** kolom Destination Port pada header UDP bernilai `53` (mengarahkan data ke layanan DNS).
- **Tingkat aplikasi (DNS):** kolom Transaction ID (TxID) di dalam payload DNS untuk mencocokkan respons dengan kueri awal.

### 13. Ulangi soal sebelumnya untuk HTTP/3 melalui QUIC. Jelaskan mengapa QUIC tetap dapat dianggap transport meskipun menggunakan UDP.

```
[Ethernet Header] [IP Header] [UDP Header] [QUIC Header + Encrypted Frame (HTTP/3)] [Ethernet Trailer]
```

**Pengenal pada setiap batas:**

- **Ethernet → IP:** EtherType `0x0800` (IPv4) atau `0x86DD` (IPv6).
- **IP → UDP:** Protocol `17` (UDP).
- **UDP → QUIC:** Destination Port `443`.
- **QUIC → HTTP/3:** Connection ID (CID) dan Stream ID untuk *multiplexing* frame stream data.

**Alasan QUIC dianggap transport:** UDP hanya difungsikan sebagai wadah transmisi datagram agar paket dapat melewati perangkat perantara Internet tanpa hambatan. Seluruh logika protokol transport (pembentukan koneksi, kontrol kemacetan, retransmisi paket hilang, dan *multiplexing* bebas *head-of-line blocking*) dieksekusi secara mandiri oleh arsitektur QUIC.

### 14. Dua host berada pada subnet berbeda. Jelaskan header mana yang berubah dan tetap ketika paket melewati satu router, dengan mengabaikan NAT.

**Header yang tetap:**

- **Transport Header (TCP/UDP):** Source Port, Destination Port, Sequence Number, dan flag kendali tidak mengalami perubahan.
- **IP Header:** Source IP Address dan Destination IP Address host asal dan tujuan tetap sama dari ujung ke ujung.

**Header yang berubah:**

- **Data Link Header:** berubah total pada setiap lompatan. MAC Address asal berganti menjadi MAC antarmuka keluar router, dan MAC Address tujuan berganti menjadi MAC host tujuan (atau router berikutnya).
- **IP Header:**
  - Nilai TTL (*Time to Live*) dikurangi satu oleh router.
  - Nilai IP Header Checksum dihitung ulang karena nilai TTL berubah.

### 15. Jelaskan perubahan analisis apabila router tersebut juga melakukan NAT/PAT.

Jika router menjalankan NAT/PAT:

- **Perubahan pada IP Header:**
  - Source IP Address (arah keluar) diganti dari IP privat host lokal menjadi IP publik router.
  - Destination IP Address (arah masuk/balasan) diganti dari IP publik router ke IP privat host lokal.
  - IP Header Checksum dihitung ulang.
- **Perubahan pada Transport Header (TCP/UDP):**
  - Source Port dapat dimodifikasi oleh router ke nomor port baru yang dialokasikan pada tabel terjemahan (*NAT translation table*) untuk mencegah tabrakan port antar-klien internal.
  - TCP/UDP Checksum wajib dihitung ulang karena perhitungan checksum transport melibatkan Pseudo-Header IP (yang memuat IP asal/tujuan) serta nomor port yang telah dimodifikasi.

### 16. Sebuah capture menunjukkan checksum TCP salah pada paket keluar, tetapi tidak ada gangguan komunikasi. Ajukan hipotesis yang berkaitan dengan NIC offload.

- **Hipotesis:** fitur *TCP Checksum Offload* / *Hardware Offloading* aktif pada kartu jaringan komputer pengirim.
- **Penjelasan:** aplikasi penganalisis paket (seperti Wireshark) menangkap paket pada antarmuka sistem operasi sebelum paket tersebut dikirimkan ke perangkat keras NIC. Sistem operasi sengaja mengosongkan atau mengisi nilai sembarang pada kolom TCP Checksum untuk menghemat siklus komputasi CPU, menyerahkan kalkulasi checksum matematis ke prosesor perangkat keras NIC saat transmisi fisik. Karena paket ditangkap sebelum melewati NIC, penganalisis menandainya sebagai *Checksum Bad/Incorrect*, padahal checksum yang terkirim ke media jaringan sudah valid.

### 17. Pengguna dapat membuka portal dengan alamat IP, tetapi tidak dengan nama. Gunakan model lapisan untuk menyusun diagnosis.

- **Status L1–L4 (Fisik hingga Transport):** normal, karena jalur fisik, perutean IP, dan koneksi port server terbukti terhubung saat dipanggil dengan IP.
- **Akar masalah di Application Layer (DNS):** kegagalan terjadi murni pada proses resolusi domain ke IP, yang bisa dipicu oleh IP DNS resolver klien salah/mati, port 53 (UDP/TCP) terblokir firewall, atau nama domain belum terdaftar/salah konfigurasi di server DNS.

### 18. Ping ke server berhasil, tetapi HTTPS gagal. Susun sedikitnya enam hipotesis pada lapisan Transport hingga Application.

- **Firewall memblokir port TCP 443 (Transport):** paket ICMP (ping) diizinkan lewat, tetapi paket SYN untuk koneksi HTTPS di-*drop*.
- **Web server mati / tidak aktif (Transport/Aplikasi):** layanan web (Nginx/Apache) tidak berjalan di server, menghasilkan respons penolakan (TCP RST).
- **Path MTU Discovery blackhole (Network/Transport):** paket ping kecil lolos, namun paket jabat tangan TLS yang besar tertahan karena melebihi MTU jaringan dan dibuang tanpa peringatan.
- **Ketidakcocokan versi TLS / cipher suite (Presentation – TLS):** klien dan server tidak memiliki kesepakatan versi enkripsi atau algoritma kriptografi yang cocok.
- **Validasi sertifikat gagal (Presentation/Aplikasi):** sertifikat SSL kedaluwarsa, tidak dipercaya, atau domain tidak cocok, sehingga peramban langsung memutus sesi.
- **Kegagalan server aplikasi / reverse proxy (Aplikasi):** server web mengalami *internal error* atau *bad gateway* (HTTP 500/502/504) saat memproses permintaan HTTPS.

### 19. Bandingkan sesi aplikasi dengan koneksi TCP. Berikan contoh ketika sesi bertahan setelah koneksi berubah.

- **Perbedaan singkat:** koneksi TCP (Layer 4) bersifat teknis dan kaku, terikat pada kombinasi IP dan nomor port; jika IP perangkat berubah, koneksi putus. Sebaliknya, sesi aplikasi (Layer 7) mengelola status pengguna (login, data belanja) melalui token atau cookie yang independen dari koneksi fisik.
- **Contoh:** saat ponsel berpindah dari Wi-Fi ke sinyal data seluler, IP perangkat berganti dan koneksi TCP terputus. Namun, sesi aplikasi tetap bertahan karena aplikasi memakai *session token* (misal: JWT/Cookie), sehingga pengguna tidak ter-*logout* dan unduhan/video langsung menyambung kembali.

### 20. Jelaskan mengapa enkripsi tidak dapat selalu ditempatkan secara mutlak pada Presentation layer.

- **Perlindungan jalur fisik (Layer 2 – MACsec):** mencegah penyadapan kabel antar-switch dengan mengenkripsi seluruh frame termasuk header IP.
- **Perlindungan jaringan antar-kantor (Layer 3 – IPsec):** menyembunyikan seluruh topologi IP internal dan port untuk koneksi VPN router-ke-router.
- **Perlindungan ujung-ke-ujung aplikasi (Layer 7):** mengenkripsi muatan data tertentu (misal: PIN/data transaksi) di tingkat aplikasi agar server perantara atau basis data tidak dapat membacanya meski sesi TLS transport telah dibuka.

Presentation layer tidak fleksibel untuk mengakomodasi seluruh skenario tersebut.

---

## Level C: Evaluasi dan Sintesis

### 21. Evaluasi pernyataan: "Model OSI tidak lagi relevan karena Internet menggunakan TCP/IP." Susun argumen akademik yang membedakan model, protokol, dan kegunaan pedagogis.

Pernyataan tersebut tidak tepat secara akademik.

- **Model vs. protokol:** TCP/IP adalah tumpukan protokol implementatif, sedangkan OSI adalah model acuan arsitektur konseptual. Kegagalan adopsi protokol OSI (seperti CLNP) tidak menghapus nilai analitis modelnya.
- **Kegunaan pedagogis dan kosakata industri:** OSI memberikan dekomposisi masalah yang terstruktur untuk pendidikan dan standardisasi bahasa teknis. Istilah modern seperti *Layer 2 switching*, *Layer 3 routing*, dan *Layer 7 inspection* semuanya berakar dari model referensi OSI.

### 22. Analisis keuntungan dan kerugian strict layering. Kapan cross-layer information dapat membantu dan kapan ia merusak modularitas?

- **Keuntungan strict layering:** menjamin modularitas tinggi, isolasi kegagalan, kemudahan standardisasi antarmuka, serta portabilitas kode aplikasi antar-media.
- **Kerugian strict layering:** mengurangi efisiensi performa dan memicu *information hiding* yang kaku (misalnya TCP mengira paket hilang selalu karena kemacetan antrean, bukan akibat sinyal radio buruk).
- **Kapan cross-layer membantu:** pada jaringan nirkabel/bergerak (Wi-Fi, 5G), di mana data kondisi kanal fisik (*Signal-to-Noise Ratio*) langsung dibagikan ke Transport/Application untuk mengatur bitrate streaming secara adaptif.
- **Kapan merusak modularitas:** ketika aplikasi bergantung langsung pada variabel perangkat keras tertentu, menyebabkan perangkat lunak menjadi kaku, rentan bug, dan sulit diperbarui ke arsitektur jaringan baru.

### 23. Buat prosedur penelusuran gangguan untuk kasus video konferensi yang tersendat hanya pada Wi-Fi kampus saat jam sibuk. Hubungkan bukti pada sedikitnya empat lapisan.

- **Lapisan 1 (Physical):** pindai spektrum RF; bukti berupa *channel utilization* >80%, interferensi tinggi pada pita 2.4/5 GHz, serta lonjakan *noise floor*.
- **Lapisan 2 (Data Link):** ambil statistik Access Point; bukti berupa tingginya *frame retry rate* (>30%) dan tunda antrean akibat tabrakan CSMA/CA di jam sibuk.
- **Lapisan 3 (Network):** jalankan pengujian ping dan MTR; bukti berupa lonjakan *jitter* (variasi latensi tinggi) dan hilangnya paket akibat *bufferbloat* pada router/AP.
- **Lapisan 4 (Transport):** periksa lalu lintas RTP/UDP di Wireshark; bukti berupa *packet loss* UDP >5% yang melampaui kemampuan pemulihan codec audio/video.

### 24. Rancang skenario laboratorium perekaman paket yang menunjukkan Ethernet, IP, TCP atau UDP, TLS, dan protokol aplikasi tanpa mengumpulkan data sensitif.

- **Topologi & konfigurasi:** klien dan web server lokal di lingkungan terisolasi, menyajikan halaman statis teks *dummy* non-sensitif menggunakan sertifikat SSL/TLS lokal.
- **Langkah kerja:** jalankan Wireshark pada antarmuka klien dengan filter `host <ip_server_lokal> and port 443`, lalu minta berkas via terminal (`curl -k https://<ip_server_lokal>/test.html`).
- **Bukti yang diamati:**
  - **Ethernet:** MAC header.
  - **IP:** header IP lokal.
  - **TCP:** *three-way handshake* (SYN, SYN-ACK, ACK).
  - **TLS:** Client Hello, penawaran cipher suite, dan sertifikat server.
  - **Aplikasi:** muatan berlabel *Encrypted Application Data* (isi data terlindungi dan tidak mengekspos informasi pribadi).

### 25. Sebuah organisasi menggunakan VXLAN di atas UDP dan IPsec tunnel. Gambarkan kemungkinan urutan header dan jelaskan risiko MTU.

```
[Outer Ethernet] [Outer IP (IPsec)] [ESP Header] [Underlay IP] [UDP (Port 4789)] [VXLAN] [Inner Ethernet] [Inner IP (VM)] [TCP/UDP Payload] [ESP Trailer/ICV]
```

**Risiko MTU:** VXLAN menambahkan beban header sebesar 50 byte, sedangkan IPsec mode tunnel menambah sekitar 50–70 byte. Jika MTU jaringan fisik adalah 1500 byte, kapasitas muatan efektif menyusut menjadi ~1370 byte. Paket VM berukuran 1500 byte dengan bit DF (*Don't Fragment*) akan langsung di-*drop* (*Path MTU Discovery blackhole*). Solusinya adalah mengaktifkan *Jumbo Frames* (MTU 1600 byte) pada switch underlay atau menerapkan *MSS clamping*.

### 26. Bandingkan perlindungan MACsec, IPsec, TLS, dan enkripsi end-to-end aplikasi dari sisi cakupan kepercayaan dan titik terminasi.

| Protokol | Lapisan | Titik Terminasi | Cakupan Kepercayaan (Trust Boundary) | Objek yang Dilindungi |
|---|---|---|---|---|
| MACsec | Layer 2 | Hop-ke-hop (antar dua switch/kartu jaringan langsung) | Hanya sebatas kabel fisik lokal tunggal | Seluruh frame Ethernet; didekripsi di setiap perangkat perantara |
| IPsec | Layer 3 | Gateway-ke-Gateway / Host-ke-Host | Antar-router/gateway VPN | Menyembunyikan IP host asli dan seluruh port/payload L4–L7 (mode tunnel) |
| TLS | Layer 4/7 | Klien ke Server Web (atau Reverse Proxy/CDN) | Antar-proses soket aplikasi pengguna dengan server terminasi | Mengamankan transmisi muatan aplikasi; IP dan port jaringan tetap terlihat oleh ISP |
| E2E Aplikasi | Layer 7 | Antar-klien pengguna akhir secara langsung | Ujung-ke-ujung murni (*Zero-Trust Server*) | Isi payload data terlindungi mutlak; server transit/cloud tidak dapat membaca data mentah |

### 27. Jelaskan bagaimana firewall, proxy, dan load balancer menantang anggapan bahwa setiap perangkat hanya membaca header lapisannya.

- **Next-Generation Firewall (NGFW):** berada di jalur transmisi, tetapi melakukan *Deep Packet Inspection* (DPI) hingga L7 untuk mendeteksi ancaman malware di dalam muatan data.
- **Reverse Proxy / WAF:** berfungsi sebagai perantara yang menamatkan sesi TCP/TLS, membaca konten payload HTTP/JSON secara penuh, lalu membentuk koneksi baru ke server internal.
- **Layer 7 Load Balancer:** membuka muatan aplikasi untuk memeriksa URL path, header HTTP, atau cookie sebelum menentukan tujuan perutean server *backend*.

### 28. Gunakan prinsip end-to-end untuk mengevaluasi penempatan fungsi pemeriksaan integritas berkas pada router, transport, atau aplikasi.

- **Di router (L2/L3):** tidak mencukupi; checksum Ethernet/IP hanya memeriksa eror transmisi pada tautan kabel individual dan tidak mendeteksi kerusakan bit di memori router atau bug sistem internal.
- **Di lapisan transport (L4):** checksum TCP hanya 16-bit sederhana dan tidak menjamin integritas berkas saat tersimpan di disk atau buffer memori OS.
- **Di lapisan aplikasi (L7):** penempatan paling tepat. Aplikasi menghitung tanda tangan digital atau *cryptographic hash* (seperti SHA-256) dari berkas asli, sehingga penerima dapat memverifikasi keutuhan berkas secara menyeluruh dari awal pembuatan hingga penyimpanan akhir.

### 29. Analisis potensi retry storm ketika aplikasi, service mesh, dan client sama-sama melakukan pengulangan. Jelaskan mengapa masalah ini bersifat lintas lapisan.

- **Mekanisme retry storm:** ketika layanan *backend* lambat, Lapisan Aplikasi (klien HTTP) melakukan *retry*, *Service Mesh* (Envoy/Istio) melakukan *retry* internal, dan Lapisan Transport (TCP) mengulang segmen data yang belum ter-ACK. Jika masing-masing komponen mencoba ulang 3 kali, satu permintaan gagal dapat berlipat ganda menjadi puluhan permintaan, menciptakan badai lalu lintas (*traffic storm*) yang menumbangkan server yang sedang kritis (*cascading failure*).
- **Mengapa bersifat lintas lapisan:** masalah ini muncul karena loop kendali pada Transport (TCP timeout), Lapisan Sesi/Infrastruktur (service mesh timeout), dan Lapisan Aplikasi berjalan sendiri-sendiri tanpa sinkronisasi status. Solusinya memerlukan strategi lintas batas seperti *exponential backoff with jitter*, pembatasan kuota *retry*, dan pola *circuit breaker*.

### 30. Susun argumen apakah materi jaringan pemula sebaiknya memakai model OSI tujuh lapisan, TCP/IP empat lapisan, atau model lima lapisan. Nyatakan tujuan pembelajaran, manfaat, dan keterbatasan pilihan Anda.

- **Pilihan terbaik:** model hibrida lima lapisan (Physical, Data Link, Network, Transport, Application).
- **Tujuan pembelajaran:** membangun pemahaman komprehensif yang menjembatani transmisi perangkat keras fisik hingga pemrograman aplikasi jaringan nyata.
- **Manfaat:**
  - Memperbaiki keterbatasan model TCP/IP 4-lapisan yang menggabungkan Physical dan Data Link menjadi satu, sehingga mahasiswa pemula dapat membedakan dengan tegas peran media sinyal (L1) dan mekanisme *switching*/*framing* MAC (L2).
  - Menghilangkan kerumitan teoretis dari pemisahan lapisan Session dan Presentation pada model OSI 7-lapisan yang jarang diimplementasikan secara terisolasi pada tumpukan protokol modern.
- **Keterbatasan:** model lima lapisan merupakan model pengajaran pedagogis dan bukan standar resmi ISO/IETF, sehingga pengajar tetap perlu mengenalkan penomoran 7 lapisan OSI agar mahasiswa tidak asing dengan terminologi sertifikasi industri (misal: CCNA).
