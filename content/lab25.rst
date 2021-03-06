Машинное обучение (Machine Learning)
####################################

:date: 2020-04-23 09:00
:summary: Классические методы машинного обучения, ч.1
:status: draft

.. default-role:: code

.. contents:: Содержание

.. role:: python(code)
   :language: python

**Запись онлайн-занятия:** https://youtu.be/IKaxaE0fKNc

Машинное обучение (Machine Learning) — обширный подраздел искусственного
интеллекта, изучающий методы построения алгоритмов, способных обучаться.

Общая постановка задачи обучения по прецедентам
-----------------------------------------------

Дано конечное множество прецедентов (объектов, ситуаций), по каждому из
которых собраны (измерены) некоторые данные. Данные о прецеденте
называют также его описанием. Совокупность всех имеющихся описаний
прецедентов называется обучающей выборкой. Требуется по этим частным
данным выявить общие зависимости, закономерности, взаимосвязи, присущие
не только этой конкретной выборке, но вообще всем прецедентам, в том
числе тем, которые ещё не наблюдались. Говорят также о восстановлении
зависимостей по эмпирическим данным — этот термин был введён в работах
Вапника и Червоненкиса.

Наиболее распространённым способом описания прецедентов является
признаковое описание. Фиксируется совокупность n показателей, измеряемых
у всех прецедентов. Если все n показателей числовые, то признаковые
описания представляют собой числовые векторы размерности n. Возможны и
более сложные случаи, когда прецеденты описываются временными рядами или
сигналами, изображениями, видеорядами, текстами, попарными отношениями
сходства или интенсивности взаимодействия, и т. д.

Для решения задачи обучения по прецедентам в первую очередь фиксируется
модель восстанавливаемой зависимости. Затем вводится функционал
качества, значение которого показывает, насколько хорошо модель
описывает наблюдаемые данные. Алгоритм обучения (learning algorithm)
ищет такой набор параметров модели, при котором функционал качества на
заданной обучающей выборке принимает оптимальное значение. Процесс
настройки (fitting) модели по выборке данных в большинстве случаев
сводится к применению численных методов оптимизации.


Типы задач Машинного обучения
-----------------------------

-  классификация – отнесение объекта к одной из категорий на основании
   его признаков
-  регрессия – прогнозирование количественного признака объекта на
   основании прочих его признаков
-  кластеризация – разбиение множества объектов на группы на основании
   признаков этих объектов так, чтобы внутри групп объекты были похожи
   между собой, а вне одной группы – менее похожи
-  детекция аномалий – поиск объектов, “сильно непохожих” на все
   остальные в выборке либо на какую-то группу объектов
-  и много-много других, более специфичных.

Обучение с учителем и без учителя
---------------------------------

В зависимости от данных алгоритмы машинного обучения могут быть поделены
на те, что обучаются с учителем и без учителя (supervised & unsupervised
learning). В задачах обучения без учителя имеется выборка, состоящая из
объектов, описываемых набором признаков. В задачах обучения с учителем
вдобавок к этому для каждого объекта некоторой выборки, называемой
обучающей, известен целевой признак – по сути это то, что хотелось бы
прогнозировать для прочих объектов, не из обучающей выборки. **Т.е в
задачах МО с учителем на обучающей выборке у нас есть “правильные”
ответы, а когда задача без учителя - то нет**

Пример
~~~~~~

Задачи классификации и регрессии – это задачи обучения с учителем. В
качестве примера будем представлять задачу кредитного скоринга: на
основе накопленных кредитной организацией данных о своих клиентах
хочется прогнозировать невозврат кредита. Здесь для алгоритма данные –
это имеющаяся обучающая выборка: набор объектов (людей), каждый из
которых характеризуется набором признаков (таких как возраст, зарплата,
тип кредита, невозвраты в прошлом и т.д.), а также целевым признаком.
Если этот целевой признак – просто факт невозврата кредита (1 или 0,
т.е. банк знает о своих клиентах, кто вернул кредит, а кто – нет), то
это задача (бинарной) классификации. Если известно, на сколько по
времени клиент затянул с возвратом кредита и хочется то же самое
прогнозировать для новых клиентов, то это будет задачей регрессии.

Метрики качества
----------------

Наконец, третья абстракция в машинном обучении – это метрика оценки
производительности алгоритмов. Такие метрики различаются для разных
задач и алгоритмов. Пока скажем, что самая простая метрика качества
алгоритма, решающего задачу классификации – это доля правильных ответов
(accuracy, не называйте ее точностью, этот перевод зарезервирован под
другую метрику, precision) – то есть попросту доля верных прогнозов
алгоритма на тестовой выборке.

**На паре вам более подробно расскажут о классификации задач машинного
обучения, метриках**

