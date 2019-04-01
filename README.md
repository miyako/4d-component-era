# 4d-component-era
西暦/和暦の変換メソッド

### Version

<img src="https://cloud.githubusercontent.com/assets/1725068/18940649/21945000-8645-11e6-86ed-4a0f800e5a73.png" width="32" height="32" /> <img src="https://cloud.githubusercontent.com/assets/1725068/18940648/2192ddba-8645-11e6-864d-6d5692d55717.png" width="32" height="32" />

---

### ポイント

日付の設定は外部``XML``ファイルで管理しており，カスタマイズすることができます。
標準XLIFFファイルなので，MEIJI, HEISEIなど，ローカライズもOKです。

**TODO**: スレッドセーフ（``Storage``）

* フォーマット

``EraList``:``明治;大正;昭和;平成;新元号``

``4``番目の元号は「平成」という意味です。

``EraSettings4``:``31;1988;1;8;3;31``

最高年は``31``であり，西暦に対するオフセットは``1988``，``1``月``8``日に始まり，``3``月``31``日に終わるという意味です。

* その他

明治は29日の閏月，13月の閏年が存在します。

明治45年7月30日の翌日は大正元年7月30日です。

``1``年は「元年」と変換されます。

```
  //西暦から和暦に変換する
C_TEXT($wareki)
C_LONGINT($era;$year;$month;$day)
$wareki:=ERA_Convert_from_date (!1989-01-01!;->$era;->$year;->$month;->$day)  //昭和64年1月1日
$wareki:=ERA_Convert_from_date (!1989-01-08!;->$era;->$year;->$month;->$day)  //平成元年1月8日
$wareki:=ERA_Convert_from_date (!2017-01-01!;->$era;->$year;->$month;->$day)  //平成29年1月1日
$wareki:=ERA_Convert_from_date (!2019-03-31!;->$era;->$year;->$month;->$day)  //平成31年3月31日
$wareki:=ERA_Convert_from_date (!2019-04-01!;->$era;->$year;->$month;->$day)  //平成31年4月1日
$wareki:=ERA_Convert_from_date (!2019-05-01!;->$era;->$year;->$month;->$day)  //令和元年5月1日
$wareki:=ERA_Convert_from_date (!2020-01-01!;->$era;->$year;->$month;->$day)  //令和2年1月1日
```

```
  //和暦から西暦に変換する
C_DATE($seireki)
$seireki:=ERA_Convert_to_date (3;64;1;7)  //89/01/07
$seireki:=ERA_Convert_to_date (4;31;3;31)  //19/03/31
$seireki:=ERA_Convert_to_date (5;1;4;1)  //19/04/01
$seireki:=ERA_Convert_to_date (1;45;7;30)  //1912/07/29
$seireki:=ERA_Convert_to_date (2;1;7;30)  //1912/07/30
```

* ポップアップメニュー・セットアップ用

```
  //平成（元号#4）の年リストを取得する（1~31）
ARRAY TEXT($years;0)
ERA_GET_YEAR_LIST (->$years;4)

  //平成（元号#4）31年の月リストを取得する（1~3）
ARRAY TEXT($months;0)
ERA_GET_MONTH_LIST (->$months;31;4)

  //平成（元号#4）1年の1月の日リストを取得する（8~31）
ARRAY TEXT($days;0)
ERA_GET_DAY_LIST (->$days;1;1;4)
```

* ポップアップメニュー・項目選択処理用

```
  //新元号（元号#5）1年1番目の月
$month_index:=ERA_Get_month_index (5;1;1)  //4
  //平成（元号#4）1年1月1番目の日
$day_index:=ERA_Get_day_index (4;1;1;1)  //8
```
