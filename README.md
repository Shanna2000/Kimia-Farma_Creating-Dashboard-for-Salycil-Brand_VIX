# Kimia Farma_Dashboard for Salicyl Brand Sales
## Data Warehouse, Data Lake, and Data Mart
There are three types repository data:
- Data Warehouse: The place where all the data gathered in one repository and most likely, the data very unstructure.
- Data Lake: A derivative of the data warehouse but has been tidied up and more structured but the scope is still very broad
- Data Mart: A dervative from a data lake and aimed for a particular field analysis data.
For this task, we need to make a data mart with just contained Salicyl Brand from the Data Lake

## Dataset
The dataset formed Excel with three sheets: Sheet 'penjualan', 'pelanggan', and 'barang'
- Sheet 'penjualan': contain sales data for the entire year
- Sheet 'pelanggan': contain customer data
- Sheet 'barang': contain products from Kimia Farma with several brands, including Salicyl Brand <br>
From the database, we need to make Table Base and Table Aggregate. Table base contained raw data for the Salicyl Brand whereas Table Aggregate is derivied from Tabel Base and contain more short data to visualize with Google Data Studio

## Table and SQL Queries
### Table Base
Here are my SQL Queries to create the Table Base: <br>
```sql
Create table Tabel_base_salicyl as
select 
	penjualan.id_cabang,
	pelanggan.cabang_sales,
	penjualan.id_customer,
	pelanggan.nama,
	penjualan.id_distributor,
	penjualan.id_barang,
	barang.nama_barang,
	barang.lini,
	penjualan.tanggal,
	to_char(penjualan.tanggal, 'Month') as bulan,
	penjualan.jumlah_barang,
	penjualan.harga
from penjualan 
join barang on barang.kode_barang = penjualan.id_barang
join pelanggan on penjualan.id_customer = pelanggan.id_customer
where barang.lini = 'SLCYL'
