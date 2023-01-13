# Program Daftar Nilai Mahasiswa

Source Code

Main.py

    import view.input_nilai as view
    import view.view_nilai as inp
    import model.daftar_nilai as dn


    data = {}

    while True:
        print('[(T)ambah, (U)bah, (L)ihat, (H)apus, (C)ari, (K)eluar]')
        pilih2 = input('Pilih Menu :  ')
        if pilih2 == 't':
            view.tambahdata(data, dn)
        elif pilih2 == 'u':
            dn.ubah_data(data)
        elif pilih2 == 'l':
            inp.lihatdata(data)
        elif pilih2 == 'h':
            dn.hapus_data(data)
        elif pilih2 == 'c':
            inp.cetak_data(data, dn)
        elif pilih2 == 'k':
            break


        else:
            tidak = input('Menu Tidak Ada ')

tambahdata di file view_nilai :

    def tambahdata(df,dn):
        print("Tambah Data")
        nim = int(input("NIM            : "))
        nama = input("Nama           : ")
        tugas = int(input("Nilai Tugas    : "))
        uts = int(input("Nilai UTS      : "))
        uas = int(input("Nilai UAS      : "))
        dn.tambah_data(df, nim, nama, tugas, uts, uas)


tamba_data di file daftar_nilai :

    def tambah_data(df, nim, nama, tugas, uts, uas):
        print("Menambahkan Data..")
        akhir = ((int(tugas) / 100*30) + (int(uts)/100*35) + (int(uas) / 100*35))
        df[nim] = {"nama": nama, "tugas": tugas,
                "uts": uts, "uas": uas, "akhir": akhir}
        print("Data Berhasil tersimpan")
    
lihatdata pada file view_nilai :

    def lihatdata(df):
        if df.items():
            print("Daftar Nilai")
            print("=" * 78)
            print("| NO | NIM            |       NAMA       |  TUGAS  |  UTS  |  UAS  |  Akhir  |")
            print("=" * 78)
            x = 1
            for i, j in df.items():
                print('| {0:^3}| {1:11} | {2:<17} | {3:7} | {4:4} | {5:3} | {6:7.2f} |'.format(
                    x, i, df[i]["nama"], df[i]["tugas"], df[i]["uts"], df[i]["uas"], df[i]["akhir"]))
                x += 1
            i = 0

            print("=" * 78)
        else:
            print("Daftar Nilai")
            print("=" * 78)
            print("| NO | NIM            |       NAMA       |  TUGAS  |  UTS  |  UAS  |  Akhir  |")
            print("=" * 78)
            print("|                                TIDAK ADA DATA                              |")
            print("=" * 78)

ubah_data pada file daftar_nilai :

    def ubah_data(data):
        print("Ubah Data")
        nama = input("Masukkan Nama  : ")
        if nama in data.keys():
            nim = int(input("NIM            : "))
            tugas = int(input("Nilai Tugas    : "))
            uts = int(input("Nilai UTS      : "))
            uas = int(input("Nilai UAS      : "))
            akhir = tugas * 30 / 100 + uts * 35 / 100 + uas * 35 / 100
            data[nama] = nim, uts, uas, tugas, akhir
        else:
            print("Nama {0} tidak ditemukan".format(nama))

cetak_data pada file view_nilai:

    def cetak_data(df, dn):
        print("mencetak hasil cari nilai...")
        nama = input("Cari Data nilai berdasarkan Nama : ")
        Jdl_Tbl()
        dn.Cari_data(df, nama)
        foot_Tbl()

cari_data pada file daftar_nilai :

    def Cari_data(df, nama):
        x, found = 0, 0
        for i, j in df.items():
            x += 1
            if (df.get(i)).get('nama').startswith(nama):
                found += 1
                print('| {0:^3}| {1:11} | {2:<17} | {3:7} | {4:4} | {5:3} | {6:6.2f} |'.format(
                    1, i, df[i]["nama"], df[i]["tugas"], df[i]["uts"], df[i]["uas"], df[i]["akhir"]))
        if (found == 0):
            print("Data tidak ada")

hapus_data pada file daftar_nilai :

    def hapus_data(data):
        print("Hapus Data")
        nama = input("Masukkan Nama  : ")
        if nama in data.keys():
            del data[nama]
        else:
            print("Nama {0} Tidak Ditemukan".format(nama))
