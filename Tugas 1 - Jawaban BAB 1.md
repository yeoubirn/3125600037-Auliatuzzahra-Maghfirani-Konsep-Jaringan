# Tugas Konsep Jaringan: Pengantar Jaringan Komputer dan Internet

## A. Level A: Ingatan dan Pemahaman

### 1. Jelaskan pengertian jaringan komputer dengan menyebutkan empat unsur pokoknya.

Jaringan komputer adalah sekumpulan perangkat otonom yang sering terhubung melalui satu/lebih media komunikasi untuk bertukar data dan berbagi sumber daya berdasarkan aturan komunikasi yang disepakati. Empat unsur pokoknya:

1. **Perangkat akhir (end system)**: sumber atau tujuan data, misalnya laptop, server, atau sensor.
2. **Media komunikasi**: pembawa sinyal, misalnya kabel tembaga, serat optik, dan gelombang radio.
3. **Perangkat perantara**: meneruskan/mengendalikan/melindungi lalu lintas, misalnya router, switch, firewall.
4. **Protokol**: aturan format pesan, urutan pertukaran, dan penanganan kesalahan.

### 2. Apa yang dimaksud dengan perangkat otonom dalam definisi jaringan?

Setiap perangkat yang terhubung tetap memiliki fungsi dan kendali komputasinya sendiri, tidak kehilangan identitas atau kendali internalnya ketika bergabung ke jaringan.

### 3. Bedakan data, sinyal, dan paket.

- **Data**: representasi informasi dalam bentuk bit.
- **Sinyal**: bentuk fisik yang membawa representasi data tersebut melalui media.
- **Paket**: unit data yang kecil hasil dari pembagian data aplikasi besar, dilengkapi informasi kendali agar dapat diteruskan oleh jaringan berbasis paket.

### 4. Jelaskan perbedaan PAN, LAN, MAN, dan WAN tanpa hanya menggunakan ukuran jarak.

- **PAN (Personal Area Network)**: sekitar individu, dikelola perorangan, teknologi seperti Bluetooth/NFC.
- **LAN (Local Area Network)**: rumah/gedung/kampus, kendali administratif terpadu oleh satu organisasi/rumah tangga, teknologi Ethernet/Wi-Fi.
- **MAN (Metropolitan Area Network)**: beberapa lokasi dalam satu kawasan metropolitan, biasanya disediakan operator (Metro Ethernet, serat metropolitan), ada batas tanggung jawab pelanggan-penyedia.
- **WAN (Wide Area Network)**: menghubungkan lokasi berjauhan, umumnya melibatkan infrastruktur operator (leased line, MPLS, VPN, SD-WAN, satelit), menuntut perhatian pada latensi dan keragaman jalur.

### 5. Apa perbedaan intranet, ekstranet, dan Internet publik?

- **Intranet**: layanan internal berbasis internet, akses terbatas hanya untuk anggota organisasi.
- **Ekstranet**: memperluas layanan internal kepada pihak eksternal terotorisasi dengan akses minimum sesuai kebutuhan.
- **Internet publik**: keterhubungan terbuka antar banyak jaringan namun tetap dapat menerapkan kendali akses pada layanan tertentu.

### 6. Mengapa Wi-Fi tidak dapat disamakan dengan Internet?

Wi-Fi hanyalah teknologi akses lokal nirkabel yang menghubungkan perangkat ke jaringan setempat, dan perangkat bisa terhubung ke Wi-Fi tanpa memiliki jalur ke Internet. Internet adalah interkoneksi global jaringan-jaringan, sedangkan Wi-Fi hanyalah salah satu cara mengakses jaringan tersebut.

### 7. Jelaskan perbedaan client, server, dan peer.

- **Client**: pihak yang meminta layanan.
- **Server**: pihak yang menyediakan layanan, umumnya melayani banyak client dan beroperasi terus-menerus.
- **Peer**: dalam arsitektur P2P, setiap node dapat bertindak sekaligus sebagai peminta dan penyedia sumber daya, tanpa peran client/server yang tetap.

