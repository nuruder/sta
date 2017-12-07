Основную документацию смотреть [здесь](https://confluence.hflabs.ru/pages/viewpage.action?pageId=592412676&src=sidebar)

Получить подсказки:

```js
<input id="address" name="address" type="text" size="100"/>
<link href="https://cdn.jsdelivr.net/npm/suggestions-jquery@17.10.1/dist/css/suggestions.min.css" type="text/css" rel="stylesheet" />
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<!--[if lt IE 10]>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery-ajaxtransport-xdomainrequest/1.0.1/jquery.xdomainrequest.min.js"></script>
<![endif]-->
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/suggestions-jquery@17.10.1/dist/js/jquery.suggestions.min.js"></script>
<script type="text/javascript">
    $("#address").suggestions({
        token: "TOKEN",
        type: "ADDRESS",
        count: 5,
        /* Вызывается, когда пользователь выбирает одну из подсказок */
        onSelect: function(suggestion) {
            console.log(suggestion);
        }
    });
</script>
```

curl с результатами подсказок \([подробно](https://confluence.hflabs.ru/display/SGTDOC1710/REST+API)\):

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "Authorization: Token TOKEN" \
  -d '{ "query": "Санкт-Петербург, Ждановская наб. 10", "count": 1 }' \
  https://suggestions.dadata.ru/suggestions/api/4_1/rs/suggest/address
```

**Что возвращается:**

| Название | Описание |
| :--- | :--- |
| value | Адрес одной строкой \(как показывается в списке подсказок\) |
| unrestricted\_value | Адрес одной строкой \(полный, от региона\) |
| data.postal\_code | Индекс |
| data.country | Страна |
| data.region\_fias\_id | Код ФИАС региона |
| data.region\_kladr\_id | Код КЛАДР региона |
| data.region\_with\_type | Регион с типом |
| data.region\_type | Тип региона \(сокращенный\) |
| data.region\_type\_full | Тип региона |
| data.region | Регион |
| data.area\_fias\_id | Код ФИАС района в регионе |
| data.area\_kladr\_id | Код КЛАДР района в регионе |
| data.area\_with\_type | Район в регионе с типом |
| data.area\_type | Тип района в регионе \(сокращенный\) |
| data.area\_type\_full | Тип района в регионе |
| data.area | Район в регионе |
| data.city\_fias\_id | Код ФИАС города |
| data.city\_kladr\_id | Код КЛАДР города |
| data.city\_with\_type | Город с типом |
| data.city\_type | Тип города \(сокращенный\) |
| data.city\_type\_full | Тип города |
| data.city | Город |
| data.city\_area | Административный округ \(только для Москвы\) |
| data.city\_district\_fias\_id | Код ФИАС района города |
| data.city\_district\_kladr\_id | Код КЛАДР района города |
| data.city\_district\_with\_type | Район города с типом |
| data.city\_district\_type | Тип района города \(сокращенный\) |
| data.city\_district\_type\_full | Тип района города |
| data.city\_district | Район города |
| data.settlement\_fias\_id | Код ФИАС нас. пункта |
| data.settlement\_kladr\_id | Код КЛАДР нас. пункта |
| data.settlement\_with\_type | Населенный пункт с типом |
| data.settlement\_type | Тип населенного пункта \(сокращенный\) |
| data.settlement\_type\_full | Тип населенного пункта |
| data.settlement | Населенный пункт |
| data.street\_fias\_id | Код ФИАС улицы |
| data.street\_kladr\_id | Код КЛАДР улицы |
| data.street\_with\_type | Улица с типом |
| data.street\_type | Тип улицы \(сокращенный\) |
| data.street\_type\_full | Тип улицы |
| data.street | Улица |
| data.house\_fias\_id | Код ФИАС дома |
| data.house\_kladr\_id | Код КЛАДР дома |
| data.house\_type | Тип дома \(сокращенный\) |
| data.house\_type\_full | Тип дома |
| data.house | Дом |
| data.block\_type | Тип корпуса/строения \(сокращенный\) |
| data.block\_type\_full | Тип корпуса/строения |
| data.block | Корпус/строение |
| data.flat\_type | Тип квартиры \(сокращенный\) |
| data.flat\_type\_full | Тип квартиры |
| data.flat | Квартира |
| data.flat\_area | Площадь квартиры \(не заполняется\) |
| data.square\_meter\_price | Рыночная стоимость м² \(не заполняется\) |
| data.flat\_price | Рыночная стоимость квартиры \(не заполняется\) |
| data.postal\_box | Абонентский ящик |
| data.history\_values | Исторические наименования объекта с типом \(только уникальные\) |
| data.fias\_id | Код ФИАС:`HOUSE.HOUSEGUID`, если дом найден в ФИАС по точному совпадению;`HOUSEINT.INTGUID`, если дом найден в ФИАС как часть интервала;`ADDROBJ.AOGUID` в противном случае. |
| data.fias\_level | Уровень детализации, до которого адрес найден в ФИАС: 0 — страна; 1 — регион; 3 — район; 4 — город; 6 — населенный пункт; 7 — улица; 8 — дом; -1 — иностранный или пустой. |
| data.kladr\_id | Код КЛАДР |
| data.capital\_marker | Является ли город центром:1 — центр района \(Московская обл, Одинцовский р-н, г Одинцово\) 2 — центр региона \(Новосибирская обл, г Новосибирск\); 3 — центр района и региона \(Костромская обл, Костромской р-н, г Кострома\); 4 — центральный район региона \(Тюменская обл, Тюменский р-н\); 0 — ни то, ни другое \(Московская обл, г Балашиха\). |
| data.okato | Код ОКАТО |
| data.oktmo | Код ОКТМО |
| data.tax\_office | Код ИФНС для физических лиц |
| data.tax\_office\_legal | Код ИФНС для организаций \(не заполняется\) |
| data.timezone | Часовой пояс \(не заполняется\) |
| data.geo\_lat | Координаты: широта |
| data.geo\_lon | Координаты: долгота |
| data.beltway\_hit | Внутри кольцевой? \(не заполняется\) |
| data.beltway\_distance | Расстояние от кольцевой в км \(не заполняется\) |
| data.metro | Ближайшие станции метро \(не более 3 станций в радиусе 5 км\): |
| data.metro.name | наименование станции |
| data.metro.line | ветка метро |
| data.metro.distance | расстояние до станции |
| data.qc\_geo | Код точности координат: 0 — Точные координаты 1—Ближайший дом 2—Улица 3—Населенный пункт 4—Город 5—Координаты не определены |
| data.qc\_complete | Код пригодности к рассылке \(не заполняется\) |
| data.qc\_house | Код проверки дома \(не заполняется\) |
| data.qc | Код проверки \(не заполняется\) |
| data.source | Исходный адрес, как его указал человек. Для организаций — адрес как в ЕГРЮЛ. |
| data.unparsed\_parts | Нераспознанная часть адреса \(не заполняется\) |

Гранулярные подсказки:

* отдельно регион, город, улица и дом - [https://codepen.io/dadata/pen/cGkah?editors=1010](https://codepen.io/dadata/pen/cGkah?editors=1010)
* отдельно город и улица - [http://codepen.io/dadata/pen/VLPZgG?editors=1010](http://codepen.io/dadata/pen/VLPZgG?editors=1010)
* отдельно все поля - [http://codepen.io/dadata/pen/ONNjJq?editors=1010](http://codepen.io/dadata/pen/ONNjJq?editors=1010)

Разложить адрес по полям - [http://codepen.io/dadata/pen/wajbh?editors=1010](http://codepen.io/dadata/pen/wajbh?editors=1010)

Показывать адрес внутри области \(города\) - [http://codepen.io/dadata/pen/qADdb?editors=1010](http://codepen.io/dadata/pen/qADdb?editors=1010)

Показывать только город и населенные пункты - [http://codepen.io/dadata/pen/aOxzVg?editors=1010](http://codepen.io/dadata/pen/aOxzVg?editors=1010)

Показывать только город - [http://codepen.io/dadata/pen/HIBem?editors=1010](http://codepen.io/dadata/pen/HIBem?editors=1010)



ФИАС - федеральная государственная информационная система, обеспечивающая формирование, ведение и использование государственного адресного реестра

Поля`city_district`,`city_area`,`flat_area`,`flat_price`,`timezone`,`metro`,`geo_*`,`beltway_*`заполняются после того, как пользователь выбрал конкретный адрес из подсказок. До этого они пустые.

Поля`qc_complete`,`qc_house`,`qc`и`unparsed_parts`не заполняются вообще. Они зарезервированы для автоматической обработки адресов через API стандартизации.

Количество запросов в день — в соответствии с тарифным планом.

Длина запроса — не более 300 символов.

Количество условий \(параметр`locations`\) — не более 100.











