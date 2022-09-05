# [Project 1: Penduduk Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)
- Pulau Jawa merupakan pulau terpadat di dunia
- Hampir 60% penduduk Indonesia tinggal di Pulau Jawa
- Pulau Jawa terdiri dari 5 provinsi
![alt text](scsc.png)

# [Project 2: PDRB Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)
- Pulau Jawa merupakan pusat perekonomian Indonesia
- Jakarta selaku ibukota merupakan salah satu metropolitan terbesar di dunia
![alt text](g2ie2e.png)

# Code in R
`#Kabupaten tanpa 'Kabupaten' Kota dengan 'Kota'`<br/>
`jakarta2020 <- read_excel ('Jakarta.xlsx')`<br/>
`banten2020 <- read_excel ('Banten.xlsx')`<br/>
`jabar2020 <- read_excel ('Jawa Barat.xlsx')`<br/>
`jatim2020 <- read_excel ('Jawa Timur.xlsx')`<br/>
`jateng2020 <- read_excel ('Jawa Tengah.xlsx')`<br/>
`yogya2020 <- read_excel ('Yogyakarta.xlsx')`<br/>
<br/>
`jakarta2020 <- jakarta2020[-c(1:2,10:13),]`<br/>
`jakarta2020 <- jakarta2020[,c(1,3)]`<br/>
`jabar2020 <- jabar2020[,c(1,4)]`<br/>
`jabar2020 <- jabar2020[-c(1,30:33),]`<br/>
`jateng2020 <- jateng2020[,c(1,3)]`<br/>
`jateng2020 <- jateng2020[-c(1,38:41),]`<br/>
`jatim2020 <- jatim2020[,c(1,10)]`<br/>
`jatim2020 <- jatim2020[-c(1:2,42:45),]`<br/>
`banten2020 <- banten2020[,c(1,9)]`<br/>
`banten2020 <- banten2020[-c(1:2,12:15),]`<br/>
`yogya2020 <- yogya2020[,c(1:2)]`<br/>
`yogya2020 <- yogya2020[-c(1,8:11),]`<br/>
<br/>
`jakarta2020 <- jakarta2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
`jateng2020 <- jateng2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
`jabar2020 <- jabar2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
`jatim2020 <- jatim2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
`banten2020 <- banten2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
`yogya2020 <- yogya2020 %>%`<br/>
&emsp;&emsp;`setNames(c("Daerah", "Penduduk"))`<br/>
<br/>
`#penduduk jakarta 2268.81 ubah ke integer dan dikali 1000`<br/>
`library(readr) --parse_number()`<br/>
`jakarta2020$Penduduk <- jakarta2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
`jakarta2020 <- jakarta2020 %>%`<br/>
&emsp;&emsp;`mutate(Penduduk = Penduduk*1000)`<br/>
`banten2020$Penduduk <- banten2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
`jabar2020$Penduduk <- jabar2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
`jatim2020$Penduduk <- jatim2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
`jateng2020$Penduduk <- jateng2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
`yogya2020$Penduduk <- yogya2020$Penduduk %>%`<br/>
&emsp;&emsp;`parse_number()`<br/>
<br/>
`#add Provinsi table`<br/>
`yogya2020 <- yogya2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Yogyakarta')`<br/>
`jabar2020 <- jabar2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Jawa Barat')`<br/>
`jatim2020 <- jatim2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Jawa Timur')`<br/>
`jateng2020 <- jateng2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Jawa Tengah')`<br/>
`banten2020 <- banten2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Banten')`<br/>
`jakarta2020 <- jakarta2020 %>%`<br/>
&emsp;&emsp;`mutate(Provinsi = 'Jakarta Raya')`<br/>
<br/>
`bindrow<br/>`<br/>
`jawa2020 <- banten2020 %>%`<br/>
&emsp;&emsp;`bind_rows(jakarta2020, jabar2020, jateng2020, jatim2020, yogya2020)`<br/>
<br/>
`#rename`<br/>
`jawa2020$Daerah <- jawa2020$Daerah  %>%`<br/>
&emsp;&emsp;`str_replace("Kabupaten ", "") %>%`<br/>
&emsp;&emsp;`str_replace("Kab ", "") %>%`<br/>
&emsp;&emsp;`str_replace("Kep", "Kepulauan") %>%`<br/>
&emsp;&emsp;`str_replace("DKI Jakarta", "Jakarta Raya") %>%`<br/>
&emsp;&emsp;`str_replace("D.I. ", "") %>%`<br/>
&emsp;&emsp;`str_replace("PROVINSI JAWA TENGAH", "Jawa Tengah") %>%`<br/>
&emsp;&emsp;`str_replace("Provinsi", "") %>%`<br/>
&emsp;&emsp;`str_replace("Gunungkidul", "Gunung Kidul")`<br/>
&emsp;&emsp;`str_replace("Kulonprogo", "Kulon Progo")`<br/>
&emsp;&emsp;`str_replace("Yogyakarta", "Kota Yogyakarta")`<br/>
<br/>
`jawa2020 <- jawa2020[-c(120),]`<br/>
<br/>
`#web scraping to add pdrb data`<br/>
https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB<br/>
<br/>
`library(rvest)`<br/>
`g <- read_html("https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB")`<br/>
`gdp2016 <- g %>%`<br/>
&emsp;&emsp;`html_nodes("table")`<br/>
`gdp2016 <- gdp2016[[1]]`<br/>
`gdp2016 <- gdp2016 %>%`<br/>
&emsp;&emsp;`html_table()`<br/>
<br/>
`gdp2016 <- gdp2016[,c(2:4)]`<br/>
<br/>
`gdp2016 <- gdp2016 %>%
&emsp;&emsp;`setNames(c("Daerah", "Provinsi", "PDRB"))`<br/>
<br/>

`#rename provinsi di pulau jawa`<br/>
`gdp2016$Provinsi <- gdp2016$Provinsi %>%`<br/>
&emsp;&emsp;`str_replace("Daerah Istimewa Yogyakarta", "Yogyakarta") %>%`<br/>
&emsp;&emsp;`str_replace("Daerah Khusus Ibukota Jakarta", "Jakarta Raya") %>%`<br/>
&emsp;&emsp;`str_replace("Daerah Khusus Ibu Kota Jakarta", "Jakarta Raya")`<br/>
<br/>

