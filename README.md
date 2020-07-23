<p align='center'>
	<img src="https://i.ibb.co/P6HGqnf/receipt.png" width="450" title="Designed by Freepik">
<br><br>
</p>

# Receipt parser🧾

## What is it?
**receipt_parser** - Python библиотека, помогающая распознавать товарную позицию из чеков. Для это задачи есть хороший [сервис](https://receiptnlp.tinkoff.ru/#/) от Тинькофф, однако он не справляется с [грязными данными](https://proverkacheka.com/check/9282000100225162-17705-420231526), как на картинке выше. Изначально была задумка использовать нейронные сети, однако в процессе работы, понял, что на разметку нужно потратить много времени/денег, да и модель, основанная на правилах и словарях, даёт хороший [результат](https://github.com/slgero/receipt_parser/tree/master/receipt_parser/benchmarks).

## Features
* распознавание продукта;
* определение категории товара;
* распознавание брендов;
* перевод англицизмов (`хугарден --> hoegaarden`)🍺


## Where to get it
Исходный код в размещен на [GitHub](https://github.com/slgero/receipt_parser).

Библиотека размещёна на [Python package index](https://pypi.org/project/receipt-parser/):
```bash
pip install receipt-parser
```

## Usage
Для распознавания сейчас доступна только [RuleBased](https://github.com/slgero/receipt_parser/blob/master/receipt_parser/receipt_parser.py#L75) модель.

На вход можно подавать как строку:
```python
from receipt_parser import RuleBased

product_desription = 'Нап.пив.ХУГАР.ГРЕЙПФ.н/ф 0.47л'
rb = RuleBased()
rb.parse(product_desription)
```
 *output*:
|    | name                           | product_norm   | brand_norm   | cat_norm            |
|---:|:-------------------------------|:---------------|:-------------|:--------------------|
|  0 | Нап.пив.ХУГАР.ГРЕЙПФ.н/ф 0.47л | напиток, пиво  | hoegaarden   | Воды, соки, напитки |

Так и pd.DataFrame *(колонка с товарной позицией должна называться name)*:
```python
from receipt_parser import RuleBased

rb = RuleBased()
rb.parse(df)
```
Также в библиотеке есть два вспомогательных класса:
* Normalizer - для нормализации;
* Finder - для поиску по словарям.

## Future work

 - [ ] Добавить тесты
 - [ ] Дополнить словари собранные датасеты
 - [ ] Поднять сервис
 - [ ] Перейти на нейронные сети...

## Support the project 🤗
Буду рад, если вы:
* найдёте баги;
* сможете оптимизировать код;
* дополните словари и датасеты;
* поможете с разметкой.
