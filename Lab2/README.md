Lab2
---
## Цель работы

1.  Развить практические навыки использования языка программирования R для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных пакета dplyr -- функции select(), filter(), mutate(), arrange(), group_by()

## Ход работы
> library(dplyr)

Присоединяю пакет: ‘dplyr’

Следующие объекты скрыты от ‘package:stats’:

    filter, lag

Следующие объекты скрыты от ‘package:base’:

    intersect, setdiff, setequal, union

Пакет ‘dplyr’ был собран под R версии 4.2.3 
## Ответы на вопросы

1.Сколько строк в датафрейме?
```
> starwars %>% nrow()
[1] 87
```
2.Сколько столбцов в датафрейме?
```
> starwars %>% ncol()
[1] 14
```
3.Как посмотреть примерный вид датафрейма?
> starwars %>% glimpse()
Rows: 87
Columns: 14
$ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "…
$ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188,…
$ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84…
$ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "br…
$ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "li…
$ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", …
$ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0,…
$ sex        <chr> "male", "none", "none", "male", "female", "male", "f…
$ gender     <chr> "masculine", "masculine", "masculine", "masculine", …
$ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Aldera…
$ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human"…
$ films      <list> <"The Empire Strikes Back", "Revenge of the Sith", …
$ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <…
$ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanc…
```
4.Сколько уникальных рас персонажей (species) представлено в данных?
```
> unique(starwars$species)
 [1] "Human"          "Droid"          "Wookiee"        "Rodian"        
 [5] "Hutt"           "Yoda's species" "Trandoshan"     "Mon Calamari"  
 [9] "Ewok"           "Sullustan"      "Neimodian"      "Gungan"        
[13] NA               "Toydarian"      "Dug"            "Zabrak"        
[17] "Twi'lek"        "Vulptereen"     "Xexto"          "Toong"         
[21] "Cerean"         "Nautolan"       "Tholothian"     "Iktotchi"      
[25] "Quermian"       "Kel Dor"        "Chagrian"       "Geonosian"     
[29] "Mirialan"       "Clawdite"       "Besalisk"       "Kaminoan"      
[33] "Aleena"         "Skakoan"        "Muun"           "Togruta"       
[37] "Kaleesh"        "Pau'an"  
```
5.Найти самого высокого персонажа.
```
> starwars |> slice_max(height)
A tibble: 1 × 14
  name      height  mass hair_color skin_color eye_color birth_year sex  
  <chr>      <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr>
1 Yarael P…    264    NA none       white      yellow            NA male 
```
6.Найти всех персонажей ниже 170.
```
> starwars |> filter(height < 170)
A tibble: 23 × 14
   name     height  mass hair_color skin_color eye_color birth_year sex  
   <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr>
 1 C-3PO       167    75 NA         gold       yellow           112 none 
 2 R2-D2        96    32 NA         white, bl… red               33 none 
 3 Leia Or…    150    49 brown      light      brown             19 fema…
 4 Beru Wh…    165    75 brown      light      blue              47 fema…
 5 R5-D4        97    32 NA         white, red red               NA none 
 6 Yoda         66    17 white      green      brown            896 male 
 7 Mon Mot…    150    NA auburn     fair       blue              48 fema…
 8 Wicket …     88    20 brown      brown      brown              8 male 
 9 Nien Nu…    160    68 none       grey       black             NA male 
10 Watto       137    NA black      blue, grey yellow            NA male 
13 more rows
```
7.Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать по формуле I = m/h2, где m -- масса (weight), а h -- рост (height).
```
> starwars %>% mutate("IMT" = mass/height*height)
A tibble: 87 × 15
   name     height  mass hair_color skin_color eye_color birth_year sex  
   <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr>
 1 Luke Sk…    172    77 blond      fair       blue            19   male 
 2 C-3PO       167    75 NA         gold       yellow         112   none 
 3 R2-D2        96    32 NA         white, bl… red             33   none 
 4 Darth V…    202   136 none       white      yellow          41.9 male 
 5 Leia Or…    150    49 brown      light      brown           19   fema…
 6 Owen La…    178   120 brown, gr… light      blue            52   male 
 7 Beru Wh…    165    75 brown      light      blue            47   fema…
 8 R5-D4        97    32 NA         white, red red             NA   none 
 9 Biggs D…    183    84 black      light      brown           24   male 
10 Obi-Wan…    182    77 auburn, w… fair       blue-gray       57   male 
77 more rows
```
8.Найти 10 самых "вытянутых" персонажей. "Вытянутость" оценить по отношению массы (mass) к росту (height) персонажей.
```
> starwars |> mutate("vitanytost" = mass/height) |> slice_max(vitanytost,n=10)
A tibble: 10 × 15
   name     height  mass hair_color skin_color eye_color birth_year sex  
   <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr>
 1 Jabba D…    175  1358 NA         green-tan… orange         600   herm…
 2 Grievous    216   159 none       brown, wh… green, y…       NA   male 
 3 IG-88       200   140 none       metal      red             15   none 
 4 Owen La…    178   120 brown, gr… light      blue            52   male 
 5 Darth V…    202   136 none       white      yellow          41.9 male 
 6 Jek Ton…    180   110 brown      fair       blue            NA   male 
 7 Bossk       190   113 none       green      red             53   male 
 8 Tarfful     234   136 brown      brown      blue            NA   male 
 9 Dexter …    198   102 none       brown      yellow          NA   male 
10 Chewbac…    228   112 brown      unknown    blue           200   male 
```
9.Найти средний возраст персонажей каждой расы вселенной Звездных войн.
```
> starwars %>%na.omit() %>%group_by(species) %>%summarise("MA" = mean(birth_year))
A tibble: 11 × 2
   species         MA
   <chr>        <dbl>
 1 Cerean        92  
 2 Ewok           8  
 3 Gungan        52  
 4 Human         45.5
 5 Kel Dor       22  
 6 Mirialan      49  
 7 Mon Calamari  41  
 8 Trandoshan    53  
 9 Twi'lek       48  
10 Wookiee      200  
11 Zabrak        54  
```
10.Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.
```
> starwars %>%group_by(eye_color) %>%summarise("BC" = n() ) %>%slice_max(BC)
A tibble: 1 × 2
  eye_color    BC
  <chr>     <int>
1 brown        21
```
11.Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.
```
> starwars %>%mutate("LN" = nchar(name)) %>%group_by(species) %>%summarise(mean(LN))
A tibble: 38 × 2
   species   `mean(LN)`
   <chr>          <dbl>
 1 Aleena         13   
 2 Besalisk       15   
 3 Cerean         12   
 4 Chagrian       10   
 5 Clawdite       10   
 6 Droid           4.83
 7 Dug             7   
 8 Ewok           21   
 9 Geonosian      17   
10 Gungan         11.7 
28 more rows

## Вывод

Научился пользоваться на практике функциями обработки данных пакета dplyr