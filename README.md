# ccbench gladi — 2026-11-05

Hasil **gladi (dress rehearsal)** koneksi TCP congestion control, diambil dari
`pep-star01:~/` ke laptop pada 2026-11-06.

> ⚠️ **BUKAN hasil penelitian final.** Semua isi folder ini adalah
> **pengukuran paket nyata** (bukan emulasi/simulasi), tetapi **jalurnya bukan
> Starlink** — paket berjalan melalui gateway kampus USK + jalur terestrial
> Telkom, tidak pernah naik ke satelit. Jangan kutip angka dari sini sebagai
> angka Starlink.

## Isi

| Folder | Apa | Status |
|---|---|---|
| `ccbench-matrix-20261105T004038Z` | 4 × 1 jam uplink (indigo, taova, vivace) + 5 slot referensi cubic | jalur kampus; `pcc` gagal di 65% durasi |
| `ccbench-matrix-20261105T054527Z` | ulangan `pcc` 1 jam penuh setelah patch 0007 | jalur kampus |
| `ccbench-dlsmoke-20261105T081524Z` | smoke downlink 120 s → bukti `taova` loss 65%, `vivace` 35% | dasar patch 0008 |
| `ccbench-mtutest-20261105T083351Z` | run menggantung 6 j 45 m karena `--local-if` + rp_filter | dasar patch 0008 (b) |

Setiap folder memuat data mentah (`.tsv`, `.log.gz`, `.json`, PDF/PNG/SVG),
`schedule.csv`, `run.log`, serta `provenance/` (binary sha256, image tag, dan
patch 0001–0008).

## Masih berguna untuk apa

1. **Bab metode**: bukti harness bekerja ujung ke ujung selama 4 jam, dan slot
   referensi `cubic` mendeteksi kestabilan jalur.
2. **Pembanding terestrial** terhadap matriks Starlink nanti (jalur disebut
   eksplisit).
3. **Dua temuan patch** (0007 dan 0008) yang reproduksinya ada di sini.

Detail lengkap: lihat [`BACA-INI.md`](BACA-INI.md).