### 8. Apa perbedaan bandwidth, throughput, dan goodput?

- **Bandwidth**: kapasitas nominal/teoritis suatu kanal atau tautan.
- **Throughput**: laju data aktual yang berhasil dipindahkan, termasuk sebagian overhead protokol.
- **Goodput**: laju muatan data aplikasi yang benar-benar berguna bagi pengguna, tidak menghitung header dan pengiriman ulang.

### 9. Sebutkan empat komponen nodal delay.

Processing delay, queuing delay, transmission delay, dan propagation delay, dijumlahkan sebagai:

$$d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$$

### 10. Mengapa Web tidak sama dengan Internet?

Internet adalah infrastruktur jaringan dan protokol global (IP, TCP, routing, dsb.), sedangkan Web adalah salah satu layanan aplikasi yang berjalan di atas infrastruktur tersebut (menggunakan HTTP, HTML, URL).

---

## B. Level B: Penerapan dan Analisis

### 1. Sebuah paket berukuran 1.000 byte dikirim melalui tautan 10 Mbps. Hitung transmission delay ideal paket tersebut. Jelaskan komponen delay yang belum tercakup.

![Perhitungan transmission delay](images/pengantar-transmission-delay.png)

Komponen delay yang belum tercakup: *processing delay* (waktu perangkat memeriksa header), *queuing delay* (waktu menunggu di buffer akibat kepadatan lalu lintas), dan *propagation delay* (waktu sinyal merambat sepanjang jarak fisik media). Nilai 0,8 ms hanya menggambarkan waktu serialisasi paket ke tautan, bukan total waktu paket sampai ke tujuan.

### 2. Sebuah kampus memiliki koneksi Internet 2 Gbps, tetapi pengguna di satu lantai hanya memperoleh throughput rendah. Susun sedikitnya lima hipotesis yang tidak langsung menyalahkan koneksi ISP.

- Access point di lantai tersebut kelebihan beban atau ditempatkan buruk sehingga sinyal lemah/interferensi.
- Kesalahan konfigurasi VLAN/switch pada segmen lantai itu.
- Uplink dari switch lantai ke distribution/core berkapasitas kecil (bottleneck lokal), bukan koneksi Internet global.
- Interferensi radio dari perangkat lain pada kanal Wi-Fi yang sama.
- Pembatasan bandwidth per pengguna/VLAN yang diterapkan secara tidak sengaja terlalu ketat di segmen tersebut.

### 3. Bandingkan kebutuhan jaringan untuk transfer berkas cadangan dan panggilan video. Metrik apa yang paling penting bagi masing-masing aplikasi?

- **Transfer berkas cadangan**: mengutamakan throughput/kapasitas tinggi secara agregat, toleran terhadap delay dan jitter (longgar), loss harus sangat rendah karena integritas data penting.
- **Panggilan video**: mengutamakan latency rendah dan jitter rendah karena sifatnya real-time interaktif; throughput sedang-tinggi tapi lebih fleksibel, sedikit packet loss dapat ditoleransi dengan mekanisme adaptasi, karena data yang terlambat sudah tidak berguna.

### 4. Sebuah organisasi mempunyai dua koneksi Internet dari dua operator. Keduanya melewati tiang dan jalur ducting yang sama. Evaluasi kualitas redundansinya.

Redundansi tidak efektif. Meski secara logis ada dua jalur dari dua operator berbeda, keduanya berbagi *failure domain* fisik yang sama. Jika terjadi kegagalan fisik tunggal, kedua koneksi dapat terputus bersamaan. Redundansi yang baik harus dirancang berdasarkan analisis failure domain termasuk jalur fisik, sumber listrik, dan titik masuk gedung, bukan hanya jumlah operator/perangkat.

### 5. Jelaskan mengapa penambahan bandwidth tidak selalu mengurangi waktu akses ke server yang sangat jauh.

