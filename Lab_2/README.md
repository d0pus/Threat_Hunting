# Введение в R
 
 
## Цель работы 
 
  1. Развить практические навыки использования языка программирования R для
обработки данных
  2. Развить навыки работы в Rstudio IDE:
      установка пакетов
      работа с проектами в Rstudio
      настройка и работа с Git
  3. Закрепить знания базовых типов данных языка R и простейших операций с ними
  
## Исходные данные 
 
1.  Windows 10

2.  Rstudio Version: 2024.09.1+394

3.  R-4.4.2 for Windows

## План

1. Установить программный пакет dplyr
2. Проанализировать встроенный в пакет dplyr набор данных starwars с помощью языка R
3. Выполнить задания и оформить отчет
 
## Шаги

1.  Для начала прохождения курса необходимо установить программный пакет dplyr.
    ```         
    install.packages("dplyr")
    ```
2. Выполнение заданий:

2.1 Сколько строк в датафрейме?
```{r}
starwars %>% nrow()
```
2.2 Сколько столбцов в датафрейме?
```{r}
starwars %>% ncol()
```
2.3 Как просмотреть примерный вид датафрейма?
```{r}
starwars %>% glimpse()
```
  2.4 Сколько уникальных рас персонажей (species) представлено в данных?
```{r}
starwars %>% distinct(species)
```
2.5 Найти самого высокого персонажа.
```{r}
starwars %>% arrange(desc(height)) %>% head(1) %>% select(name)
```
2.6 Найти всех персонажей ниже 170.
```{r}
starwars %>% filter(!is.na(height) & height < 170) %>% select(name,height)
```
2.7 Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать по формуле.
```{r}
starwars %>% filter(!is.na(mass) & !is.na(height)) %>% mutate(bmi = mass / (height/100)^2) %>% select(name,bmi)
```
2.8 Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей.
```{r}
starwars %>% filter(!is.na(height) & !is.na(mass)) %>% mutate(stretch = mass / height) %>% arrange(desc(stretch)) %>% slice(1:10) %>% select(name,stretch)
```
2.9 Найти средний возраст персонажей каждой расы вселенной Звездных войн.
```{r}
starwars %>% filter(!is.na(species) & !is.na(birth_year)) %>% group_by(species) %>% summarise(average_age = mean(birth_year, na.rm = TRUE))
```
2.10 Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.
```{r}
starwars %>% filter(!is.na(eye_color)) %>% group_by(eye_color) %>% summarise(count = n()) %>% arrange(desc(count)) %>% slice(1)
```
2.11 Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.
```{r}
starwars %>% filter(!is.na(species) & !is.na(name)) %>% mutate(name_length = nchar(name)) %>% group_by(species) %>% summarise(len = mean(name_length, na.rm = TRUE))
```
    
## Оценка результата
  
В ходе выполнения практической работы был установлена пакет dplyr, а также выполнены задания по датасету starwars.
 
## Вывод 

Так, мною были изучены инструменты обработки данных пакета dplyr.