Задача Классификации
--------------------

Начнем с задач Классификации, хотя зачастую эти задачи можно свести к
задаче регрессии

k-NN
~~~~

Заметим одно житейское наблюдение: обычно схожие объекты лежат гораздо
чаще лежат в одном классе, чем в разных. Это свойство называется
гипотезой компактности и все *метрические методы* опираются на нее.

Более строго Гипотеза компактности формулируется так: если мера сходства
объектов введена достаточно удачно, то схожие объекты гораздо чаще лежат
в одном классе, чем в разных. В этом случае граница между классами имеет
достаточно простую форму, а классы образуют компактно локализованные
области в пространстве объектов.

Пусть мы каким то образом можем измерять расстояние между объектами, т.е
у нас задана функция расстояний (метрика, не путайте с метрикой
качества!) на пространстве признаков.

**Метод ближайшего соседа** является, пожалуй, самым простым алгоритмом
классификации. Классифицируемый объект :math:`x` относится к тому классу
:math:`y_i`, которому принадлежит ближайший объект обучающей выборки
:math:`x_i`.

**Метод k ближайших соседей**. Для повышения надёжности классификации
объект относится к тому классу, которому принадлежит большинство из его
соседей — :math:`k` ближайших к нему объектов обучающей выборки
:math:`x_i`. В задачах с двумя классами число соседей берут нечётным,
чтобы не возникало ситуаций неоднозначности, когда одинаковое число
соседей принадлежат разным классам.

**Метод взвешенных ближайших соседей**. В задачах с числом классов 3 и
более нечётность уже не помогает, и ситуации неоднозначности всё равно
могут возникать. Тогда i-му соседу приписывается вес :math:`w_i`, как
правило, убывающий с ростом ранга соседа i. Объект относится к тому
классу, который набирает больший суммарный вес среди k ближайших
соседей.

В чистом виде kNN может послужить хорошим стартом (baseline) в решении
какой-либо задачи; В соревнованиях Kaggle kNN часто используется для
построения мета-признаков (прогноз kNN подается на вход прочим моделям)
или в стекинге/блендинге; Идея ближайшего соседа расширяется и на другие
задачи, например, в рекомендательных системах простым начальным решением
может быть рекомендация какого-то товара (или услуги), популярного среди
ближайших соседей человека, которому хотим сделать рекомендацию;


Плюсы и минусы метода ближайших соседей
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Плюсы:

-  Простая реализация;
-  Неплохо изучен теоретически;
-  Как правило, метод хорош для первого решения задачи, причем не только
   классификации или регрессии, но и, например, рекомендации;
-  Можно адаптировать под нужную задачу выбором метрики или ядра (в двух
   словах: ядро может задавать операцию сходства для сложных объектов
   типа графов, а сам подход kNN остается тем же). Кстати, профессор ВМК
   МГУ и опытный участник соревнований по анализу данных Александр
   Дьяконов любит самый простой kNN, но с настроенной метрикой сходства
   объектов.
-  Неплохая интерпретация, можно объяснить, почему тестовый пример был
   классифицирован именно так. Хотя этот аргумент можно атаковать: если
   число соседей большое, то интерпретация ухудшается (условно: “мы не
   дали ему кредит, потому что он похож на 350 клиентов, из которых 70 –
   плохие, что на 12% больше, чем в среднем по выборке”).

Минусы:

-  Метод считается быстрым в сравнении, например, с композициями
   алгоритмов, но в реальных задачах, как правило, число соседей,
   используемых для классификации, будет большим (100-150), и в таком
   случае алгоритм будет работать не так быстро, как дерево решений;
-  Если в наборе данных много признаков, то трудно подобрать подходящие
   веса и определить, какие признаки не важны для
   классификации/регрессии;
-  Зависимость от выбранной метрики расстояния между примерами. Выбор по
   умолчанию евклидового расстояния чаще всего ничем не обоснован. Можно
   отыскать хорошее решение перебором параметров, но для большого набора
   данных это отнимает много времени;
-  Нет теоретических оснований выбора определенного числа соседей —
   только перебор (впрочем, чаще всего это верно для всех
   гиперпараметров всех моделей). В случае малого числа соседей метод
   чувствителен к выбросам, то есть склонен переобучаться;
-  Как правило, плохо работает, когда признаков много, из-за “прояклятия
   размерности”. Про это хорошо рассказывает известный в ML-сообществе
   профессор Pedro Domingos – тут в популярной статье “A Few Useful
   Things to Know about Machine Learning”, также “the curse of
   dimensionality” описывается в книге Deep Learning в главе “Machine
   Learning basics”.

Класс KNeighborsClassifier в Scikit-learn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