Karena waktu akses juga dipengaruhi *propagation delay*, yaitu waktu sinyal merambat sepanjang jarak fisik, yang ditentukan oleh jarak dan kecepatan rambat media, bukan oleh kapasitas tautan. Menambah bandwidth hanya mengurangi transmission delay (waktu serialisasi), tidak mengubah jarak fisik. Untuk server yang sangat jauh, propagation delay bisa mendominasi total delay, sehingga solusi yang lebih efektif adalah mendekatkan konten/komputasi ke pengguna (CDN, edge computing, pusat data regional).

### 6. Sebuah layanan tersedia 99,9% selama satu tahun. Hitung perkiraan maksimum durasi ketidaktersediaannya. Bandingkan dengan target 99,99%.

- Total menit dalam setahun (365 hari) = 525.600 menit.
- Ketidaktersediaan 99,9% = 0,1% × 525.600 = 525,6 menit ≈ 8 jam 46 menit.
- Ketidaktersediaan 99,99% = 0,01% × 525.600 = 52,56 menit ≈ 52 menit.

### 7. Analisis kelebihan dan kelemahan client–server serta P2P untuk distribusi berkas berukuran besar kepada ribuan pengguna.

- **Client-server**: kelebihannya konsisten dalam pengelolaan (kontrol versi, autentikasi, pencatatan terpusat), tapi server dapat menjadi bottleneck dan titik kegagalan tunggal ketika permintaan sangat banyak; membutuhkan kapasitas/infrastruktur besar (atau load balancer dan banyak instance) untuk skala ribuan pengguna.
- **P2P**: berpotensi skalabilitas lebih baik karena setiap peer yang mengunduh juga dapat berbagi ke peer lain, sehingga kapasitas distribusi bertambah seiring jumlah peserta; risikonya ada pada penemuan peer, konsistensi data, kepercayaan/keamanan, dan pengelolaan peer yang keluar-masuk. P2P sering tetap memerlukan server untuk koordinasi awal atau pelacakan (tracker).

### 8. Berikan contoh ketika topologi fisik dan topologi logis pada jaringan kampus berbeda.

Secara fisik seluruh perangkat di suatu gedung terhubung ke satu switch pusat membentuk topologi *star* (semua kabel menuju satu titik). Namun secara logis, switch tersebut dapat mengelola beberapa VLAN (misalnya VLAN mahasiswa, VLAN staf, VLAN kamera pengawas) yang masing-masing membentuk domain broadcast dan jalur routing tersendiri, sehingga secara logis jaringan tersebut tersegmentasi menjadi beberapa jaringan terpisah meski secara fisik terhubung ke perangkat yang sama.

---

## C. Level C: Evaluasi dan Sintesis

### 1. Rancang klasifikasi kebutuhan jaringan kampus untuk mahasiswa, staf administrasi, tamu, kamera pengawas, dan laboratorium riset. Jelaskan alasan segmentasi dan aturan komunikasi utamanya.

| Kelompok | Kebutuhan akses | Segmentasi (VLAN/subnet) | Aturan komunikasi utama |
|---|---|---|---|
| Mahasiswa | Sistem pembelajaran, Internet umum | VLAN mahasiswa | Boleh ke Internet & portal akademik; dibatasi ke sistem administrasi |
| Staf administrasi | Data sensitif (keuangan, akademik) | VLAN staf, terpisah dari mahasiswa | Akses lebih luas ke sistem internal; enkripsi & autentikasi lebih ketat |
| Tamu | Internet publik saja | VLAN tamu terisolasi | Tidak boleh mengakses jaringan internal sama sekali |
| Kamera pengawas | Ke server perekam saja | VLAN terisolasi, tanpa akses Internet bebas | Komunikasi satu arah/terbatas ke server perekam; tanpa akses ke VLAN lain |
| Lab riset | Bandwidth besar, mungkin protokol non-standar | VLAN/subnet terpisah dengan kebijakan longgar untuk eksperimen | Dibatasi agar lalu lintas tidak mengganggu VLAN lain, dipantau ketat |

