---
name: ponytail-review
description: Review kualitas seluruh repo: bug, celah keamanan, titik rusak di bawah beban nyata, kode berisiko tanpa test, jalur lambat, dan apa yang perlu dihapus, digabung, atau dipecah. Laporan satu kali, berurutan, tanpa mengubah kode. Gunakan untuk "review codebase", "review repo", "cari bloat", "apa yang bisa dihapus", /ponytail-review.
metadata:
  author: niamkvn
  version: "1.0.0"
---

Review repo seperti senior developer yang baru mewarisinya dan akan dipanggil saat rusak. Prioritas: benar, aman, tahan beban, teruji, cepat, ramping. Setiap baris tambahan harus dibaca, diuji, dan diperbaiki kelak. Ini laporan yang diminta pengguna, jadi tulis lengkap.

## 1. Petakan dulu
- Review yang disebut pengguna (folder, package, atau repo). Tidak disebut: seluruh repo.
- Baca README, config build/deploy, daftar dependency, entry point (main, routes, handlers, jobs, CLI), dan test.
- Tentukan beban yang diharapkan (satu orang menjalankan script, atau banyak pengguna/proses sekaligus). Nilai skala terhadapnya dan sebutkan asumsinya.
- Telusuri alur utama ujung ke ujung: data masuk, tersimpan, keluar. Baca penuh jalur input pengguna, uang, auth, penulisan data, background job, dan state yang dibagi antarproses.
- Repo besar: dalami bagian yang paling mahal bila salah, bukan file per file. Sebutkan bagian yang tidak dibaca.

## 2. Cari
1. **Bug:** hasil salah, crash, edge case terlewat (kosong, nol, item terakhir, pembulatan, zona waktu), pemanggil tidak sesuai dengan return fungsi, aturan sama diterapkan berbeda di dua tempat.
2. **Risiko:** celah keamanan (injection, random lemah, secret di kode, input pengguna tanpa validasi), kehilangan data (error ditelan, urutan tulis salah, tanpa transaction).
3. **Skala:** aman untuk satu pengguna, salah untuk banyak: race check-then-write, kerja sama diulang tiap proses, memori/list yang terus tumbuh, query per item, O(n^2) pada input besar, state per proses yang seharusnya dibagi.
4. **Test hilang:** logika berisiko (percabangan, parser, uang, keamanan, penulisan data) tanpa test yang gagal saat logikanya rusak. Satu test bagus, bukan coverage.
5. **Kecepatan:** perlambatan besar = masalah. Optimasi kecil (kerja berulang di hot loop) = saran.
6. **Ramping:** kode yang tidak perlu ada atau perlu lebih kecil.
   - hapus: dead code, opsi/flag/config tak terpakai, fitur spekulatif
   - reuse: dua helper melakukan hal sama (pertahankan satu, sebut path-nya)
   - stdlib/native: sudah disediakan standard library atau platform; dependency yang kerjanya cukup beberapa baris
   - yagni: interface dengan satu implementasi, factory dengan satu produk, wrapper yang hanya meneruskan panggilan
   - gabung: salinan mirip yang harus berubah bersama
   - pecah: satu fungsi/class dengan beberapa tugas tak terkait. Pecah menurut tugas, bukan jumlah baris, dan jangan jadi helper yang hanya memperpendek fungsi.

## 3. Periksa sebelum melapor
- Tiap temuan butuh kasus konkret: "input/situasi ini menghasilkan hasil salah ini". Tanpa kasus, bukan temuan.
- Sebelum menyebut kode tak terpakai, grep seluruh tree, termasuk test, fixture, config, dan referensi string/dinamis.
- Jalan pintas bertanda komentar `shortcut:` (atau `ponytail:` lama) yang menyebut batasnya adalah keputusan, bukan temuan, kecuali beban yang diharapkan sudah melewatinya.
- Usulkan perbaikan terkecil yang berhasil. Utamakan yang menghapus kode. Jangan menambah layer, framework, atau config yang tidak dibutuhkan.
- Tanpa selera gaya, tanpa "pertimbangkan", tanpa kekhawatiran samar.

## 4. Output
Bahasa Indonesia sederhana: kalimat pendek, kata sehari-hari. Jelaskan istilah teknis saat pertama dipakai. Pembaca mungkin belum pernah melihat kode ini.

Mulai dengan `Fungsi repo ini:` (2-3 kalimat) dan beban yang diasumsikan.

Lalu temuan dalam tiga grup, terpenting dulu, lewati grup kosong:
- **Wajib diperbaiki:** bug, keamanan, kehilangan data, rusak pada beban yang diharapkan.
- **Sebaiknya diperbaiki:** kode berisiko tanpa test, lambat nyata, duplikasi, fungsi campur tugas, kode yang tidak perlu ada.
- **Bagus bila ada:** optimasi kecil, bentuk lebih pendek.

Beri nomor berurutan lintas grup agar pengguna bisa bilang "perbaiki 2 dan 5". Maksimal 20 temuan; sebutkan jumlah yang dilewati. Tiap temuan punya empat bagian, masing-masing 1-2 kalimat pendek:

2. **Order tercatat di hari yang salah** (`billing/close_day.py:L40-52`)
   - **Ini apa:** Job tengah malam menutup hari dan menagih semua order hari itu.
   - **Masalah:** "Hari ini" diambil dari jam server (UTC). Order pukul 00:30 di Berlin tertagih di hari sebelumnya.
   - **Perbaikan:** Hitung hari sekali dalam zona waktu toko: `datetime.now(ZoneInfo("Europe/Berlin")).date()`.
   - **Jika dilewati:** Order larut malam bertanggal salah, akuntansi memperbaikinya manual.

Akhiri dengan:
- `Verdict:` satu baris: sehat, atau apa yang diperbaiki dulu.
- `Lean: -<N> baris, -<M> dependency mungkin.` bila ada temuan ramping.
- `Tidak diperiksa:` bagian yang tidak dibaca atau tidak bisa dijalankan.

Tidak ada temuan: `Fungsi repo ini:`, lalu `Sehat. Tidak ada yang perlu diperbaiki.` dan satu baris tentang yang diperiksa.

Laporan satu kali, tidak mengubah kode.