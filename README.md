# Bahasa Pemograman Uas

Nama: Rahmat Ibnu Zidane

Nim: 312210471

Kelas: TI.22.B2

## Buatlah package dan modul dengan struktur seperti berikut:

-daftar_nilai.py berisi modul untuk tambah data, ubah data, cari data, hapus data -cetak_nilai.py berisi modul untuk cetak daftar nilai, cetak hasil pencarian -nput_nilai.py berisi modul untuk input data yang diminta pengguna untuk memasukkan data -main. py berisi program secara keseluruhan -Susunan package dan modul nya akan terlihat seperti di bawah ini

Berikut adalah prograam programnya

- dibawah ini adalah script untuk daftar_nilai.py

from tabulate import tabulate
from view import input_nilai
from view import view_nilai


def tambah_data(data):
    newData = input_nilai.input_data(data)
    return data

def hapus_data(data, nama):
    if nama in data['nama']:
        # buat dictionary kosong untuk menampilkan data yang cocok sesuai input NIM
        dataMhs = {}
        index = data['nama'].index(nama)

        # lakukan pengisian data yang cocok ke dalam variabel dataMhs
        for key in data.keys():
            dataMhs[key] = []
            dataMhs[key].append(data[key][index])
        print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))
        # lakukan konfirmasi penghapusan
        confirm = input("anda yakin ingin menghapus data ini?? (y/t)")

        # jika input selain y atau t lakukan konfirmasi berulang
        while (confirm not in ['y', 't']):
            print("input salah")
            confirm = input("anda yakin ingin menghapus data ini?? (y/t)")

        # jika konfirmasi selesai dilakukan, maka hapus data mahasiswa pada variabel data
        if confirm == "y":
            for key in data.keys():
                data[key].pop(index)
            print("Data Berhasil Dihapus!!\n")
        return data

    else:
        print("data nama tidak ditemukan!!")
        
def ubah_data(data, nama):
    if nama in data['nama']:
        # buat dictionary kosong untuk menampilkan data yang cocok sesuai input nama
        dataMhs = {}
        index = data['nama'].index(nama)
        # lakukan pengisian data yang cocok ke dalam variabel dataMhs
        for key in data.keys():
            dataMhs[key] = []
            dataMhs[key].append(data[key][index])

        print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))
        # lakukan input data apa yang akan diubah
        pilihan = input("pilih field yang akan diubah : \n1.Nama\n2.Nilai\n")
        # lakukan pengecekan pada variabel pilihan yang dikonversi menjadi nilai integer
        match int(pilihan):
            case 1:
                print("data nama sebelumnya : " + dataMhs['nama'][0])
                nama = input("Masukkan nama Baru : ")
                while nama in data['nama']:
                    if nama == dataMhs['nama'][0]:
                        break
                    print("Mahasiswa dengan nama yang sama sudah ada")
                    nama = input("Masukkan nama Baru : ")
                data['nama'][index] = nama

            case 2:
                print("data nilai sebelumnya :" , dataMhs['nilai'][0])
                nilai = input("Masukkan nilai baru : ")
                data['nilai'][index] = nilai

        for key in data.keys():
            dataMhs[key] = []
            dataMhs[key].append(data[key][index])
        print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))
        return data
    else:
        print("data nama tidak ditemukan!")

def cari_data(data, nama):
    dataMhs = {}
    if nama in data['nama']:
        index = data['nama'].index(nama)
        for key in data.keys():
            dataMhs[key] = []
            dataMhs[key].append(data[key][index])
        view_nilai.cetak_hasil_pencarian(dataMhs)
    else:
        print("Data Tidak Ditemukan!")
        
        