### 2. Evaluasi pernyataan: "Jaringan internal tidak memerlukan enkripsi karena sudah dilindungi firewall." Gunakan prinsip kerahasiaan, integritas, dan ketersediaan.

Firewall terutama menjaga ketersediaan dan kontrol akses di batas jaringan (perimeter), tapi tidak melindungi kerahasiaan data yang mengalir di dalam jaringan internal; data yang tidak dienkripsi tetap dapat disadap oleh pihak yang sudah berada di dalam jaringan. Firewall juga tidak menjamin integritas data yang berpindah antarnode. Ancaman dari dalam tidak tercegah oleh firewall perimeter saja. Karena itu enkripsi dan verifikasi identitas tetap diperlukan di dalam jaringan, sejalan dengan prinsip "keamanan sebagai sifat sistem", bukan perangkat tunggal.

### 3. Diskusikan mengapa Internet dapat berkembang tanpa otoritas teknis pusat tunggal. Jelaskan manfaat serta risikonya.

Internet dapat berkembang karena bersifat jaringan dari jaringan: setiap organisasi mengelola *autonomous system*-nya sendiri dan saling terhubung melalui kesepakatan teknis terbuka (protokol standar seperti TCP/IP, BGP) yang dikembangkan secara kolaboratif (IETF, RFC).

- **Manfaat**: fleksibilitas berinovasi tanpa menunggu persetujuan otoritas tunggal, ketahanan terhadap kegagalan sebagian komponen, dan pertumbuhan skala global yang cepat karena banyak pihak dapat berpartisipasi.
- **Risiko**: koordinasi menjadi kompleks (kesalahan pengumuman rute BGP oleh satu operator bisa berdampak lintas wilayah), tidak ada pihak tunggal yang bertanggung jawab penuh atas insiden global, serta kebutuhan besar akan standar terbuka dan praktik operasional bersama agar interoperabilitas tetap terjaga.

### 4. Bandingkan circuit switching dan packet switching untuk layanan suara. Jelaskan mengapa suara modern tetap dapat berjalan pada jaringan paket.

- **Circuit switching**: sumber daya jalur dialokasikan penuh selama sesi berlangsung, memberi prediktabilitas tinggi (delay konsisten) tapi boros karena kapasitas menganggur saat tidak ada suara yang dikirim.
- **Packet switching**: kapasitas dibagi secara dinamis antarpengguna (*statistical multiplexing*), lebih efisien untuk lalu lintas yang bersifat *bursty*.

Suara modern (VoIP) tetap dapat berjalan baik di jaringan paket karena:

- (a) suara terkompresi menjadi paket kecil yang dikirim berkala,
- (b) mekanisme *jitter buffer* menyerap variasi delay antarpaket,
- (c) sedikit packet loss dapat ditoleransi tanpa terlalu mengganggu kualitas persepsi, dan
- (d) kapasitas jaringan modern umumnya cukup besar sehingga delay dan jitter dapat ditekan ke level yang dapat diterima untuk komunikasi real-time.

### 5. Ambil satu keluhan nyata atau hipotetis berupa "Internet lambat". Susun prosedur pengumpulan bukti, pengujian hipotesis, dan kriteria keberhasilan perbaikannya.

- **Tentukan ruang lingkup**: apakah dialami satu pengguna, satu ruangan, atau seluruh kampus.
- **Tentukan waktu**: terus-menerus, periodik, atau hanya jam sibuk.
- **Pisahkan akses lokal dan tujuan**: uji apakah gateway lokal terjangkau, dan apakah hanya satu aplikasi yang bermasalah atau semua.
- **Ukur**: catat RTT, packet loss, throughput, utilisasi uplink, kekuatan sinyal Wi-Fi.
- **Bandingkan dengan baseline**: apakah angka yang diukur menyimpang dari kondisi normal sebelumnya.
- **Uji satu hipotesis pada satu waktu**: misalnya coba ganti kanal Wi-Fi, lalu evaluasi; jangan ubah banyak hal sekaligus.
- **Periksa dependency**: apakah DNS, sertifikat, autentikasi, atau layanan pihak ketiga yang menjadi penyebab, bukan jaringan itu sendiri.
- **Kriteria keberhasilan**: metrik terukur (misalnya RTT dan throughput kembali ke rentang baseline, packet loss di bawah ambang tertentu) yang dicek kembali setelah perbaikan, bukan sekadar "pengguna tidak mengeluh lagi".
- **Dokumentasikan** temuan dan solusi untuk mempercepat penanganan kejadian serupa berikutnya.

