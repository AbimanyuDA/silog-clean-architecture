# SILOG - Integrated Logistics SaaS Platform

Proyek ini adalah platform Software as a Service (SaaS) untuk Sistem Manajemen Logistik dan Rantai Pasok yang terintegrasi. [cite_start]Platform ini dikembangkan secara kolaboratif oleh 4 tim Capstone (CAPS17 - CAPS20) untuk menciptakan ekosistem logistik yang efisien, transparan, dan cerdas.

## Arsitektur Proyek
Sesuai arahan teknis, proyek ini menggunakan pendekatan:
* **Backend:** Modular Monolith dengan Clean Architecture (Domain-Centric).
* **Frontend Web:** Next.js (Feature-Based Architecture).
* **Frontend Mobile:** Flutter (Feature-Based Architecture).

---

## Struktur Repositori & Folder

Tujuan: Memisahkan logika bisnis antar tim agar independen namun tetap dalam satu ekosistem.

```text
/backend
├── cmd/
│   └── api/                # Entry point aplikasi (main.go)
├── internal/
│   ├── modules/            # PEMBAGIAN PER TIM (MODULAR)
│   │   ├── driver/         # CAPS17: Driver Management
│   │   │   ├── delivery/   # Layer Presentation (HTTP Handlers/REST)
│   │   │   ├── usecase/    # Layer Application (Logic Bisnis)
│   │   │   ├── domain/     # Layer Domain (Entities & Interfaces)
│   │   │   └── repository/ # Layer Infrastructure (Database/External)
│   │   ├── warehouse/      # CAPS18: Warehouse Management
│   │   ├── customer/       # CAPS19: Customer Portal
│   │   └── transportation/ # CAPS20: Carrier Management 
│   ├── shared/             # Kode yang dipakai bersama (Loosely Coupled)
│   │   ├── middleware/     # Auth JWT, Logging
│   │   ├── database/       # Global DB Connection
│   │   └── domain/         # Interface bersama untuk komunikasi antar-modul
│   └── infrastructure/     # Driver pihak ketiga (GPS, Mailer, Storage)
├── api/                    # Kontrak API (Swagger/OpenAPI)
└── go.mod


/frontend-web
├── src/
│   ├── app/                # Next.js App Router (Layout per Role)
│   │   ├── admin/          # Dashboard Admin SILOG
│   │   ├── warehouse/      # Panel Manajemen Gudang
│   │   └── customer/       # Portal Pemilik Barang
│   ├── components/
│   │   ├── ui/             # Komponen umum (Shadcn, dsb)
│   │   └── features/       # Komponen spesifik fitur
│   │       ├── tracking/   # Fitur pelacakan armada (CAPS20)
│   │       └── inventory/  # Fitur stok barang (CAPS18)
│   ├── hooks/              # Logika API (UseQuery/SWR) per modul
│   ├── services/           # Axios/Fetch call ke backend per modul
│   └── lib/                # Konfigurasi global (Axios instance, utils)
├── public/                 # Aset gambar & icon
└── package.json


/frontend-mobile            # Flutter App
├── lib/                    # Direktori utama kode Dart
│   ├── main.dart           # File utama aplikasi (Entry point)
│   ├── app/                # Halaman/Routing per Role
│   │   ├── admin/          # Dashboard Admin SILOG
│   │   ├── warehouse/      # Panel Manajemen Gudang
│   │   └── customer/       # Portal Pemilik Barang
│   ├── components/         # Widget Reusable
│   │   ├── ui/             # Komponen umum (Tombol, Input, dsb)
│   │   └── features/       # Komponen spesifik fitur
│   │       ├── tracking/   # Fitur pelacakan armada (CAPS20)
│   │       └── inventory/  # Fitur stok barang (CAPS18)
│   ├── controllers/        # State Management (Bloc/Provider/GetX)
│   ├── services/           # API Call (Dio/http) ke backend
│   └── core/               # Konfigurasi & Utilitas global
│       ├── utils/          # Fungsi format/helper murni
│       ├── network/        # Konfigurasi Dio & Interceptor
│       └── theme/          # Konfigurasi Tema & Warna
├── assets/                 # Folder aset gambar, icon, font
└── pubspec.yaml            # Manajemen dependency Flutter
```