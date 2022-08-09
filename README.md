# [Project 1: Penduduk Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)
- sada
- H2saas

# [Project 2: PDRB Kabupaten/ Kota di Pulau Jawa](https://github.com/rifqiazhari/indonesia/blob/main/pulau_jawa)

# THE CODE
#Kabupaten tanpa 'Kabupaten' Kota dengan 'Kota'
`jakarta2020 <- read_excel ('Jakarta.xlsx')`
`banten2020 <- read_excel ('Banten.xlsx')`
jabar2020 <- read_excel ('Jawa Barat.xlsx')
jatim2020 <- read_excel ('Jawa Timur.xlsx')
jateng2020 <- read_excel ('Jawa Tengah.xlsx')
yogya2020 <- read_excel ('Yogyakarta.xlsx')

jakarta2020 <- jakarta2020[-c(1:2,10:13),]
jakarta2020 <- jakarta2020[,c(1,3)]
jabar2020 <- jabar2020[,c(1,4)]
jabar2020 <- jabar2020[-c(1,30:33),]
jateng2020 <- jateng2020[,c(1,3)]
jateng2020 <- jateng2020[-c(1,38:41),]
jatim2020 <- jatim2020[,c(1,10)]
jatim2020 <- jatim2020[-c(1:2,42:45),]
banten2020 <- banten2020[,c(1,9)]
banten2020 <- banten2020[-c(1:2,12:15),]
yogya2020 <- yogya2020[,c(1:2)]
yogya2020 <- yogya2020[-c(1,8:11),]

jakarta2020 <- jakarta2020 %>%
    setNames(c("Daerah", "Penduduk"))
jateng2020 <- jateng2020 %>%
    setNames(c("Daerah", "Penduduk"))
jabar2020 <- jabar2020 %>%
    setNames(c("Daerah", "Penduduk"))
jatim2020 <- jatim2020 %>%
    setNames(c("Daerah", "Penduduk"))
banten2020 <- banten2020 %>%
    setNames(c("Daerah", "Penduduk"))
yogya2020 <- yogya2020 %>%
    setNames(c("Daerah", "Penduduk"))
	
#penduduk jakarta 2268.81 ubah ke integer dan dikali 1000
library(readr) --parse_number()
jakarta2020$Penduduk <- jakarta2020$Penduduk %>%
	parse_number()
jakarta2020 <- jakarta2020 %>%
    mutate(Penduduk = Penduduk*1000)
banten2020$Penduduk <- banten2020$Penduduk %>%
    parse_number()
jabar2020$Penduduk <- jabar2020$Penduduk %>%
    parse_number()
jatim2020$Penduduk <- jatim2020$Penduduk %>%
    parse_number()
jateng2020$Penduduk <- jateng2020$Penduduk %>%
    parse_number()
yogya2020$Penduduk <- yogya2020$Penduduk %>%
    parse_number()

#add Provinsi table
yogya2020 <- yogya2020 %>%
    mutate(Provinsi = 'Yogyakarta')
jabar2020 <- jabar2020 %>%
    mutate(Provinsi = 'Jawa Barat')
jatim2020 <- jatim2020 %>%
    mutate(Provinsi = 'Jawa Timur')
jateng2020 <- jateng2020 %>%
    mutate(Provinsi = 'Jawa Tengah')
banten2020 <- banten2020 %>%
    mutate(Provinsi = 'Banten')
jakarta2020 <- jakarta2020 %>%
    mutate(Provinsi = 'Jakarta Raya')

#bindrow
jawa2020 <- banten2020 %>%
    bind_rows(jakarta2020, jabar2020, jateng2020, jatim2020, yogya2020)

#rename
jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Kabupaten ", "") %>%
    str_replace("Kab ", "") %>%
    str_replace("Kep", "Kepulauan") %>%
    str_replace("DKI Jakarta", "Jakarta Raya") %>%
    str_replace("D.I. ", "") %>%
    str_replace("PROVINSI JAWA TENGAH", "Jawa Tengah") %>%
    str_replace("Provinsi", "") %>%
    str_replace("Gunungkidul", "Gunung Kidul")

jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Kulonprogo", "Kulon Progo")

jawa2020 <- jawa2020[-c(120),]

jawa2020$Daerah <- jawa2020$Daerah  %>%
    str_replace("Yogyakarta", "Kota Yogyakarta")

#web scraping to add pdrb data
https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB

library(rvest)
g <- read_html("https://id.wikipedia.org/wiki/Daftar_kabupaten_dan_kota_di_Indonesia_menurut_PDRB")
gdp2016 <- g %>% html_nodes("table")
gdp2016 <- gdp2016[[1]]
gdp2016 <- gdp2016 %>% html_table

gdp2016 <- gdp2016[,c(2:4)]

gdp2016 <- gdp2016 %>%
    setNames(c("Daerah", "Provinsi", "PDRB"))

#rename provinsi di pulau jawa
gdp2016$Provinsi <- gdp2016$Provinsi %>%
    str_replace("Daerah Istimewa Yogyakarta", "Yogyakarta") %>%
    str_replace("Daerah Khusus Ibukota Jakarta", "Jakarta Raya") %>%
    str_replace("Daerah Khusus Ibu Kota Jakarta", "Jakarta Raya")

#filter hanya provinsi di pulau jawa
gdp2016 <- gdp2016 %>%
    filter(Provinsi %in% c('Jakarta Raya', 'Jawa Barat', 'Banten', 'Jawa Tengah', 'Yogyakarta', 'Jawa Timur'))

#rename nama daerah

gdp2016$Daerah <- gdp2016$Daerah  %>%
    str_replace("Kabupaten ", "") %>%
    str_replace("Kota Administrasi ", "") %>%
    str_replace("Administrasi ", "") %>%
    str_replace("Gunungkidul", "Gunung Kidul")
	

#join jawa2020 & gdp2016
join <- jawa2020 %>%
    inner_join(gdp2016, by = "Daerah")

#penyesuaian dengan data shp
join$Daerah <- join$Daerah %>%
    str_replace("Kota Cilegon", "Cilegon") %>%
    str_replace("Kota Tangerang Selatan", "Tangerang Selatan") %>%
    str_replace("Kota Depok", "Depok") %>%
    str_replace("Kota Cimahi", "Cimahi") %>%
    str_replace("Kota Banjar", "Banjar") %>%
    str_replace("Kota Salatiga", "Salatiga") %>%
    str_replace("Kota Surakarta", "Surakarta") %>%
    str_replace("Kota Batu", "Batu") %>%
    str_replace("Kota Surabaya", "Surabaya")
