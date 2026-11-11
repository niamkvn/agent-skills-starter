---
name: anti-slop-design
description: Gunakan saat membangun UI frontend (komponen, landing page, dashboard) yang khas dan siap production. Hindari tampilan generik buatan AI seperti gradien ungu, rounded seragam, font Inter.
metadata:
  author: niamkvn
  version: "1.0.0"
---

# Anti Slop Design
Cegah desain frontend yang terkesan "buatan AI".

## Ciri AI Slop (dilarang)
- Font default: Inter/Roboto/Arial/sistem
- Gradien ungu di latar putih
- Rounded corners seragam
- Layout rata tengah saja
- Hero section + 3 kolom fitur yang klise
- Bayangan identik di semua kartu
- Ilustrasi tanpa karakter

## Proses
1. **Konteks**
   - Tujuan: masalah apa yang diselesaikan?
   - Pengguna: developer atau umum?
   - Tone (pilih satu, tegas): brutalism, minimal, retrofuturism, organik, mewah, playful, editorial, art deco, industrial, pastel lembut, neon 80-an, minimalis Jepang
   - Pembeda: apa satu elemen yang akan diingat pengguna?
2. **Prinsip**
   - Tipografi: font unik (Google Fonts), pasangkan display + body
   - Warna: variabel CSS; satu warna dominan + aksen tegas; palet tidak umum
   - Motion: utamakan CSS-only; staggered reveal saat load; interaksi hover/scroll tak terduga
   - Ruang: asimetris, tumpang tindih, alur diagonal, elemen keluar grid; whitespace lega atau padat secara disengaja
   - Latar: jangan solid default; gunakan gradient mesh, noise, pola geometris, layer, bayangan, transparansi

## Checklist
- [ ] Ada elemen asimetris
- [ ] Tidak terkesan buatan AI