### 6. Kunjungi statistik IPv6 Google atau sumber pengukuran APNIC. Catat tanggal, definisi metrik, populasi yang diukur, dan nilai untuk Indonesia. Jelaskan mengapa angka dari dua sumber dapat berbeda.

Pada 7 Juli 2026, halaman Google IPv6 Statistics menunjukkan adopsi global sekitar 46,69% (perlu diverifikasi ulang karena berubah harian). Metodologi Google mengukur proporsi pengguna yang mengakses layanannya melalui IPv6, sedangkan APNIC menggunakan metodologi eksperimen iklan untuk menaksir kapabilitas pengguna.

Angka dari dua sumber dapat berbeda karena:

- (a) populasi yang diukur berbeda (pengguna layanan Google vs pengguna yang terjangkau iklan APNIC),
- (b) metode pengukuran berbeda (traffic langsung vs eksperimen iklan), dan
- (c) waktu snapshot berbeda, sehingga nilai berubah dari hari ke hari.

> Catatan: untuk angka Indonesia yang spesifik dan terkini, perlu dicek langsung ke situs Google IPv6 Statistics atau APNIC Labs karena datanya dinamis.

### 7. Buat argumen mengenai penggunaan satelit orbit rendah sebagai koneksi utama atau cadangan bagi kampus di wilayah terpencil. Nilai kinerja, biaya, ketergantungan cuaca, pengelolaan, dan keamanan.

- **Kinerja**: LEO menawarkan propagation delay jauh lebih rendah dibanding satelit geostasioner, mendekati kualitas terestrial untuk aplikasi interaktif, namun tetap dipengaruhi kepadatan pelanggan, gateway, dan cuaca (terutama hujan lebat).
- **Biaya**: perangkat terminal dan biaya langganan relatif lebih tinggi dibanding koneksi terestrial biasa, tapi jauh lebih murah dibanding membangun serat baru ke lokasi sangat terpencil.
- **Ketergantungan cuaca**: sinyal dapat terganggu cuaca ekstrem, sehingga kurang cocok sebagai satu-satunya jalur untuk layanan kritis.
- **Pengelolaan**: memerlukan koordinasi dengan penyedia layanan satelit dan pemantauan kualitas sinyal secara berkala.
- **Keamanan**: perlu memastikan enkripsi end-to-end dan kebijakan akses tetap diterapkan setara jaringan terestrial.

### 8. Jelaskan bagaimana otomatisasi jaringan dapat meningkatkan konsistensi sekaligus memperbesar dampak kesalahan. Usulkan kontrol teknis dan proses untuk mengurangi risiko tersebut.

Otomasi meningkatkan konsistensi karena konfigurasi diterapkan seragam tanpa kesalahan manual berulang, dan mempercepat respons terhadap perubahan skala besar. Namun, otomasi juga dapat menyebarkan kesalahan dengan sangat cepat: jika skrip atau kebijakan salah, kesalahan tersebut dapat diterapkan ke seluruh jaringan hampir seketika, jauh lebih cepat daripada kesalahan manual yang biasanya terbatas pada satu perangkat.

Usulan kontrol untuk mengurangi risiko:

