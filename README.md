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

SS

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
 SS

## LANGKAH 3
- Filter Data Menggunakan WHERE dan LIKE

```
$sql = "SELECT * FROM data_barang
        WHERE nama LIKE '%$keyword%'
        LIMIT $per_page OFFSET $offset";
```

SS

## LANGKAH 4
- Menyesuaikan Pagination dengan Hasil Pencarian
- Agar jumlah halaman sesuai hasil pencarian.

```
$sql_total = "SELECT COUNT(*) AS total
              FROM data_barang
              WHERE nama LIKE '%$keyword%'";
```









