Sistem Informasi Manajemen Bank Sampah (E-Waste) 🌱Tugas Besar Algoritma & Pemrograman > Milestone 1: Progress 50%👤 Identitas PengembangNama: Airlangga Putra SumadiNIM: 2501624Kelas: Pendidikan Ilmu Komputer A📝 Deskripsi ProyekProgram ini adalah aplikasi berbasis Console (CLI) yang dibuat menggunakan bahasa C. Aplikasi ini berfungsi untuk mensimulasikan sistem teller bank sampah, di mana nasabah dapat menukar sampah (E-Waste) menjadi saldo tabungan.Pada tahap ini (Versi 0.5), pengembangan berfokus pada pematangan Struktur Data (Struct & Array) serta logika dasar Input-Output (CRUD) sebelum melangkah ke algoritma yang lebih kompleks.✅ Status Fitur (Progress 50%)NoFiturStatusKeterangan1Registrasi Nasabah✅ ReadyInput ID, Nama, Alamat ke Array2Lihat Data✅ ReadyMenampilkan tabel data nasabah3Setor Sampah⚠️ BasicInput transaksi manual by Index4Tarik Tunai🚧 On ProgressMenunggu logic validasi saldo5Cari Nasabah🚧 On ProgressMenunggu algoritma Sequential Search6Ranking Saldo🚧 On ProgressMenunggu algoritma Bubble Sort7Statistik (Max/Min)🚧 On ProgressMenunggu algoritma MaxMin💻 Kode Program (Source Code)Berikut adalah kode program untuk milestone 50%.#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// --- KONFIGURASI ---
// Saya mendefinisikan konstanta ini untuk membatasi jumlah maksimal data nasabah
// agar penggunaan memori array tetap terkendali.
#define MAX_NASABAH 100
#define MAX_STRING 50

// TODO: Saya akan menambahkan definisi MAX_RIWAYAT di sini apabila fitur histori transaksi telah selesai saya implementasikan.

// --- STRUKTUR DATA ---
// Saya menggunakan Struct ini sebagai wadah untuk mengelompokkan data per nasabah.
// Saat ini, saya baru menyimpan data identitas dasar dan saldo.
typedef struct {
    char id[10];
    char nama[MAX_STRING];
    char alamat[MAX_STRING];
    long saldo;
    // RENCANA: Ke depannya, saya akan menambahkan array di dalam struct ini untuk mencatat riwayat transaksi.
} Nasabah;

// --- VARIABEL GLOBAL ---
// Array ini saya gunakan sebagai database sementara untuk menampung seluruh data nasabah.
Nasabah daftarNasabah[MAX_NASABAH];
// Variabel ini berfungsi sebagai penghitung (counter) agar saya mengetahui jumlah nasabah yang telah terdaftar saat ini.
int jumlahNasabah = 0; 

// --- PROTOTYPE ---
// Saya mendeklarasikan fungsi-fungsi ini di awal agar program utama (main) dapat mengenali fungsi tersebut sebelum definisinya ditulis di bawah.
void registrasiNasabah();
void lihatSemuaData();
void setorSampah();
long hitungHarga(int jenis, float berat); // Fungsi ini saya gunakan untuk mengkalkulasi total uang yang didapat.
void fiturBelumTersedia(); // Fungsi placeholder untuk menampilkan pesan pada menu yang belum selesai saya kerjakan.
void clearScreen();
void pauseScreen();
void bersihkanNewline(char* str);

// ==========================================
// PROGRAM UTAMA (MAIN)
// ==========================================
int main() {
    // Saya menonaktifkan buffering output agar teks dapat langsung muncul di terminal Visual Studio Code tanpa jeda (delay).
    setbuf(stdout, NULL); 

    int pilihan;
    char bufferInput[10]; 

    do {
        clearScreen();
        // Tampilan menu ini saya buat untuk menunjukkan progres pengerjaan sebesar 50%.
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
        
        // Saya memilih menggunakan fgets daripada scanf agar pembacaan input lebih aman dan menghindari bug input yang terlewati.
        fgets(bufferInput, sizeof(bufferInput), stdin);
        pilihan = atoi(bufferInput); // Saya mengonversi input string menjadi integer.

        switch (pilihan) {
            case 1: registrasiNasabah(); break;
            case 2: lihatSemuaData(); break;
            case 3: setorSampah(); break;
            case 4: 
            case 5: 
            case 6: 
            case 7: 
            case 8: 
                fiturBelumTersedia(); // Apabila pengguna memilih menu yang belum selesai saya buat, saya akan menampilkan pesan informasi.
                break;
            case 0: printf("\nKeluar program...\n"); break;
            default: printf("\nMenu salah.\n"); pauseScreen();
        }

    } while (pilihan != 0); // Perulangan akan terus berjalan hingga pengguna memilih angka 0.

    return 0;
}

