---
name: anti-slop-design
description: >
   Gunakan saat membangun UI frontend (komponen, landing page, dashboard) yang khas dan siap production. Hindari tampilan generik buatan AI: gradien ungu, rounded seragam, font Inter.
metadata:
  author: niamkvn
  version: "1.1.0"
---

# Anti Slop Design
Cegah desain frontend yang terkesan "buatan AI".

## Ciri AI Slop (dilarang)
- Font default: Inter/Roboto/Arial/sistem, juga Space Grotesk
- Gradien ungu di latar putih
- Rounded corners seragam
- Layout rata tengah saja
- Hero section + 3 kolom fitur yang klise
- Bayangan identik di semua kartu
- Ilustrasi tanpa karakter

## Alur
1. **Konsep**
   - Tujuan dan pengguna: masalah apa yang diselesaikan, untuk siapa?
   - Tone (pilih satu, tegas): brutalism, minimal, maksimalis, retrofuturism, organik, mewah, playful, editorial, art deco, industrial, pastel lembut, neon 80-an, minimalis Jepang
   - Pembeda: satu elemen yang akan diingat pengguna
   - Batasan teknis: framework, performa, aksesibilitas
2. **Bangun** (kode siap production: HTML/CSS/JS, Svelte, Vue, React, dll.)
   - Tipografi: font berkarakter (Google Fonts), pasangkan display + body
   - Warna: variabel CSS; satu warna dominan + aksen tegas; palet tidak umum
   - Motion: staggered reveal saat load; hover/scroll tak terduga; CSS untuk HTML, Motion library untuk Svelte
   - Ruang: asimetris, tumpang tindih, alur diagonal, elemen keluar grid; whitespace lega atau padat secara disengaja
   - Latar: jangan solid default; gradient mesh, noise, pola geometris, transparansi berlapis, bayangan dramatis, border dekoratif
   - Kompleksitas kode sesuai visi: maksimalis butuh kode rumit, minimalis butuh presisi spasi dan tipografi
3. **Verifikasi**: hierarki visual, interaksi, animasi, aksesibilitas; ada elemen asimetris; tidak ada ciri AI Slop