![ss52](https://user-images.githubusercontent.com/115911489/211203959-5791b8a1-37d3-41c4-9caa-2f9c403477b5.JPG)



![ss53](https://user-images.githubusercontent.com/115911489/211203964-ea7eaa58-18aa-4ac4-badc-306c4cf8bbe0.JPG)



![ss54](https://user-images.githubusercontent.com/115911489/211203973-b0cb0b97-9c2c-48f4-b3ec-a4c5251c24db.JPG)



![ss55](https://user-images.githubusercontent.com/115911489/211203981-1946e5ed-f097-4a82-954e-78e5b25bc507.JPG)



- dibawah ini adalah script untuk view_nilai.py

from tabulate import tabulate

def cetak_daftar_nilai(data):
    # variabel i untuk membuat penomoran data ketika dibuat tabel
    i = range(1, len(data['nama'])+1)
    # membuat list header kolom yang akan ditampilkan
    headers = ["No", "Nama", "Nilai"]

    # data dapat ditampilkan jika variabel data terisi minimal satu data
    if len(data['nama']) > 0:
        print(tabulate(data, headers, showindex=i,tablefmt="rounded_outline"))

    # jika tidak ada data, maka tampilkan pesan
    else:
        print("\nTidak Ada Data \n")
        
def cetak_hasil_pencarian(dataMhs):
        print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline
        
        
        ![ss58](https://user-images.githubusercontent.com/115911489/211205500-60637a52-24ec-46b0-ad85-0487c2cc9c5b.JPG)



- dibawah ini script untuk input_nilai.py

def input_data(data):
    # buat inputan untuk mengisi nama
    nama = input("Masukkan Nama : ")
    while len(nama) < 3:
        nama = input("Masukkan Nama : ")
    
    # jika nim yang di input tersedia pada variabel data, cetak pesan lalu lakukan input ulang
    while nama in data['nama']:
        print("Mahasiswa dengan nama yang sama sudah ada")
        nama = input("Masukkan Nama : ")
    
    nilai = input("masukkan nilai : ")
    while not nilai.isnumeric():
        nilai = input("masukkan nilai : ")
    
    data['nama'].append(nama)
    data['nilai'].append(int(nilai))
    print("Data Berhasil Ditambah!!")
    return data
    
    
    
![ss56](https://user-images.githubusercontent.com/115911489/211205551-67824ee6-def9-4b92-9e2b-588ae80c2bd6.JPG)


    

#Seebelum itu kita harus mendownload pip.tabulate di cmd/command prompt pada pc atau laptop kalian agar tabel yang kita buat bisa muncul di keluarannya nanti 


![Screenshot (8)](https://user-images.githubusercontent.com/115911489/211202671-cb39574e-ace5-4d63-af81-a8d8722d7e77.png)

-dibawh ini adalah script untuk main.py

from model import daftar_nilai
from view import view_nilai

data = {'nama' : [], 'nilai' : []}
while True:
    print("[ (l)ihat , (t)ambah, (c)ari (u)bah, (h)apus, (k)eluar ] \n")
    tanya = input("Masukkan Pilihan : ")
    match tanya:
        case "l":
            view_nilai.cetak_daftar_nilai(data)
        case "t":
            data = daftar_nilai.tambah_data(data)
        case "u":
            view_nilai.cetak_daftar_nilai(data)
            if len(data['nama']) > 0:
                nama = input("masukkan nama siswa yang akan diubah : ")
                data = daftar_nilai.ubah_data(data, nama)
        case "c":
            # view_nilai.cetak_daftar_nilai(data)
            if len(data['nama']) > 0:
                nama = input("masukkan nama siswa yang akan dicari : ")
                daftar_nilai.cari_data(data, nama)
        case "h":
            view_nilai.cetak_daftar_nilai(data)
            if len(data['nama']) > 0:
                nama = input("masukkan nama siswa yang akan dihapus : ")
                data = daftar_nilai.hapus_data(data, nama)
        case "k":
            print("anda sudah Keluar dari program")
            break
        case _:
            print("Tidak Sesuai Pilihan, Silahkan Pilih Kembali!!\n")
            continue
            
![ss59](https://user-images.githubusercontent.com/115911489/211204334-d8810218-d8b6-4b69-ad24-09c3ac6931a4.JPG)



![ss60](https://user-images.githubusercontent.com/115911489/211204345-f60f5fab-5329-4ae5-887a-2467fe66af77.JPG)



## Berikut adalah hasil dari keluaran programnya

-dibawah ini adalah hasil program ketika menambahkan data

![ss48](https://user-images.githubusercontent.com/115911489/211202835-03b15599-2155-4c9d-a04c-39608060ff22.JPG)


- dibawah ini adalah hasil program ketika menghapus data

![ss49](https://user-images.githubusercontent.com/115911489/211202893-c871c9d1-2279-4f66-995e-7f25b29fccb4.JPG)


- dibnawah ini adalah hasil program untuk mengubah data


![ss50](https://user-images.githubusercontent.com/115911489/211202988-c575a356-f050-493f-b674-15ee6022bdb3.JPG)


- dibawa ini adalah ketika kita sudah keluar dari program

![ss51](https://user-images.githubusercontent.com/115911489/211203042-26de3343-8775-4585-aa06-b60f61c7e6d8.JPG)


https://youtu.be/I5SHMv_2WTQ

berikut  video tutrialnya

