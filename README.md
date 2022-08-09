# [Project 1: Penduduk Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)
- Pulau Jawa merupakan pulau terpadat di dunia
- Hampir 60% penduduk Indonesia tinggal di Pulau Jawa
- Pulau Jawa terdiri dari 5 provinsi
![alt text](scsc.png)

# [Project 2: PDRB Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)
- Pulau Jawa merupakan pusat perekonomian Indonesia
- Jakarta selaku ibukota merupakan salah satu metropolitan terbesar di dunia
![alt text](g2ie2e.png)

# Code
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
jabar2020 <- jabar2020 %>%
    setNames(c("Daerah", "Penduduk"))<br/><br/>
jatim2020 <- jatim2020 %>%
    setNames(c("Daerah", "Penduduk"))<br/>
banten2020 <- banten2020 %>%
    setNames(c("Daerah", "Penduduk"))<br/>
yogya2020 <- yogya2020 %>%
    setNames(c("Daerah", "Penduduk"))<br/>
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
