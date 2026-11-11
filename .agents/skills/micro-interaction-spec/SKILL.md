---
name: micro-interaction-spec
description: >
  Gunakan saat menyerahkan satu micro-interaction ke engineering: trigger, rules, feedback, loops, dan modes. Untuk motion saja pakai `animation-principles`; untuk komponen multi-state pakai `state-machine`.
metadata:
  author: niamkvn
  version: "1.0.0"
---

# Micro-Interaction Spec
Spesifikasikan micro-interaction secara lengkap dengan kerangka berikut.

## Kerangka
1. **Trigger**: pemicu: aksi pengguna (click, hover, swipe), event sistem (notifikasi, selesai), atau kondisional (waktu, ambang batas)
2. **Rules**: logika dan urutan setelah terpicu, termasuk kondisi dan percabangan
3. **Feedback**: respons yang dirasakan: visual (warna, ukuran, posisi), motion, audio, haptic
4. **Loops dan Modes**: apakah berulang atau berubah seiring waktu; perilaku pertama kali vs berulang; progressive disclosure

## Format Spesifikasi
Nama, trigger, rules (urutan), feedback (visual/audio/haptic), durasi/easing, perilaku loop, aksesibilitas.

## Praktik Terbaik
- Setiap micro-interaction punya tujuan jelas
- Durasi pendek (100-500ms untuk kebanyakan kasus)
- Feedback langsung untuk aksi pengguna
- Hormati preferensi reduced-motion
- Uji performa di perangkat target