sklearn.neighbors.KNeighborsClassifier: \* weights: “uniform” (все веса
равны), “distance” (вес обратно пропорционален расстоянию до тестового
примера) или другая определенная пользователем функция

-  algorithm (опционально): “brute”, “ball_tree”, “KD_tree”, или “auto”.
   В первом случае ближайшие соседи для каждого тестового примера
   считаются перебором обучающей выборки. Во втором и третьем —
   расстояние между примерами хранятся в дереве, что ускоряет нахождение
   ближайших соседей. В случае указания параметра “auto” подходящий
   способ нахождения соседей будет выбран автоматически на основе
   обучающей выборки.
-  leaf_size (опционально): порог переключения на полный перебор в
   случае выбора BallTree или KDTree для нахождения соседей
-  metric: “minkowski”, “manhattan”, “euclidean”, “chebyshev” и другие

Дерево решений
--------------

Деревья решений используются в повседневной жизни в самых разных
областях человеческой деятельности, порой и очень далеких от машинного
обучения. Деревом решений можно назвать наглядную инструкцию, что делать
в какой ситуации. Приведем пример из области консультирования научных
сотрудников института. Высшая Школа Экономики выпускает инфо-схемы,
облегчающие жизнь своим сотрудникам. Вот фрагмент инструкции по
публикации научной статьи на портале института.

.. image:: ../images/lab23/tree_article.png
   :width: 900px
   :height: 550px

В терминах машинного обучения можно сказать, что это элементарный
классификатор, который определяет форму публикации на портале (книга,
статья, глава книги, препринт, публикация в “НИУ ВШЭ и СМИ”) по
нескольким признакам: типу публикации (монография, брошюра, статья и
т.д.), типу издания, где опубликована статья (научный журнал, сборник
трудов и т.д.) и остальным.

.. image:: ../images/lab23/Кредит_дерево.png
   :width: 900px
   :height: 550px

Построение дерева
~~~~~~~~~~~~~~~~~

Алгоритм построения дерева

В основе популярных алгоритмов построения дерева решений лежит принцип
жадной максимизации прироста информации – на каждом шаге выбирается тот
признак, при разделении по которому прирост информации оказывается
наибольшим. Дальше процедура повторяется рекурсивно, пока энтропия не
окажется равной нулю или какой-то малой величине (если дерево не
подгоняется идеально под обучающую выборку во избежание переобучения). В
разных алгоритмах применяются разные эвристики для “ранней остановки”
или “отсечения”, чтобы избежать построения переобученного дерева.

.. code-block:: python

   def build(L):
       create node t
       if the stopping criterion is True:
           assign a predictive model to t
       else:
           Find the best binary split L = L_left + L_right
           t.left = build(L_left)
           t.right = build(L_right)
       return t  

**На семинаре вам расскажут как именно выбирается признак, по которому
производить разбиение, об энтропии, информации и других понятиях, на
которых строится математическое понимание работы Деревьев**

Основные параметры дерева
~~~~~~~~~~~~~~~~~~~~~~~~~

В принципе дерево решений можно построить до такой глубины, чтоб в
каждом листе был ровно один объект. Но на практике это не делается (если
строится только одно дерево) из-за того, что такое дерево будет
переобученным – оно слишком настроится на обучающую выборку и будет
плохо работать на прогноз на новых данных. Где-то внизу дерева, на
большой глубине будут появляться разбиения по менее важным признакам
(например, приехал ли клиент из Саратова или Костромы). Если утрировать,
может оказаться так, что из всех 4 клиентов, пришедших в банк за
кредитом в зеленых штанах, никто не вернул кредит. Но мы не хотим, чтобы
наша модель классификации порождала такие специфичные правила.

Есть два исключения, ситуации, когда деревья строятся до максимальной
глубины:

Случайный лес (композиция многих деревьев) усредняет ответы деревьев,
построенных до максимальной глубины (почему стоит делать именно так,
разберемся позже) Стрижка дерева (pruning). При таком подходе дерево
сначала строится до максимальной глубины, потом постепенно, снизу вверх,
некоторые вершины дерева убираются за счет сравнения по качеству дерева
с данным разбиением и без него (сравнение проводится с помощью
кросс-валидации, о которой чуть ниже). Подробнее можно почитать в
материалах репозитория Евгения Соколова.

Плюсы и минусы деревьев решений
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Плюсы:

-  Порождение четких правил классификации, понятных человеку, например,
   “если возраст < 25 и интерес к мотоциклам, то отказать в кредите”.
   Это свойство называют интерпретируемостью модели;
-  Деревья решений могут легко визуализироваться, то есть может
   “интерпретироваться” (строгого определения я не видел) как сама
   модель (дерево), так и прогноз для отдельного взятого тестового
   объекта (путь в дереве);
