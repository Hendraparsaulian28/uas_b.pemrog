# UAS BAHASA PEMOGRAMAN
## Link Youtube: coming soon

        from tabulate import tabulate  # Modul eksternal untuk menampilkan tabel (pip install tabulate)


        class Mahasiswa:
        def __init__(self, nim, nama, nilai, semester, jenis_kelamin):
        self.nim = nim
        self.nama = nama
        self.nilai = nilai
        self.semester = semester
        self.jenis_kelamin = jenis_kelamin



    class View:
    @staticmethod
    def tampilkan_data(data_mahasiswa):
        if not data_mahasiswa:
            print("Tidak ada data untuk ditampilkan.")
            return

        # Membuat tabel menggunakan tabulate
        tabel = [[mhs.nim, mhs.nama, mhs.nilai, mhs.semester, mhs.jenis_kelamin] for mhs in data_mahasiswa]
        print(tabulate(tabel, headers=["NIM", "Nama", "Nilai", "Semester", "Jenis Kelamin"], tablefmt="grid"))

    @staticmethod
    def tampilkan_pesan(pesan):
        print(pesan)



    class Process:
    def __init__(self):
        self.data_mahasiswa = []

    # Menambahkan data mahasiswa dengan validasi
    def tambah_data(self):
        try:
            nim = input("Masukkan NIM: ").strip()
            if not nim.isdigit() or len(nim) != 9:
                raise ValueError("NIM harus berupa 9 digit angka!")

            nama = input("Masukkan Nama: ").strip()
            if not nama.replace(" ", "").isalpha():
                raise ValueError("Nama hanya boleh berisi huruf!")

            nilai = float(input("Masukkan Nilai: ").strip())
            if nilai < 0 or nilai > 100:
                raise ValueError("Nilai harus dalam rentang 0-100!")

            semester = input("Masukkan Semester: ").strip()
            if not semester.isdigit() or int(semester) < 1:
                raise ValueError("Semester harus berupa angka positif!")

            jenis_kelamin = input("Masukkan Jenis Kelamin (L/P): ").strip().upper()
            if jenis_kelamin not in ['L', 'P']:
                raise ValueError("Jenis kelamin harus 'L' atau 'P'!")

            # Menambahkan data ke dalam list
            mahasiswa = Mahasiswa(nim, nama, nilai, semester, jenis_kelamin)
            self.data_mahasiswa.append(mahasiswa)
            View.tampilkan_pesan("Data berhasil ditambahkan!")
        except ValueError as e:
            View.tampilkan_pesan(f"Input tidak valid: {e}")
        except Exception as e:
            View.tampilkan_pesan(f"Terjadi kesalahan: {e}")

    # Menghapus data berdasarkan NIM
    def hapus_data(self):
        try:
            nim = input("Masukkan NIM yang akan dihapus: ").strip()
            for mhs in self.data_mahasiswa:
                if mhs.nim == nim:
                    self.data_mahasiswa.remove(mhs)
                    View.tampilkan_pesan("Data berhasil dihapus!")
                    return
            View.tampilkan_pesan("NIM tidak ditemukan.")
        except Exception as e:
            View.tampilkan_pesan(f"Terjadi kesalahan: {e}")

    # Mengubah data berdasarkan NIM
    def ubah_data(self):
        try:
            nim = input("Masukkan NIM yang akan diubah: ").strip()
            for mhs in self.data_mahasiswa:
                if mhs.nim == nim:
                    nama_baru = input("Masukkan Nama baru: ").strip()
                    if not nama_baru.replace(" ", "").isalpha():
                        raise ValueError("Nama hanya boleh berisi huruf!")

                    nilai_baru = float(input("Masukkan Nilai baru: ").strip())
                    if nilai_baru < 0 or nilai_baru > 100:
                        raise ValueError("Nilai harus dalam rentang 0-100!")

                    semester_baru = input("Masukkan Semester baru: ").strip()
                    if not semester_baru.isdigit() or int(semester_baru) < 1:
                        raise ValueError("Semester harus berupa angka positif!")

                    jenis_kelamin_baru = input("Masukkan Jenis Kelamin baru (L/P): ").strip().upper()
                    if jenis_kelamin_baru not in ['L', 'P']:
                        raise ValueError("Jenis kelamin harus 'L' atau 'P'!")

                    mhs.nama = nama_baru
                    mhs.nilai = nilai_baru
                    mhs.semester = semester_baru
                    mhs.jenis_kelamin = jenis_kelamin_baru
                    View.tampilkan_pesan("Data berhasil diubah!")
                    return
            View.tampilkan_pesan("NIM tidak ditemukan.")
        except ValueError as e:
            View.tampilkan_pesan(f"Input tidak valid: {e}")
        except Exception as e:
            View.tampilkan_pesan(f"Terjadi kesalahan: {e}")

    # Menampilkan semua data
    def tampilkan_semua_data(self):
        View.tampilkan_data(self.data_mahasiswa)



        def main():
    process = Process()

    while True:
        print("\n=== MENU UTAMA ===")
        print("1. Tambah Data")
        print("2. Hapus Data")
        print("3. Ubah Data")
        print("4. Tampilkan Semua Data")
        print("5. Keluar")

        pilihan = input("Pilih menu (1-5): ").strip()
        if pilihan == "1":
            process.tambah_data()
        elif pilihan == "2":
            process.hapus_data()
        elif pilihan == "3":
            process.ubah_data()
        elif pilihan == "4":
            process.tampilkan_semua_data()
        elif pilihan == "5":
            print("Program selesai. Terima kasih!")
            break
        else:
            print("Pilihan tidak valid. Silakan pilih 1-5.")


        if __name__ == "__main__":
            main()
