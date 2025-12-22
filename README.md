Nama : Navyta Budi Yulia

NIM : 312410184

kelas : TI.24.A2

# Lab13Web

# PRAKTIKUM 13 (Membuat Pagination)

## LANGKAH 1
- Memnentukan jumlah data per halaman `$per_page = 5;`
- Setiap halaman hanya menampilkan 5 data.

## LANGKAH 2
- Menentukan Halaman Aktif
- Halaman aktif diambil dari parameter URL menggunakan `$_GET` :

```
$hal = isset($_GET['hal']) ? (int)$_GET['hal'] : 1;
```
- Jika URL tidak memiliki `hal` → halaman pertama
- Jika `hal=2` → halaman kedua

## LANGKAH 3
- Menghitung OFFSET
- OFFSET digunakan untuk menentukan data mulai dari baris ke berapa
  
```
$offset = ($hal - 1) * $per_page;
```

## LANGKAH 4
- Menggunakan LIMIT dan OFFSET
- Query SQL diubah agar data dibatasi per halaman :

```
$sql = "SELECT * FROM data_barang
        LIMIT $per_page OFFSET $offset";
```

## LANGKAH 5
- Menghitung Total Data
- Total data dihitung untuk menentukan jumlah halaman :

```
$sql_total = "SELECT COUNT(*) AS total FROM data_barang";
```

- Hasil total data dibagi dengan `$per_page`.

## LANGKAH 6
- Menampilkan Pagination (Nomor Halaman, Previous, Next)
- Jumlah halaman dihitung dengan :
  
```
$total_page = ceil($total_data / $per_page);
```

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/5491bb6f-f684-4ccf-a220-e176ca22d10e" />

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/191a6909-fbf2-42e1-9b97-5824ea4ef09d" />

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/11385104-1f3c-4afc-9386-11842f0622ba" />


# PRAKTIKUM 14 (MEembuat Pencarian Data)

## LANGKAH 1
- Membuat Form Pencarian
- Form pencarian dibuat menggunakan metode GET :

```
<form method="GET">
    <input type="text" name="keyword">
    <button type="submit">Cari</button>
</form>
```

## LANGKAH 2
- Menangkap Keyword di PHP
- Keyword yang diketik user ditangkap menggunakan :

```
$keyword = isset($_GET['keyword']) ? $_GET['keyword'] : '';
```
- Jika user mengetik `iphone`, maka : `$keyword = "iphone"`

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/7fbff970-d9b2-43aa-af66-6aa05e751712" />

## LANGKAH 3
- Filter Data Menggunakan WHERE dan LIKE

```
$sql = "SELECT * FROM data_barang
        WHERE nama LIKE '%$keyword%'
        LIMIT $per_page OFFSET $offset";
```

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/ac713ac6-4f98-4bac-ba1d-8cd2b052f291" />

## LANGKAH 4
- Menyesuaikan Pagination dengan Hasil Pencarian
- Agar jumlah halaman sesuai hasil pencarian.

```
$sql_total = "SELECT COUNT(*) AS total
              FROM data_barang
              WHERE nama LIKE '%$keyword%'";
```









