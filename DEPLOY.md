# Update Sales Monitor tanpa bikin Vercel dari awal

Kuncinya: **jangan bikin project Vercel baru tiap update.** Data (upload, pengaturan kontrak, SO-DO) disimpan di Vercel Blob yang menempel di project. Selama pakai project yang sama, data aman dan tinggal deploy ulang kodenya.

## Setup sekali saja
1. Bikin repo GitHub (private), upload **isi** folder zip ini (bukan folder pembungkusnya).
2. Vercel > Add New > Project > Import repo itu. Framework: Vite (build `npm run build`, output `dist`). Deploy.
3. Project > Storage > Create > **Blob**, lalu Connect ke project. Redeploy sekali supaya token terbaca.

## Tiap ada versi baru (pilih satu)
**A. Lewat web GitHub (paling gampang)**
Repo > Add file > Upload files > drag semua isi zip baru (menimpa file lama) > Commit. Vercel otomatis deploy sekitar 1 menit. Batas GitHub 100 file per upload; zip ini sekitar 60 file.

**B. Lewat git**
Unzip ke folder repo (timpa), lalu: `git add -A && git commit -m "update" && git push`

**C. Lewat Vercel CLI (tanpa GitHub)**
`npm i -g vercel` > `vercel link` (sekali) > tiap update: `vercel --prod` dari folder project.

## Kalau terlanjur bikin project baru
Datanya masih ada di Blob lama. Di project baru: Storage > **Connect existing store** > pilih store lama > Redeploy. Data muncul lagi.