`#filter hanya provinsi di pulau jawa`<br/>
`gdp2016 <- gdp2016 %>%`<br/>
&emsp;&emsp;`filter(Provinsi %in% c('Jakarta Raya', 'Jawa Barat', 'Banten', 'Jawa Tengah', 'Yogyakarta', 'Jawa Timur'))`<br/>
<br/>

`#rename nama daerah`<br/>
`gdp2016$Daerah <- gdp2016$Daerah  %>%`<br/>
&emsp;&emsp;`str_replace("Kabupaten ", "") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Administrasi ", "") %>%`<br/>
&emsp;&emsp;`str_replace("Administrasi ", "") %>%`<br/>
&emsp;&emsp;`str_replace("Gunungkidul", "Gunung Kidul")`<br/>
<br/>

`#join jawa2020 & gdp2016`<br/>
`join <- jawa2020 %>%`<br/>
&emsp;&emsp;`inner_join(gdp2016, by = "Daerah")`<br/>
<br/>

`#penyesuaian dengan data shp`<br/>
`join$Daerah <- join$Daerah %>%`<br/>
&emsp;&emsp;`str_replace("Kota Cilegon", "Cilegon") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Tangerang Selatan", "Tangerang Selatan") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Depok", "Depok") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Cimahi", "Cimahi") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Banjar", "Banjar") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Salatiga", "Salatiga") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Surakarta", "Surakarta") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Batu", "Batu") %>%`<br/>
&emsp;&emsp;`str_replace("Kota Surabaya", "Surabaya")`<br/>

# Code in Python
`#Import file`<br/>
`#Import library`<br/>
`import pandas as pd`<br/>
`import numpy as pd`<br/>
`import matplotlib.pyplot as plt`<br/>
<br/>
`#read files`<br/>
`data1= pd.read_excel('PDRB 2010.xlsx')`<br/>
`data2= pd.read_excel('PDRB 2010B.xlsx')`<br/>
`data3= pd.read_excel('PDRB 2010C.xlsx')`<br/>
<br/>
`#rename columns`<br/>
`data1.rename(columns={'Provinsi': 'Provinsi', '[Seri 2010] Produk Domestik Regional Bruto (Milyar Rupiah)':'2019','Unnamed: 2':'2020', 'Unnamed: 3':'2021'}, inplace = True)`<br/>
`data2.rename(columns={'Provinsi': 'Provinsi', '[Seri 2010] Produk Domestik Regional Bruto (Milyar Rupiah)':'2016','Unnamed: 2':'2017', 'Unnamed: 3':'2018'}, inplace = True)`<br/>
`data3.rename(columns={'Provinsi': 'Provinsi', '[Seri 2010] Produk Domestik Regional Bruto (Milyar Rupiah)':'2013','Unnamed: 2':'2014', 'Unnamed: 3':'2015'}, inplace = True)`<br/>
<br/>

`#delete columns`<br/>
`data1 = data1.drop(`<br/>
&emsp;&emsp;`labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],`<br/>
&emsp;&emsp;`axis = 1,`<br/>
&emsp;&emsp;`inplace = False`<br/>
&emsp;&emsp;`)`<br/>
<br/>
`data2 = data2.drop(`<br/>
&emsp;&emsp;`labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],`<br/>
&emsp;&emsp;`axis = 1,`<br/>
&emsp;&emsp;`inplace = False`<br/>
&emsp;&emsp;`)`<br/>
<br/>
`data3 = data3.drop(`<br/>
&emsp;&emsp;`labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],`<br/>
&emsp;&emsp;`axis = 1,`<br/>
&emsp;&emsp;`inplace = False`<br/>
&emsp;&emsp;`)`<br/>
<br/>

