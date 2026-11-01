# Agent Skills

Kumpulan skill reusable untuk Codex dan agent yang kompatibel. Setiap skill berada di foldernya masing-masing dan memiliki file utama `SKILL.md`.

**English:** [README.md](README.md)

## Skill tersedia

| Skill | Fungsi |
| --- | --- |
| [`atomic-commits`](skills/atomic-commits/SKILL.md) | Membagi perubahan kode menjadi commit Git yang fokus, mudah ditinjau, ditelusuri, dan dibatalkan. |

## Instalasi di Codex

Jalankan instruksi berikut melalui Codex:

```text
$skill-installer install https://github.com/yawpie/agent-skills/tree/main/skills/atomic-commits
```

Jika skill belum terbaca, restart Codex.

Alternatifnya, clone repository lalu salin folder `skills/atomic-commits` ke `~/.codex/skills/` (Windows: `%USERPROFILE%\.codex\skills\`).

## Cara menggunakan

Panggil `$atomic-commits` secara eksplisit atau sampaikan permintaan terkait pembagian commit. Skill tidak akan membuat commit tanpa izin pengguna.

```text
$atomic-commits Pisahkan perubahan saya menjadi commit-commit logis, jalankan pemeriksaan, dan jangan sertakan perubahan di luar tugas ini.
```

## Kontribusi dan lisensi

Panduan kontribusi ada di [CONTRIBUTING.md](CONTRIBUTING.md). Kode dan dokumentasi disediakan dengan lisensi [MIT](LICENSE).
