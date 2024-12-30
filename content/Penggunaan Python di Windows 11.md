---
title: Penggunaan Python di Windows 11
created: 2024-12-30T21:26
updated: 2024-12-31T05:50
tags: [python, environment-setup]
publish: "true"
---

## Penggunaan Python di Windows

Python di Windows dapat digunakan untuk dua tujuan utama: sebagai dependency untuk software lain seperti Node.js dan Google Cloud SDK, atau untuk mengembangkan kode dalam proyek.

- **Untuk Dependency:** Gunakan versi terbaru Python yang dibutuhkan software seperti Google Cloud SDK dan Node.js. Install Python melalui Microsoft Store. Hingga saat ini (30 Desember 2024), Google Cloud SDK dan Node.js mendukung Python 3.13.1, dan pastikan Python ini menjadi default di level OS dan muncul pada PATH.

- **Untuk Proyek:** Terdapat tiga pilihan untuk manajemen proyek Python: Miniconda, Miniforge, dan UV. Pilihannya tergantung pada kebutuhan proyek, library, dan dependencies. Kenali bagaimana cara aktivasi environment didalam vs code atau tool yang relevan

## [Environment and Package Manager in Python](Environment%20and%20Package%20Manager%20in%20Python.md)

- **Miniconda:** Menggunakan hanya conda package manager dan repository dari conda-forge serta conda-default. Miniconda cenderung terlambat dalam update package dan rentan terhadap konflik versi package.

- **Miniforge:** Menyediakan opsi mamba dan conda sebagai package manager, mamba lebih cepat. miniforge juga lebih sederhana karena hanya menggunakan conda-forge sebagai repository, package lebih baru karena dikelola oleh komunitas.

- **UV:** Bisa diinstal secara global atau per proyek dengan membuat `.venv` (virtual environment) dan menggunakan pip. UV lebih cocok untuk proyek data engineering yang melibatkan platform pihak ketiga dan pip-compatible packages, seperti Prefect dan MkDocs.

## Kapan Menggunakan Miniconda, Miniforge, atau UV?

Jangan mencampur conda dan pip dalam satu environment. Ini bisa menyebabkan konflik dependencies karena versi yang tidak cocok antara berbagai repository. Misalnya, package seperti numpy bisa memiliki versi yang berbeda antara conda dan conda-forge, yang dapat menyebabkan masalah saat menjalankan proyek.

Menggunakan pip di dalam conda environment tidak direkomendasikan karena keduanya memiliki resolusi konflik package manager yang berbeda.

Saat export environment, conda menggunakan environment.yml dan pip tidak dihasilkan dalam export, sehingga perlu file terpisah requirements.txt. Hal ini membuat troubleshooting menjadi lebih sulit. dan berbagi environment tidak mudah.

- **Miniconda vs Miniforge:** Miniconda cenderung memiliki keterlambatan dalam update package, Miniforge lebih cepat dengan repository conda-forge.
- **UV:** Gunakan UV untuk proyek data yang melibatkan pip packages, misalnya Prefect atau MkDocs.

## Kasus Penggunaan Python dalam Proyek Data

Untuk proyek yang sederhana, seperti pembuatan KMZ dari foto dengan koordinat, menggunakan **SimpleKML** lebih disarankan karena penulisan kode lebih mudah dan tujuan spesifik. Dalam proyek data engineering, seperti pengumpulan data, transformasi data, dan visualisasi data, UV lebih efisien karena dependency yang lebih sederhana, baru, dan kompatibel dengan Cloud modern