// --- FUNGSI UTAMA (YANG SUDAH SELESAI SAYA KERJAKAN) ---

void registrasiNasabah() {
    clearScreen();
    printf("--- REGISTRASI NASABAH ---\n");

    // Saya melakukan pengecekan kapasitas array terlebih dahulu untuk mencegah error overflow.
    if (jumlahNasabah >= MAX_NASABAH) {
        printf("Array Penuh.\n"); pauseScreen(); return;
    }

    Nasabah baru;
    
    // Saya meminta input ID Nasabah.
    printf("Masukkan ID: ");
    fgets(baru.id, sizeof(baru.id), stdin);
    bersihkanNewline(baru.id); // Saya membersihkan karakter newline (\n) agar string tersimpan dengan rapi.
    
    // TODO: Saya perlu menambahkan algoritma pengecekan ID unik di sini untuk mencegah duplikasi data (menunggu fitur Searching selesai).

    printf("Nama Lengkap: ");
    fgets(baru.nama, sizeof(baru.nama), stdin);
    bersihkanNewline(baru.nama);

    printf("Alamat: ");
    fgets(baru.alamat, sizeof(baru.alamat), stdin);
    bersihkanNewline(baru.alamat);
    
    baru.saldo = 0; // Saya menetapkan saldo awal sebesar 0 untuk nasabah baru.

    // Saya menyimpan data struct baru ke dalam array global pada indeks yang sesuai.
    daftarNasabah[jumlahNasabah] = baru;
    jumlahNasabah++; // Saya menambahkan nilai counter setelah data berhasil disimpan.

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
        // Saya menggunakan perulangan for untuk menampilkan seluruh isi array satu per satu.
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
    // Karena fitur Searching belum saya implementasikan, input data masih dilakukan secara manual berdasarkan indeks.

    if (jumlahNasabah == 0) { printf("Belum ada data.\n"); pauseScreen(); return; }

    // Saya menampilkan data terlebih dahulu agar pengguna mengetahui nomor urut nasabah yang ingin dipilih.
    // Rencananya, ini akan saya ganti dengan pencarian ID setelah fiturnya selesai.
    lihatSemuaData(); 
    printf("\n(Sementara pilih manual pakai nomor urut karena Searching belum beres)\n");
    
    int index;
    printf("Pilih nomor urut nasabah (1 - %d): ", jumlahNasabah);
    char buff[10]; fgets(buff, 10, stdin);
    index = atoi(buff) - 1; // Saya mengurangi input dengan 1 karena indeks array dimulai dari 0.

    // Saya melakukan validasi untuk memastikan indeks yang dipilih valid.
    if (index >= 0 && index < jumlahNasabah) {
        printf("\nInput sampah untuk: %s\n", daftarNasabah[index].nama);
        printf("Jenis: 1.Plastik 2.Kertas 3.Logam\n");
        
        int jenis; float berat;
        printf("Pilih (1-3): "); fgets(buff, 10, stdin); jenis = atoi(buff);
        printf("Berat (kg): "); fgets(buff, 10, stdin); berat = atof(buff);

        long total = hitungHarga(jenis, berat);
        daftarNasabah[index].saldo += total; // Saya melakukan pembaruan (update) saldo nasabah.

        printf("Saldo bertambah: Rp. %ld\n", total);
        // TODO: Saya akan menambahkan fitur pencatatan riwayat transaksi dan pencetakan struk pada tahap selanjutnya.
    } else {
        printf("Index salah.\n");
    }
    pauseScreen();
}

// --- FUNGSI BANTUAN ---

long hitungHarga(int jenis, float berat) {
    // Saat ini harga masih saya tentukan secara statis (hardcode), nanti akan saya buat lebih fleksibel.
    if (jenis == 1) return (long)(berat * 3000);
    if (jenis == 2) return (long)(berat * 2000);
    if (jenis == 3) return (long)(berat * 7000);
    return 0;
}

// Ini adalah fungsi placeholder yang saya buat untuk menangani menu yang belum selesai dikerjakan.
void fiturBelumTersedia() {
    printf("\n[UNDER CONSTRUCTION]\n");
    printf("Maaf, fitur ini sedang dalam tahap pengerjaan (Coding).\n");
    printf("Rencana implementasi: Menggunakan algoritma Bubble Sort/Sequential Search.\n");
    pauseScreen();
}

void clearScreen() {
    // Saya melakukan pengecekan sistem operasi; jika Windows menggunakan 'cls', jika Linux/Mac menggunakan 'clear'.
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

// Fungsi utilitas ini saya buat untuk menghapus karakter newline (\n) yang terbawa saat menggunakan fgets.
void bersihkanNewline(char* str) {
    str[strcspn(str, "\n")] = 0;
}
