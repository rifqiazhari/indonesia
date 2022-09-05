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
- Kabupaten tanpa 'Kabupaten' Kota dengan 'Kota'<br/>
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
`jakarta2020 <- jakarta2020 %>%
    setNames(c("Daerah", "Penduduk"))`<br/>
`jateng2020 <- jateng2020 %>%
    setNames(c("Daerah", "Penduduk"))`<br/>
`jabar2020 <- jabar2020 %>%
    setNames(c("Daerah", "Penduduk"))`<br/>
`jatim2020 <- jatim2020 %>%
    setNames(c("Daerah", "Penduduk"))`<br/>
`banten2020 <- banten2020 %>%
    setNames(c("Daerah", "Penduduk"))`<br/>
`yogya2020 <- yogya2020 %>%<br/>
    setNames(c("Daerah", "Penduduk"))`<br/>
<br/>
#penduduk jakarta 2268.81 ubah ke integer dan dikali 1000<br/>
`library(readr) --parse_number()`<br/>
`jakarta2020$Penduduk <- jakarta2020$Penduduk %>%
	parse_number()`<br/>
`jakarta2020 <- jakarta2020 %>%
    mutate(Penduduk = Penduduk*1000)`<br/>
`banten2020$Penduduk <- banten2020$Penduduk %>%
    parse_number()`<br/>
`jabar2020$Penduduk <- jabar2020$Penduduk %>%
    parse_number()`<br/>
`jatim2020$Penduduk <- jatim2020$Penduduk %>%
    parse_number()`<br/>
`jateng2020$Penduduk <- jateng2020$Penduduk %>%
    parse_number()`<br/>
`yogya2020$Penduduk <- yogya2020$Penduduk %>%
    parse_number()`<br/>
<br/>
- add Provinsi table<br/>
`yogya2020 <- yogya2020 %>%
    mutate(Provinsi = 'Yogyakarta')`<br/>
`jabar2020 <- jabar2020 %>%
    mutate(Provinsi = 'Jawa Barat')`<br/>
`jatim2020 <- jatim2020 %>%
    mutate(Provinsi = 'Jawa Timur')`<br/>
`jateng2020 <- jateng2020 %>%
    mutate(Provinsi = 'Jawa Tengah')`<br/>
`banten2020 <- banten2020 %>%
    mutate(Provinsi = 'Banten')`<br/>
`jakarta2020 <- jakarta2020 %>%
    mutate(Provinsi = 'Jakarta Raya')`<br/>
<br/>
- bindrow<br/>
`jawa2020 <- banten2020 %>%
    bind_rows(jakarta2020, jabar2020, jateng2020, jatim2020, yogya2020)`<br/>
<br/>
- rename<br/>
`jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Kabupaten ", "") %>%
    str_replace("Kab ", "") %>%
    str_replace("Kep", "Kepulauan") %>%
    str_replace("DKI Jakarta", "Jakarta Raya") %>%
    str_replace("D.I. ", "") %>%
    str_replace("PROVINSI JAWA TENGAH", "Jawa Tengah") %>%
    str_replace("Provinsi", "") %>%
    str_replace("Gunungkidul", "Gunung Kidul")`<br/>
<br/>
`jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Kulonprogo", "Kulon Progo")`<br/>
<br/>
`jawa2020 <- jawa2020[-c(120),]`<br/>
<br/>
`jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Yogyakarta", "Kota Yogyakarta")`<br/>
<br/>
- web scraping to add pdrb data<br/>
https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB<br/>
<br/>
`library(rvest)`<br/>
`g <- read_html("https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB")`<br/>
`gdp2016 <- g %>% html_nodes("table")`<br/>
`gdp2016 <- gdp2016[[1]]`<br/>
`gdp2016 <- gdp2016 %>% html_table`<br/>
<br/>
`gdp2016 <- gdp2016[,c(2:4)]`<br/>
<br/>
`gdp2016 <- gdp2016 %>%
    setNames(c("Daerah", "Provinsi", "PDRB"))`<br/>
<br/>
- rename provinsi di pulau jawa<br/>
`gdp2016$Provinsi <- gdp2016$Provinsi %>%
    str_replace("Daerah Istimewa Yogyakarta", "Yogyakarta") %>%
    str_replace("Daerah Khusus Ibukota Jakarta", "Jakarta Raya") %>%
    str_replace("Daerah Khusus Ibu Kota Jakarta", "Jakarta Raya")`<br/>

- filter hanya provinsi di pulau jawa<br/>
`gdp2016 <- gdp2016 %>%
    filter(Provinsi %in% c('Jakarta Raya', 'Jawa Barat', 'Banten', 'Jawa Tengah', 'Yogyakarta', 'Jawa Timur'))`<br/>

- rename nama daerah<br/>
`gdp2016$Daerah <- gdp2016$Daerah  %>%
    str_replace("Kabupaten ", "") %>%
    str_replace("Kota Administrasi ", "") %>%
    str_replace("Administrasi ", "") %>%
    str_replace("Gunungkidul", "Gunung Kidul")`<br/>
