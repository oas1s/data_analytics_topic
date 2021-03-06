# Фасхутдинов Азат 11-806 описание статьи

Мое повествование будет про нейронные сети в сфере медицины. Я буду говорить про проект названный **MIScnn**. Что же такое MIScnn? 

Являясь библиотекой Python с открытым исходным кодом MIScnn -это интуитивно понятный API, позволяющий быстро настраивать конвейеры сегментации медицинских изображений с помощью современных сверточных нейронных сетей и моделей глубокого обучения.

MIScnn предоставляет несколько основных функций:
* Сегментация медицинских изображений 2D/3D для бинарных и многоклассовых задач
* Ввод-вывод данных, предварительная обработка и увеличение данных для биомедицинских изображений
* Патч-анализ и полный анализ изображений
* Современная модель глубокого обучения и метрическая библиотека
* Интуитивно понятное и быстрое использование модели (обучение, прогнозирование)
* Несколько методов автоматической оценки (например, перекрестная проверка)
* Пользовательская модель, ввод-вывод данных, предварительная/постобработка и поддержка метрик

На основе Keras с Tensorflow в качестве бэкенда.

Ниже представлена **архитектура** MIScnn
![alt tag](https://github.com/frankkramer-lab/MIScnn/raw/b49f07e87528737579fb566cf09073ae81be6747/docs/MIScnn.pipeline.png)

**Эксперементы и результаты**:
Задача задачи сегментации опухоли почки 2019 (KITS19) состояла в том, чтобы вычислить семантическую сегментацию артериальной фазы КТ брюшной полости у 300 пациентов с раком почки. Каждый пиксель должен был быть помечен в один из трех классов: фон, почка или опухоль. Исходные сканы имеют разрешение изображения 512x512 и в среднем 216 срезов (самый высокий номер среза-1059).

MIScnn был использован в обучающем наборе данных KITS19 для выполнения 3-кратной перекрестной проверки с помощью 3D - стандартной модели U-Net.

MIScnn показал хорошие результаты, отчеты по проведению эксперемента были опубликованы в офицальном репозитории на GitHub: 
https://github.com/frankkramer-lab/MIScnn/blob/master/examples/KiTS19.ipynb

![alt tag](https://github.com/frankkramer-lab/MIScnn/raw/b49f07e87528737579fb566cf09073ae81be6747/docs/visualization.case_case_00044.gif)

MIScnn использует по умолчанию **U-net** сверточную нейронную сеть.

**U-Net** — это свёрточная нейронная сеть, которая была создана в 2015 году для сегментации биомедицинских изображений в отделении Computer Science Фрайбургского университета . Архитектура сети представляет собой полносвязную свёрточную сеть, модифицированную так, чтобы она могла работать с меньшим количеством примеров (обучающих образов) и делала более точную сегментацию.
**Архитектура U-Net**:
Сеть содержит сверточную (слева) и разверточную части (справа), поэтому архитектура похожа на букву U, что и отражено в названии. На каждом шаге мы удваиваем количество каналов признаков.
Сверточная часть похожа на обычную свёрточную сеть, он содержит два подряд свёрточных слоя 3x3, после которых идет слой ReLU и пулинг с функцией максимума 2×2 с шагом 2.
Каждый шаг разверточной части содержит слой, обратный пулингу, который расширяет карту признаков, после которого следует свертка 2x2, которая уменьшает количество каналов признаков. После идет конкатенация с соответствующим образом обрезанной картой признаков из сжимающего пути и две свертки 3x3, после каждой из которой идет ReLU. Обрезка нужна из-за того, что мы теряем пограничные пиксели в каждой свёртке. На последнем слое свертка 1x1 используется для приведения каждого 64-компонентного вектора признаков до требуемого количества классов.
Всего сеть имеет 23 свёрточных слоя.
Две статьи авторов сети имеют более 1600 и 1000 цитирований на май 2018 года.

Также отличительной чертой MIScnn является то, что он легко кастомизируется. Если это необходимо, пользователь сам может задать по какой модели он будет обучать нейронную сеть, задать количество эпох, слоев итд.

Создателем продукта является Dominik Müller аспирант кафедры медицинской информатики немецкого Университета Аугсбурга.
GitHub:https://github.com/frankkramer-lab/MIScnn/tree/master

