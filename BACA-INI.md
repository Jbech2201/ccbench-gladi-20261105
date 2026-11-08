# Gladi koneksi 2026-11-05 — BUKAN hasil penelitian final

Diambil dari `pep-star01:~/` ke laptop pada 2026-11-06 atas keputusan operator.
Semua isi folder ini adalah **pengukuran paket nyata** (bukan emulasi, bukan
simulasi), tetapi **jalurnya bukan Starlink**, sehingga tidak dipakai sebagai
hasil penelitian.

## Mengapa bukan Starlink

Sembilan sel matriks 2026-11-05 berjalan lewat endpoint Tailscale
`192.168.31.101:41641`. Dari pep-star01, alamat itu dijangkau sebagai

    192.168.31.101 via 192.168.0.1 dev wlp13s0

yaitu melalui gateway pep-star01 sendiri di jaringan kampus USK. Egress
pep-star01 ke internet pun terestrial:

    1 192.168.31.1  2.250 ms
    2 172.16.2.1    2.002 ms
    3 202.4.186.1   2.435 ms      <- edge publik USK
    4 36.93.250.225 2.557 ms      <- Telkom

Jadi paketnya tidak pernah naik ke satelit. `docs/decisions/008` di repo
`ccbench-remote` sudah menuliskan sifat jalur ini sejak awal: *"when Tailscale
finds that route the WAN path is not a WAN path at all."* Uraian lengkapnya di
`docs/decisions/012-starlink-path-is-star02-to-cbr2.md`.

## Isi

| Folder | Apa | Status |
|---|---|---|
| `ccbench-matrix-20261105T004038Z` | 4 × 1 jam uplink (indigo 2.929 Mbps, taova 2.582, vivace 1.654) + 5 slot referensi cubic yang sepakat (CV 4.6% tput) | jalur kampus; `pcc` gagal di 65% durasi |
| `ccbench-matrix-20261105T054527Z` | ulangan `pcc` 1 jam penuh setelah patch 0007 (2.425 Mbps, p95 716.6 ms) | jalur kampus |
| `ccbench-dlsmoke-20261105T081524Z` | smoke downlink 120 s, MTU default → bukti `taova` loss 65% dan `vivace` 35% | dasar patch 0008 |
| `ccbench-mtutest-20261105T083351Z` | run yang menggantung 6 j 45 m karena `--local-if` + rp_filter | dasar patch 0008 bagian (b) |

## Masih berguna untuk apa

1. **Bab metode**: bukti bahwa harness-nya bekerja ujung ke ujung selama 4 jam,
   dan bahwa slot referensi `cubic` memang mendeteksi kestabilan jalur.
2. **Pembanding terestrial** terhadap matriks Starlink nanti, kalau memang mau
   ditulis sebagai pembanding — dengan jalurnya disebut eksplisit.
3. **Dua temuan patch** (0007 dan 0008) yang reproduksinya ada di sini.

Jangan kutip angka dari folder ini sebagai angka Starlink.