<br/>
- join jawa2020 & gdp2016<br/>
`join <- jawa2020 %>%
    inner_join(gdp2016, by = "Daerah")`<br/>
<br/>
- penyesuaian dengan data shp<br/>
`join$Daerah <- join$Daerah %>%
    str_replace("Kota Cilegon", "Cilegon") %>%
    str_replace("Kota Tangerang Selatan", "Tangerang Selatan") %>%
    str_replace("Kota Depok", "Depok") %>%
    str_replace("Kota Cimahi", "Cimahi") %>%
    str_replace("Kota Banjar", "Banjar") %>%
    str_replace("Kota Salatiga", "Salatiga") %>%
    str_replace("Kota Surakarta", "Surakarta") %>%
    str_replace("Kota Batu", "Batu") %>%
    str_replace("Kota Surabaya", "Surabaya")`<br/>

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
`data1 = data1.drop(
    labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],
    axis = 1,
    inplace = False
)`<br/>
<br/>
`data2 = data2.drop(
    labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],
    axis = 1,
    inplace = False
)`<br/>
<br/>
data3 = data3.drop(
    labels = ["Unnamed: 4", "Unnamed: 5", "Unnamed: 6"],
    axis = 1,
    inplace = False
)

#delete rows
data3 = data3.drop(
    labels = [0,1,37,38,39,40],
    axis = 0,
    inplace = False
)

#left join
data23 = pd.merge(data3,data2, on='Provinsi', how='left')

#inner join
data123 = pd.merge(data23,data1, on='Provinsi', how='inner')

#results
print(data123)

#select only province in java island
data123jawa = data123.loc[[15,10,11,12,13,14]]

#bar chart grouped visualization
x = np.arange(len(data123jawa.Provinsi))
y5 = data123jawa['2017']
y6 = data123jawa['2018']
y7 = data123jawa['2019']
y8 = data123jawa['2020']
y9 = data123jawa['2021']

width = 0.1


fig, ax = plt.subplots()
rects5 = ax.bar(x - 0.2, y5, width, label='2017')
rects6 = ax.bar(x - 0.1, y6, width, label='2018')
rects7 = ax.bar(x - 0.0, y7, width, label='2019')
rects8 = ax.bar(x + 0.1, y8, width, label='2020')
rects9 = ax.bar(x + 0.2, y9, width, label='2021')

ax.set_ylabel('GDP')
ax.set_title('GDP (Nominal) in Java Island')
ax.set_xticks(x, data123jawa['Provinsi'])
ax.legend()

fig.tight_layout()

plt.show()

#reshaped
data123jawa_reshaped = pd.melt(data123jawa, id_vars='Provinsi', value_name='GDP', var_name='year')

# Code in SQL
#import table to the database (csv) - UI

#rename table
rename table girrafe.pdrb TO girrafe.pdrb1;

#delete and rename columns
select * from pdrb1;
alter table girrafe.pdrb1 drop column `2019 Konstan`;
alter table girrafe.pdrb1 drop column `2020 Konstan`;
alter table girrafe.pdrb1 drop column `2021 Konstan`;
alter table girrafe.pdrb1 change `2019 Berlaku` `2019` double null;
alter table girrafe.pdrb1 change `2020 Berlaku` `2020` double null;
alter table girrafe.pdrb1 change `2021 Berlaku` `2021` double null;

select * from pdrb2;
alter table girrafe.pdrb2 drop column `2016 Konstan`;
alter table girrafe.pdrb2 drop column `2017 Konstan`;
alter table girrafe.pdrb2 drop column `2018 Konstan`;
alter table girrafe.pdrb2 change `2016 (nominal)` `2016` double null;
alter table girrafe.pdrb2 change `2017 (nominal)` `2017` double null;
alter table girrafe.pdrb2 change `2018 (nominal)` `2018` double null;

select * from pdrb3;
alter table girrafe.pdrb3 drop column `2013h`;
alter table girrafe.pdrb3 drop column `2014i`;
alter table girrafe.pdrb3 drop column `2015j`;
alter table girrafe.pdrb3 change `2013 (nominal)` `2013` double null;
alter table girrafe.pdrb3 change `2014 (nominal)` `2014` double null;
alter table girrafe.pdrb3 change `2015 (nominal)` `2015` double null;

#inner join
create table pdrb23 (
	select pdrb3.Provinsi, `2013`, `2014`, `2015`, `2016`, `2017`, `2018` from pdrb3
	inner join pdrb2
	on pdrb3.Provinsi = pdrb2.Provinsi
);
select * from pdrb23

create table pdrb123 (
	select pdrb23.Provinsi, `2013`, `2014`, `2015`, `2016`, `2017`, `2018`, `2019`, `2020`, `2021` from pdrb23
	inner join pdrb1
	on pdrb23.Provinsi = pdrb1.Provinsi
);

#results
select * from pdrb123;