`#delete rows`<br/>
`data3 = data3.drop(`<br/>
&emsp;&emsp;`labels = [0,1,37,38,39,40],`<br/>
&emsp;&emsp;`axis = 0,`<br/>
&emsp;&emsp;`inplace = False`<br/>
&emsp;&emsp;`)`<br/>

`#left join`<br/>
`data23 = pd.merge(data3,data2, on='Provinsi', how='left')`<br/>
<br/>
`#inner join`<br/>
`data123 = pd.merge(data23,data1, on='Provinsi', how='inner')`<br/>
<br/>
`#results`<br/>
`print(data123)`<br/>
<br/>
`#select only province in java island`<br/>
`data123jawa = data123.loc[[15,10,11,12,13,14]]`<br/>
<br/>
`#bar chart grouped visualization`<br/>
`x = np.arange(len(data123jawa.Provinsi))`<br/>
`y5 = data123jawa['2017']`<br/>
`y6 = data123jawa['2018']`<br/>
`y7 = data123jawa['2019']`<br/>
`y8 = data123jawa['2020']`<br/>
`y9 = data123jawa['2021']`<br/>
<br/>
`width = 0.1`<br/>
<br/>

`fig, ax = plt.subplots()`<br/>
`rects5 = ax.bar(x - 0.2, y5, width, label='2017')`<br/>
`rects6 = ax.bar(x - 0.1, y6, width, label='2018')`<br/>
`rects7 = ax.bar(x - 0.0, y7, width, label='2019')`<br/>
`rects8 = ax.bar(x + 0.1, y8, width, label='2020')`<br/>
`rects9 = ax.bar(x + 0.2, y9, width, label='2021')`<br/>
<br/>
`ax.set_ylabel('GDP')`<br/>
`ax.set_title('GDP (Nominal) in Java Island')`<br/>
`ax.set_xticks(x, data123jawa['Provinsi'])`<br/>
`ax.legend()`<br/>
<br/>
`fig.tight_layout()`<br/>
<br/>
`plt.show()`<br/>
<br/>
`#reshaped`<br/>
`data123jawa_reshaped = pd.melt(data123jawa, id_vars='Provinsi', value_name='GDP', var_name='year')`<br/>
<br/>




# Code in SQL
`#import table to the database (csv) - UI`<br/>
<br/>
`#rename table`<br/>
`rename table girrafe.pdrb TO girrafe.pdrb1;`<br/>
<br/>
`#delete and rename columns`<br/>
`select * from pdrb1;`<br/>
`alter table girrafe.pdrb1 drop column `2019 Konstan`;`<br/>
`alter table girrafe.pdrb1 drop column `2020 Konstan`;`<br/>
`alter table girrafe.pdrb1 drop column `2021 Konstan`;`<br/>
`alter table girrafe.pdrb1 change `2019 Berlaku` `2019` double null;`<br/>
`alter table girrafe.pdrb1 change `2020 Berlaku` `2020` double null;`<br/>
`alter table girrafe.pdrb1 change `2021 Berlaku` `2021` double null;`<br/>

`select * from pdrb2;`<br/>
`alter table girrafe.pdrb2 drop column `2016 Konstan`;`<br/>
`alter table girrafe.pdrb2 drop column `2017 Konstan`;`<br/>
`alter table girrafe.pdrb2 drop column `2018 Konstan`;`<br/>
`alter table girrafe.pdrb2 change `2016 (nominal)` `2016` double null;`<br/>
`alter table girrafe.pdrb2 change `2017 (nominal)` `2017` double null;`<br/>
`alter table girrafe.pdrb2 change `2018 (nominal)` `2018` double null;`<br/>
<br/>
`select * from pdrb3;`<br/>
`alter table girrafe.pdrb3 drop column `2013h`;`<br/>
`alter table girrafe.pdrb3 drop column `2014i`;`<br/>
`alter table girrafe.pdrb3 drop column `2015j`;`<br/>
`alter table girrafe.pdrb3 change `2013 (nominal)` `2013` double null;`<br/>
`alter table girrafe.pdrb3 change `2014 (nominal)` `2014` double null;`<br/>
`alter table girrafe.pdrb3 change `2015 (nominal)` `2015` double null;`<br/>
<br/>
`#inner join`<br/>
`create table pdrb23 (
	select pdrb3.Provinsi, `2013`, `2014`, `2015`, `2016`, `2017`, `2018` from pdrb3
	inner join pdrb2
	on pdrb3.Provinsi = pdrb2.Provinsi
);`<br/>
<br/>
`select * from pdrb23`<br/>
<br/>
`create table pdrb123 (
	select pdrb23.Provinsi, `2013`, `2014`, `2015`, `2016`, `2017`, `2018`, `2019`, `2020`, `2021` from pdrb23
	inner join pdrb1
	on pdrb23.Provinsi = pdrb1.Provinsi
);
`<br/>
<br/>
`#results`<br/>
`select * from pdrb123;`<br/>
