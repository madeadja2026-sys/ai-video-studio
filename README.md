# VIDEO AI STUDIO V1.0

Aplikasi frontend statis untuk mengirim gambar ke model image-to-video fal.ai. Frontend di-host melalui GitHub Pages; API key disimpan hanya di Cloudflare Worker.

## 1. Publikasikan GitHub Pages
1. Buka Settings > Pages pada repository.
2. Pada Build and deployment, pilih Deploy from a branch.
3. Pilih branch main dan folder /(root), lalu Save.
4. Tunggu alamat Pages muncul. Biasanya: https://madeadja2026-sys.github.io/ai-video-studio/

## 2. Siapkan API fal.ai
1. Buat akun di https://fal.ai/ dan buat API Key.
2. Penggunaan model API dapat dikenakan biaya/kredit sesuai tarif fal.ai.
3. Jangan pernah menaruh API Key di index.html, repository publik, atau membagikannya di chat.

## 3. Pasang backend Cloudflare Worker
1. Masuk https://dash.cloudflare.com/ lalu Workers & Pages > Create > Worker.
2. Buat Worker baru, buka Edit code, ganti seluruh kode dengan isi file worker.js dari repository ini, lalu Deploy.
3. Buka Settings > Variables and Secrets pada Worker.
4. Tambahkan secret bernama FAL_KEY dengan nilai API key fal.ai. Simpan.
5. Salin URL Worker, misalnya https://nama-worker.username.workers.dev.

## 4. Hubungkan GitHub Pages ke Worker
1. Buka index.html pada repository dan tekan Edit.
2. Cari dua kemunculan teks YOUR-CLOUDFLARE-WORKER.workers.dev.
3. Ganti hanya nama host tersebut dengan URL Worker Anda (tanpa garis miring di akhir), sehingga endpoint menjadi https://nama-worker.username.workers.dev/generate dan /status.
4. Commit perubahan. Tunggu GitHub Pages memperbarui situs.

## 5. Uji
1. Buka situs GitHub Pages.
2. Unggah gambar JPG/PNG/WebP, tuliskan gerakan, pilih model, lalu tekan BUAT VIDEO AI.
3. Tunggu status sampai COMPLETED; hasil dapat diputar dan dibuka untuk disimpan sebagai MP4.

## Catatan penting
- V1.0 mendukung alur satu gambar menjadi satu klip; belum menggabungkan beberapa klip atau musik.
- Vidu dan Ovi adalah endpoint model di fal.ai; parameter/durasi mengikuti skema dan ketersediaan endpoint masing-masing.
- Model dapat mengubah detail wajah, tangan, atau pakaian. Hasil bukan jaminan identitas sempurna.
- Untuk menjaga keamanan dan biaya, jangan membagikan URL Worker tanpa pembatasan kepada publik. Tahap berikutnya perlu autentikasi, rate limit, dan batas ukuran unggahan.
- API key tidak disimpan di GitHub Pages. Semua panggilan fal.ai dilakukan dari Worker.