- Validasi dan pengujian bertahap (*staged rollout*) sebelum penerapan penuh ke seluruh jaringan.
- Mekanisme *rollback*/pengembalian otomatis jika terdeteksi anomali setelah perubahan.
- Sumber kebenaran tunggal (*single source of truth*) untuk konfigurasi, agar perubahan dapat dilacak dan diaudit.
- Batas kewenangan otomasi (*approval gate*) untuk perubahan berdampak besar, tetap melibatkan penalaran dan akuntabilitas manusia.
- Pemantauan dan *observability* yang memadai untuk mendeteksi dampak tak terduga secepat mungkin setelah perubahan diterapkan.

---

## D. Penjelasan Kabel UTP

UTP adalah kabel jaringan berisi beberapa pasang kawat tembaga yang dipilin (*twisted pair*) satu sama lain tanpa pelindung logam (*shield*) tambahan di luarnya. Fungsi pilinan ini untuk mengurangi interferensi elektromagnetik antar pasangan kabel (*crosstalk*). Semakin tinggi nomor kategorinya, umumnya semakin rapat pilinannya, semakin tinggi frekuensi yang bisa dilewatkan, dan semakin tinggi kecepatan data yang didukung.

### 1. CAT 1

- Tahun: sekitar awal 1980-an
- Kecepatan: ±1 Mbps
- Awalnya dipakai untuk kabel telepon analog biasa (POTS)
- Tidak dipilin (untwisted), sehingga tidak cocok dan tidak pernah dipakai untuk jaringan komputer/data
- Bukan standar resmi TIA/EIA, sebutan tidak resmi

### 2. CAT 2

- Tahun: 1980-an
- Kecepatan: hingga 4 Mbps
- Sempat dipakai pada jaringan IBM Token Ring dan ARCnet
- Juga bukan standar resmi TIA/EIA, sudah tidak dipakai lagi

### 3. CAT 3

- Tahun: 1980-an
- Kecepatan: hingga 4 Mbps
- Sempat dipakai pada jaringan IBM Token Ring dan ARCnet
- Juga bukan standar resmi TIA/EIA, sudah tidak dipakai lagi

### 4. CAT 4

- Tahun: 1990-an
- Kecepatan: hingga 16 Mbps, frekuensi 20 MHz
- Dipakai pada Token Ring 16 Mbps
- Cepat tergantikan karena CAT 5 muncul dengan performa jauh lebih baik

### 5. CAT 5

- Tahun: pertengahan 1990-an
- Kecepatan: hingga 100 Mbps, frekuensi 100 MHz
- Mendukung 100BASE-TX (Fast Ethernet)
- Sudah usang; resmi digantikan CAT 5e sejak 2001

### 6. CAT 6

- Tahun: dipublikasikan TIA Juni 2002
- Kecepatan: 1 Gbps penuh (100 m), atau 10 Gbps pada jarak pendek (~37-55 m)
- Frekuensi: 250 MHz
- Presisi produksi lebih tinggi, biasanya ada separator plastik di dalam untuk memisahkan pasangan kabel dan mengurangi crosstalk

### 7. CAT 6a

- Tahun: sekitar 2008-2009
- Kecepatan: 10 Gbps penuh hingga 100 meter
- Frekuensi: 500 MHz
- Karakteristik alien crosstalk jauh lebih baik dari CAT 6 biasa

### 8. CAT 7

- Tahun: sekitar 2010-an (standar ISO/IEC, bukan TIA)
- Kecepatan: 10 Gbps
- Frekuensi: 600 MHz
- Setiap pasangan kabel dilindungi shield individu, ditambah shield keseluruhan (jadi sebenarnya sudah S/FTP, bukan UTP murni lagi)
- Semua komponen (konektor, patch panel, jack) harus tersertifikasi CAT 7 agar performanya tercapai

### 9. CAT 8

- Tahun: 2016 (standar resmi TIA)
- Kecepatan: 25-40 Gbps
- Frekuensi: 2000 MHz (2 GHz)
- Jarak efektif pendek, maksimal sekitar 30 meter
- Ditujukan untuk koneksi antar-rak di data center, bukan untuk instalasi gedung biasa

