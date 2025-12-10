# Sistem Informasi Manajemen Bank Sampah (E-Waste) 🌱
**Tugas Besar Algoritma & Pemrograman  
Milestone 1: Progress 50%**

---

## 👤 Identitas Pengembang
**Nama:** Airlangga Putra Sumadi  
**NIM:** 2501624  
**Kelas:** Pendidikan Ilmu Komputer A  

---

## 📝 Deskripsi Proyek
Program ini adalah aplikasi berbasis **Console (CLI)** yang dibuat menggunakan **bahasa C**.  
Aplikasi ini mensimulasikan sistem teller bank sampah, di mana nasabah dapat menukar sampah (E-Waste) menjadi saldo tabungan.

Pada tahap ini (**Versi 0.5**), pengembangan berfokus pada:
- Struktur Data (Struct & Array)  
- Logika dasar Input-Output (CRUD)

---

## ✅ Status Fitur (Progress 50%)

| No | Fitur | Status | Keterangan |
|----|--------|---------|------------|
| 1 | Registrasi Nasabah | ✅ Ready | Input ID, Nama, Alamat ke Array |
| 2 | Lihat Data | ✅ Ready | Menampilkan tabel data nasabah |
| 3 | Setor Sampah | ⚠️ Basic | Input transaksi manual by Index |
| 4 | Tarik Tunai | 🚧 On Progress | Menunggu logic validasi saldo |
| 5 | Cari Nasabah | 🚧 On Progress | Menunggu algoritma Sequential Search |
| 6 | Ranking Saldo | 🚧 On Progress | Menunggu algoritma Bubble Sort |
| 7 | Statistik (Max/Min) | 🚧 On Progress | Menunggu algoritma MaxMin |

---

## 💻 Kode Program (Source Code)

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// --- KONFIGURASI ---
#define MAX_NASABAH 100
#define MAX_STRING 50

// --- STRUKTUR DATA ---
typedef struct {
    char id[10];
    char nama[MAX_STRING];
    char alamat[MAX_STRING];
    long saldo;
} Nasabah;

// --- VARIABEL GLOBAL ---
Nasabah daftarNasabah[MAX_NASABAH];
int jumlahNasabah = 0;

// --- PROTOTYPE ---
void registrasiNasabah();
void lihatSemuaData();
void setorSampah();
long hitungHarga(int jenis, float berat);
void fiturBelumTersedia();
void clearScreen();
void pauseScreen();
void bersihkanNewline(char* str);

// ==========================================
// PROGRAM UTAMA (MAIN)
// ==========================================
int main() {
    setbuf(stdout, NULL);

    int pilihan;
    char bufferInput[10];

    do {
        clearScreen();
        printf("=== PROGRESS TUGAS BESAR BANK SAMPAH (50%%) ===\n");
        printf("1. Registrasi Nasabah (Ready)\n");
        printf("2. Lihat Data Nasabah (Ready)\n");
        printf("3. Setor Sampah (Basic)\n");
        printf("4. Tarik Tunai (On Progress)\n");
        printf("5. Cari Nasabah (On Progress)\n");
        printf("6. Ranking Saldo (On Progress)\n");
        printf("7. Statistik Max/Min (On Progress)\n");
        printf("8. Hapus Data (On Progress)\n");
        printf("0. Keluar\n");
        printf("==============================================\n");
        printf("Menu Pilihan: ");

        fgets(bufferInput, sizeof(bufferInput), stdin);
        pilihan = atoi(bufferInput);

        switch (pilihan) {
            case 1: registrasiNasabah(); break;
            case 2: lihatSemuaData(); break;
            case 3: setorSampah(); break;
            case 4:
            case 5:
            case 6:
            case 7:
            case 8:
                fiturBelumTersedia();
                break;
            case 0: printf("\nKeluar program...\n"); break;
            default: printf("\nMenu salah.\n"); pauseScreen();
        }

    } while (pilihan != 0);

    return 0;
}

// --- FUNGSI UTAMA ---

void registrasiNasabah() {
    clearScreen();
    printf("--- REGISTRASI NASABAH ---\n");

    if (jumlahNasabah >= MAX_NASABAH) {
        printf("Array Penuh.\n"); pauseScreen(); return;
    }

    Nasabah baru;

    printf("Masukkan ID: ");
    fgets(baru.id, sizeof(baru.id), stdin);
    bersihkanNewline(baru.id);

    printf("Nama Lengkap: ");
    fgets(baru.nama, sizeof(baru.nama), stdin);
    bersihkanNewline(baru.nama);

    printf("Alamat: ");
    fgets(baru.alamat, sizeof(baru.alamat), stdin);
    bersihkanNewline(baru.alamat);

    baru.saldo = 0;

    daftarNasabah[jumlahNasabah] = baru;
    jumlahNasabah++;

    printf("\n[OK] Data berhasil disimpan ke Array index ke-%d.\n", jumlahNasabah-1);
    pauseScreen();
}

void lihatSemuaData() {
    clearScreen();
    printf("--- DATA NASABAH (BASIC VIEW) ---\n");

    if (jumlahNasabah == 0) {
        printf("Data masih kosong.\n");
    } else {
        printf("%-10s | %-20s | %-15s\n", "ID", "Nama", "Saldo");
        printf("------------------------------------------------\n");
        for (int i = 0; i < jumlahNasabah; i++) {
            printf("%-10s | %-20s | Rp. %ld\n",
                daftarNasabah[i].id,
                daftarNasabah[i].nama,
                daftarNasabah[i].saldo);
        }
    }
    pauseScreen();
}

void setorSampah() {
    clearScreen();
    printf("--- INPUT TRANSAKSI (BASIC) ---\n");

    if (jumlahNasabah == 0) { printf("Belum ada data.\n"); pauseScreen(); return; }

    lihatSemuaData();
    printf("\n(Pilih manual menggunakan nomor urut)\n");

    int index;
    char buff[10];

    printf("Pilih nomor urut nasabah (1 - %d): ", jumlahNasabah);
    fgets(buff, 10, stdin);
    index = atoi(buff) - 1;

    if (index >= 0 && index < jumlahNasabah) {
        printf("\nInput sampah untuk: %s\n", daftarNasabah[index].nama);
        printf("Jenis: 1.Plastik 2.Kertas 3.Logam\n");

        int jenis; float berat;
        printf("Pilih (1-3): "); fgets(buff, 10, stdin); jenis = atoi(buff);
        printf("Berat (kg): "); fgets(buff, 10, stdin); berat = atof(buff);

        long total = hitungHarga(jenis, berat);
        daftarNasabah[index].saldo += total;

        printf("Saldo bertambah: Rp. %ld\n", total);
    } else {
        printf("Index salah.\n");
    }
    pauseScreen();
}

long hitungHarga(int jenis, float berat) {
    if (jenis == 1) return (long)(berat * 3000);
    if (jenis == 2) return (long)(berat * 2000);
    if (jenis == 3) return (long)(berat * 7000);
    return 0;
}

void fiturBelumTersedia() {
    printf("\n[UNDER CONSTRUCTION]\n");
    printf("Maaf, fitur ini sedang dalam tahap pengerjaan.\n");
    pauseScreen();
}

void clearScreen() {
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}

void pauseScreen() {
    printf("\nEnter untuk lanjut...");
    getchar();
}

void bersihkanNewline(char* str) {
    str[strcspn(str, "\n")] = 0;
}
