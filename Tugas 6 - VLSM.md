# Laporan Tugas Konsep Jaringan: VLSM

Sebuah kampus memiliki alokasi jaringan **10.252.108.0/24** yang akan dibagi untuk empat segmen dengan kebutuhan host sebagai berikut:

| Segmen | Kebutuhan Host |
|--------|----------------|
| Laboratorium A | 90 host |
| Laboratorium B | 60 host |
| Administrasi | 14 host |
| Tautan Point-to-Point | 4 endpoint |

Tentukan untuk setiap segmen:

- IP Network
- Host Pertama
- Host Terakhir
- Broadcast
- Subnet Mask (prefix baru)
- Jumlah host yang tersedia

## Jawaban

| Kebutuhan | Network | Host Range | Broadcast | Prefix | Host terpakai |
|---|---|---|---|---|---|
| Lab A (90) | 10.252.108.0 | 10.252.108.1 – 10.252.108.126 | 10.252.108.127 | /25 | .1 – .90 |
| Lab B (60) | 10.252.108.128 | 10.252.108.129 – 10.252.108.190 | 10.252.108.191 | /26 | .129 – .188 |
| Admin (14) | 10.252.108.192 | 10.252.108.193 – 10.252.108.206 | 10.252.108.207 | /28 | .193 – .206 |
| P2P (4) | 10.252.108.208 | 10.252.108.209 – 10.252.108.214 | 10.252.108.215 | /29 | .209 – .212 |
