# Car Plates OCR Competition

Репозиторий содержит код решения Kaggle InClass соревнования [Car plates OCR Competition](https://www.kaggle.com/c/car-plates-ocr-made), проходившего в рамках курса по компьютерному зрению в [Академии больших данных MADE](https://data.mail.ru).

Для каждого изображения необходимо было распознать все автомобильные номера.

Задача решается в два этапа: детекция номеров на изображении и распознавание текста на номерах.

### Детекция номеров
* Использовалась модель maskrcnn_resnet50_fpn.
* Опробованы размеры батча 2, 4 и 6 изображений (при 8 изображениях уже не хватало памяти), лучшее качество получилось при батчах размера 6.
* Модель обучалась 4 эпохи с валидацией на отложенной выборке 10 раз за эпоху.

### Распознавание текста на номерах
* Использовалась модель CRNN, состоящая из предобученной resnet18 и рекуррентной сети.
* В качестве рекуррентной сети опробованы GRU и LSTM, для которых подбирались следующие параметры: одно/двунаправленность, размер скрытого состояния, количество слоёв.
* На локальной валидации и публичном лидерборде практически одинаковые результаты показали две модели:
  * Двунаправленная GRU с двумя слоями и размером скрытого состояния 192.
  * Двунаправленная LSTM с тремя слоями и размером скрытого состояния 128.
  * Прогнозы этих двух моделей были выбраны в качестве финальных.
 
 ### Результат
 * 14-е место на Public LB.
 * 29-е место на Private LB.
 * Результат оказался для меня странным:
  * Достаточно быстро я смог реализовать локальную валидацию, качество на которой полностью совпадало с Public LB.
  * По этой причине я сделал мало посылок (7 за всё соревнования) – валидировал всё локально. Это означает, что переобучения под Public LB не было.
  * На Private LB модели показали качество хуже более, чем в 3 раза: 1.58407 и 1.62536 против 0.48227 и 0.48683 на Public LB.