-  Быстрые процессы обучения и прогнозирования;
-  Малое число параметров модели;
-  Поддержка и числовых, и категориальных признаков.

Минусы:

-  У порождения четких правил классификации есть и другая сторона:
   деревья очень чувствительны к шумам во входных данных, вся модель
   может кардинально измениться, если немного изменится обучающая
   выборка (например, если убрать один из признаков или добавить
   несколько объектов), поэтому и правила классификации могут сильно
   изменяться, что ухудшает интерпретируемость модели;
-  Разделяющая граница, построенная деревом решений, имеет свои
   ограничения (состоит из гиперплоскостей, перпендикулярных какой-то из
   координатной оси), и на практике дерево решений по качеству
   классификации уступает некоторым другим методам;
-  Необходимость отсекать ветви дерева (pruning) или устанавливать
   минимальное число элементов в листьях дерева или максимальную глубину
   дерева для борьбы с переобучением. Впрочем, переобучение — проблема
   всех методов машинного обучения;
-  Нестабильность. Небольшие изменения в данных могут существенно
   изменять построенное дерево решений. С этой проблемой борются с
   помощью ансамблей деревьев решений (рассмотрим далее);
-  Проблема поиска оптимального дерева решений (минимального по размеру
   и способного без ошибок классифицировать выборку) NP-полна, поэтому
   на практике используются эвристики типа жадного поиска признака с
   максимальным приростом информации, которые не гарантируют нахождения
   глобально оптимального дерева;
-  Сложно поддерживаются пропуски в данных.
-  Модель умеет только интерполировать, но не экстраполировать (это же
   верно и для леса и бустинга на деревьях). То есть дерево решений
   делает константный прогноз для объектов, находящихся в признаковом
   пространстве вне параллелепипеда, охватывающего все объекты обучающей
   выборки. В нашем примере с желтыми и синими шариками это значит, что
   модель дает одинаковый прогноз для всех шариков с координатой > 19
   или < 0.

Класс DecisionTreeClassifier в Scikit-learn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Основные параметры класса sklearn.tree.DecisionTreeClassifier:

max_depth – максимальная глубина дерева max_features — максимальное
число признаков, по которым ищется лучшее разбиение в дереве (это нужно
потому, что при большом количестве признаков будет “дорого” искать
лучшее (по критерию типа прироста информации) разбиение среди всех
признаков) min_samples_leaf – минимальное число объектов в листе. У
этого параметра есть понятная интерпретация: скажем, если он равен 5, то
дерево будет порождать только те классифицирующие правила, которые верны
как минимум для 5 объектов

Параметры дерева надо настраивать в зависимости от входных данных, и
делается это обычно с помощью **кросс-валидации**, про нее чуть ниже.

Выбор параметров модели и кросс-валидация
-----------------------------------------

Главная задача обучаемых алгоритмов – их способность обобщаться, то есть
хорошо работать на новых данных. Поскольку на новых данных мы сразу не
можем проверить качество построенной модели (нам ведь надо для них
сделать прогноз, то есть истинных значений целевого признака мы для них
не знаем), то надо пожертвовать небольшой порцией данных, чтоб на ней
проверить качество модели.

.. image:: ../images/lab23/CV_pic.png
   :width: 900px
   :height: 550px

Чаще всего это делается одним из 2 способов: \* отложенная выборка
(held-out/hold-out set). При таком подходе мы оставляем какую-то долю
обучающей выборки (как правило от 20% до 40%), обучаем модель на
остальных данных (60-80% исходной выборки) и считаем некоторую метрику
качества модели (например, самое простое – долю правильных ответов в
задаче классификации) на отложенной выборке. \* кросс-валидация
(cross-validation, на русский еще переводят как скользящий или
перекрестный контроль). Тут самый частый случай – K-fold
кросс-валидация.

Тут модель обучается K раз на разных (K-1) подвыборках исходной выборки
(белый цвет), а проверяется на одной подвыборке (каждый раз на разной,
оранжевый цвет). Получаются K оценок качества модели, которые обычно
усредняются, выдавая среднюю оценку качества классификации/регрессии на
кросс-валидации.

Кросс-валидация дает лучшую по сравнению с отложенной выборкой оценку
качества модели на новых данных. Но кросс-валидация вычислительно
дорогостоящая, если данных много.

Кросс-валидация – очень важная техника в машинном обучении (применяемая
также в статистике и эконометрике), с ее помощью выбираются
гиперпараметры моделей, сравниваются модели между собой, оценивается
полезность новых признаков в задаче и т.д.

Задание (на это и следующее занятие):
-------------------------------------
Notebook_ 

.. _Notebook: {static}/extra/lab23/LABML1.ipynb
