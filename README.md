# Cookie Counter w/ Security Attribute

## EXPERIMENT 1: Session Cookie vs Persistent Cookie
sessionTest: **[hilang]** Session Cookie (tanpa Max-Age) \
persistentTest: **[ada]** Persistent Cookie: Max-Age = 3600 (1 jam)

## EXPERIMENT 2: Path Restriction
| Halaman | cookieRoot | cookieAdmin |
| ------- | ---------- | ----------- |
| /index.html | ✓ |	✗ | 
| /admin/index.html | ✓ | ✓ |
| /admin/dashboard/index.html | ✓ | ✓ |

Cookie dengan Path=/admin akan dikirim ke:
- /admin ✓
- /admin/dashboard ✓
- /profile ✗ 
- / ✗

## EXPERIMENT 3: Secure Flag
| URL | Secure Cookie |
| --- | ------------- |
| http://localhost / http://127.0.0.1 | ✅ Bisa (exception) |
| http://example.com (production) | ❌ Ditolak |
| https://example.com | ✅ Bisa |

Cookie Secure tersimpan di localhost HTTP? **Ya** \
Mengapa bisa tersimpan? **Browser exception, karena localhost hanya digunakan untuk development.**

## PERTANYAAN REFLEKSI
1. **Mengapa session cookie (tanpa Max-Age) berguna untuk login?** \
Agar informasi login otomatis hilang saat browser ditutup, kecuali dengan opsi "Remember Me"
2. **Jika kamu membuat aplikasi e-commerce, atribut apa yang akan kamu gunakan untuk cookie session ID? Jelaskan alasannya.** \
HTTPOnly, Secure, Domain sesuai subdomain, Path=/. Memastikan secure via HTTP, mencegah XSS, membatasi pengiriman cookie.
3. **Apa risiko keamanan jika cookie session TIDAK menggunakan HttpOnly?** \
JavaScript dapat dieksekusi, membaca/mencuri cookie, dan user bisa kena hack.
4. **Kapan sebaiknya menggunakan Expires vs Max-Age?** \
Max-Age untuk menentukan durasi (detik, menit, jam); Expires untuk menentukan tanggal.
5. **Apa yang terjadi jika Domain cookie di-set ke `.example.com`?** \
Cookie akan dikirim ke domain utama dan semua subdomain. (www.example.com / shop.example.com)