### 10. CAT 9

- Sampai sekarang belum ada standar resmi dari TIA maupun ISO/IEC
- Kategori tertinggi yang diakui resmi saat ini tetap CAT 8
- Jika ada produk yang mengklaim "CAT 9" di pasaran, itu istilah marketing/tidak resmi, bukan standar baku industri

---

## E. Standar Wi-Fi (802.11 a/b/g/n/ac/ax)

Wi-Fi pertama kali dirilis ke konsumen pada 1997, dan setiap penambahan kemampuan pada standar 802.11 asli diberi kode huruf tambahan (802.11b, 802.11g, dst).

- **802.11 (1997)**: standar awal, kecepatan maksimum teoretis 2 Mbps, sudah tidak dipakai lagi.
- **802.11b (1999)**: beroperasi di pita 2,4 GHz, kecepatan data teoretis maksimum 11 Mbps, memakai metode akses CSMA/CA dan modulasi CCK; populer karena murah dan cukup cepat untuk kebutuhan rumahan saat itu.
- **802.11a (1999)**: beroperasi di 5 GHz, kecepatan maksimum 54 Mbps; dirilis bersamaan dengan 802.11b tapi lebih banyak dipakai di lingkungan enterprise karena harga perangkat lebih mahal.
- **802.11g (2003)**: tetap di pita 2,4 GHz namun kompatibel dengan 802.11b, kecepatan naik menjadi 54 Mbps.
- **802.11n / Wi-Fi 4 (2009)**: mendukung pita 2,4 GHz dan 5 GHz sekaligus, memperkenalkan fitur MIMO (multi-antena), kecepatan per-channel bisa mencapai 150 Mbps (implementasi tertentu bahkan hingga 450 Mbps).
- **802.11ac / Wi-Fi 5 (2014)**: kecepatan data maksimum hingga 1300 Mbps, mendukung MU-MIMO dan dual-band (2,4 GHz & 5 GHz).
- **802.11ax / Wi-Fi 6 (2019)**: menawarkan kecepatan data hingga 10 Gbps, 30–40% lebih cepat dari 802.11ac, mendukung dual-band, MU-MIMO, dan antena hingga 8×8.

---

## F. Sejarah & Timeline Internet

- **1957**: Uni Soviet meluncurkan Sputnik; Departemen Pertahanan AS membentuk ARPA (Advanced Research Projects Agency) untuk mendorong riset teknologi sebagai respons.
- **1969**: ARPANET resmi diluncurkan, menghubungkan empat universitas AS: UCLA, Stanford Research Institute (SRI), UC Santa Barbara, dan University of Utah. Pesan pertama yang dikirim adalah kata "LOGIN", tapi sistem crash setelah huruf "LO" terkirim.
- **1973**: ARPANET mulai menghubungkan jaringan di luar AS, seperti Inggris dan Norwegia.
- **1983 (1 Januari)**: protokol TCP/IP resmi digunakan sebagai fondasi utama Internet, memungkinkan berbagai jaringan komputer berbeda saling terhubung.
- **1980-an**: Domain Name System (DNS) diperkenalkan agar pengguna bisa memakai nama domain (mis. google.com) ketimbang alamat IP.
- **1990**: ARPANET resmi dipensiunkan; Tim Berners-Lee (CERN) mengembangkan World Wide Web (WWW) berbasis tampilan grafis.
- **1991**: situs web pertama di dunia dipublikasikan oleh Tim Berners-Lee.
- **1993**: InterNIC didirikan untuk melayani pendaftaran nama domain publik.
- **1994**: Internet mulai masuk ke Indonesia, dikenal dengan nama Paguyuban Network.
- **Pertengahan–akhir 1990-an**: booming dot-com, pertumbuhan pesat perusahaan teknologi/startup internet dan e-commerce.
- **2010-an – sekarang**: Internet semakin cepat dengan hadirnya jaringan 4G/5G, meningkatnya cloud computing, IoT, dan kecerdasan buatan (AI).
