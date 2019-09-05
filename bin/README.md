# Преобразование CSV файлов в QHS файлы хранилища котировок и обратное преобразование

* *bat-файл download.bat* - скачать данные брокера Binary.com за последние 2 года (данные будут дозаписаны)
* *bat-файл date.bat* - узнать минимальную и максимальную дату котировок qhs4 файлов из папки storage
* *bat-файл build_csv.bat* - преобразует qhs4 файлы из папки storage в файлы csv с временной зоной GMT

Внимание! qhs4 файлы хранят котировки в GMT\UTC!

# Программы для работы с файлами котировок

## xqhtools.exe

*xqhtools.exe* - консольная программа для конвертации и слияния файлов котировок
Данная программа собрана при помощи компилятора *MinGW-w64* версии *7.3.0* [https://sourceforge.net/projects/mingw-w64/](https://sourceforge.net/projects/mingw-w64/)
Если на вашем компьютере нет необходимых dll файлов, их можно взять из архива с компилятором.

Команды:

* *merge* - (Не поддерживается на данный момент) слить файлы котировок вместе. Данная команда работает только с котировками в формате хранилища котировок qhs*
* *convert_csv* - конвертировать csv файлы. Данная команда подходит для конвертации csv файлов в набор hex файлов или в хранилище котировок qhs*
* *convert_storage* - конвертировать qhs* файлы. Данная команда конвертирует файлы qhs* в csv файлы
* *date* - узнать минимальную и максимальную дату котировок файла хранилища

Переменные:

* *path_hex* - путь к папке с файлами hex
* *path_csv* - путь к файлу котировок в формате csv
* *path_storage* - путь к файлу котировок в формате хранилища котировок qhs*
* *header* - заголовок csv файла (переменная нужна только для преобразования qhs* файлов в csv)

Флаги:

* *-cetgmt* - преобразовать время CET в GMT
* *-eetgmt* - преобразовать время EET в GMT
* *-gmtcet* - преобразовать время GMT в CET
* *-gmteet* - преобразовать время GMT в EET
* *-finam* - преобразовать время CET в GMT при конвертировании csv файлов 
* *-alpari* - преобразовать время EET в GMT или CET в GMT при конвертировании csv файлов (у ДЦ серверов Альпари с 01.05.2011 года время сервера поменялось с CET на EET)
* *-h* - прочитать заголовок csv файла. Не оказывает влияния
* *-oo* - использовать только цену открытия (open) бара или свечи. 
* *-oc* - использовать только цену закрытия (close) бара или свечи. 
* *-ohlc* - использовать 4 цены бара или свечи (open, high, low, close)
* *-ohlcv* - использовать 4 цены бара или свечи (open, high, low, close) и объем (volume)
* *-c* - использовать сжатие данных (только для преобразования csv в формат хранилища котировок qhs* или для слияния qhs* файлов)
* *-m4* - использовать преобразование qhs* файлов в csv формат для MetaTrader4
* *-m5* - использовать преобразование qhs* файлов в csv формат для MetaTrader5
* *-ducascopy* - использовать преобразование qhs* файлов в csv формат брокера Ducascopy
* *-sbc* - пропускать "плохие" бары во время преобразования qhs* файлов в csv. Плохие бары, это когда отсутствует цена за данную минуту
* *-fbc* - заполнять "плохие" бары во время преобразования qhs* файлов в csv. Заполнение будет происходить последней известной ценой
* *-wbc* - записывать "плохие" бары во время преобразования qhs* файлов в csv

### Пример использования

Преобразовать csv файл в qhs4 файл с использованием сжатия (флаг *-c*) и преобразованием времени из CET в GMT (флаг *-ohlc*):

```
xqhtools convert_csv path_storage ..\storage\AUDCAD path_csv ..\csv\AUDCAD1.csv -cetgmt -ohlc -c
```

Преобразовать qhs4 файл обратно в csv файл для MetaTrader4 с преобразованием GMT времени в CET (флаг *-gmtcet*) и пропуском плохих баров (*-sbc*)

```
xqhtools convert_storage path_storage ..\storage\AUDCAD.qhs4 path_csv ..\csv\AUDCAD1.csv -gmtcet -m4 -sbc
```
