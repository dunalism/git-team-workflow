# Git Team Workflow

Panduan ini menjelaskan alur kerja (workflow) yang umum digunakan dalam kolaborasi tim menggunakan Git di perusahaan. Ikuti langkah-langkah berikut untuk menjaga kolaborasi tetap terorganisir dan kode tetap berkualitas.

## 1. Forking Repository

Setiap anggota tim membuat salinan dari repository utama (_central repository_) ke akun GitHub mereka sendiri. Proses ini penting untuk memungkinkan setiap anggota bekerja secara independen tanpa memengaruhi repository utama. Dengan forking, perubahan dapat diuji dan disempurnakan terlebih dahulu sebelum diintegrasikan ke dalam kode utama.

```bash
git clone https://github.com/username/repository.git
```

Command ini digunakan untuk meng-_clone_ repository ke mesin lokal.

---

## 2. Membuat Branch Baru

Setiap fitur atau perbaikan bug dikerjakan di branch terpisah untuk menjaga agar `main` branch tetap stabil.

```bash
git checkout -b nama-branch
```

Command ini membuat branch baru dan langsung berpindah ke branch tersebut.

### Contoh Skenario

Misalkan Anda sedang mengerjakan fitur "halaman login" sementara rekan Anda mengerjakan "halaman registrasi". Jika semua perubahan dilakukan langsung di `main` branch, maka konflik dapat terjadi karena Anda dan rekan Anda mungkin mengedit file yang sama. Dengan menggunakan branch terpisah seperti `feature/login-page` dan `feature/registration-page`, masing-masing pekerjaan dapat dilakukan secara independen tanpa risiko konflik langsung pada branch utama.

---

## 3. Melakukan Perubahan dan Commit

Setelah melakukan perubahan pada kode, perubahan tersebut di-_commit_ ke branch lokal.

```bash
git add .
git commit -m "Deskripsi perubahan"
```

- `git add .` menambahkan semua perubahan ke _staging area_.
- `git commit -m "Deskripsi perubahan"` membuat _commit_ dengan pesan deskripsi.

---

## 4. Push ke Remote Repository

Setelah _commit_, branch lokal di-_push_ ke repository remote.

```bash
git push origin nama-branch
```

Command ini mengirim branch lokal ke repository remote di GitHub.

---

## 5. Membuat Pull Request (PR)

Di GitHub, anggota tim membuat _Pull Request_ untuk menggabungkan perubahan dari branch mereka ke `main` branch. Sebelum mengirim PR, pastikan untuk:

1. Memastikan kode telah diuji dengan benar dan tidak mengandung bug yang jelas.
2. Memastikan kode Anda sesuai dengan standar coding yang ditentukan oleh tim.
3. Menambahkan deskripsi yang jelas tentang apa yang telah diubah atau ditambahkan dalam PR Anda.
4. Menyertakan tangkapan layar atau dokumentasi tambahan jika diperlukan untuk memperjelas konteks perubahan.

PR ini kemudian direview oleh anggota tim lain.

---

## 6. Code Review dan Merge

Anggota tim lain melakukan _review_ terhadap PR. Jika disetujui, PR tersebut di-_merge_ ke `main` branch.

```bash
git checkout main
git pull origin main
git merge nama-branch
```

- `git checkout main` berpindah ke `main` branch.
- `git pull origin main` memperbarui `main` branch lokal dengan perubahan terbaru dari remote.
- `git merge nama-branch` menggabungkan branch yang diinginkan ke `main` di mesin lokal.

> **Catatan Penting:** Perintah `git merge nama-branch` hanya menggabungkan branch di mesin lokal Anda. Agar perubahan ini terlihat di remote repository (GitHub), Anda perlu melakukan push:
>
> ```bash
> git push origin main
> ```
>
> Namun, jika Anda melakukan merge langsung melalui GitHub menggunakan PR, langkah ini tidak diperlukan karena penggabungan sudah terjadi di remote repository.

---

## 7. Menghapus Branch yang Sudah Di-merge

Setelah branch di-_merge_, branch tersebut bisa dihapus untuk menjaga kebersihan repository dan mengurangi kebingungan dalam pengelolaan branch. Menghapus branch yang tidak lagi dibutuhkan membantu tim fokus hanya pada branch yang relevan.

### Menghapus Branch Lokal

```bash
git branch -d nama-branch
```

### Menghapus Branch Remote

```bash
git push origin --delete nama-branch
```

---

## 8. Menarik Perubahan Terbaru

Anggota tim secara berkala menarik perubahan terbaru dari `main` branch untuk memastikan mereka bekerja dengan kode terbaru.

```bash
git pull origin main
```

Command ini memperbarui branch lokal dengan perubahan terbaru dari `main` branch di remote repository.

> **Catatan:** Selalu lakukan _pull_ sebelum memulai pekerjaan baru untuk menghindari konflik dengan perubahan terbaru yang mungkin telah dilakukan oleh anggota tim lain.

---

## Tips Tambahan

- **Selalu lakukan _pull_ sebelum membuat perubahan baru:** Pastikan branch Anda selalu sinkron dengan _main_ branch sebelum memulai pekerjaan.
- **Beri nama branch dengan deskripsi yang jelas:** Contoh: `feature/login-page` atau `bugfix/fix-authentication`.
- **Tulis pesan commit yang deskriptif:** Hindari pesan seperti "update" atau "fix" tanpa konteks.

Dengan mengikuti workflow ini, tim dapat bekerja secara kolaboratif dan terorganisir, mengurangi risiko konflik kode dan memastikan kualitas kode tetap terjaga.
