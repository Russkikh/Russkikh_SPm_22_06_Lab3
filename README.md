# Russkikh_SPm_22_06_Lab3
## Комп'ютерні системи імітаційного моделювання
## СПм-22-6, **Рускix Олександр Валерійович**
### Лабораторна робота №**3**. Використання засобів обчислювального iнтелекту для оптимізації імітаційних моделей

<br>

### Варіант 6, модель у середовищі NetLogo:
[Rabbits Grass Weeds](http://www.netlogoweb.org/launch#http://www.netlogoweb.org/assets/modelslib/Sample%20Models/Biology/Rabbits%20Grass%20Weeds.nlogo)

<br>

### Вербальний опис моделі:
Цей проект досліджує просту екосистему, що складається з кроликів, трави та бур’янів. Кролики безладно блукають, а трава та бур’яни безладно ростуть. Коли кролик натикається на траву або бур’ян, він їсть траву і отримує енергію. Якщо кролик отримує достатньо енергії, він розмножується. Якщо він не отримує достатньо енергії, він гине.

Траву та бур’яни можна налаштувати так, щоб вони росли з різною швидкістю та давали кроликам різну кількість енергії. Модель можна використовувати для дослідження конкурентних переваг цих змінних.

### Керуючі параметри:
- **model speed**. Управління швидкістю моделювання.
- **number**. Початкова кілкість кроликів.
- **birth threshold**. Поріг народження, мінімальна кількість осіб необхідних для продовження популяції
- **grass-grow-rate**. Швидкість росту трави
-  **grass-energy**. Енергетична поживність трави
-  **weeds-grow-rate**. Швидкість росту бур’янів
-  **weeds-energy**.  Енергетична поживність бур’янів

### Внутрішні параметри:
- **move**. Переміщення кроликів.
- **eat-grass**. Їсти траву.
- **eat-weeds**. Їсти бур’ян.
- **reproduce**. Розмножуватися.
- **death**. Смерть.

### Показники роботи системи:
- максимальна кількість кроликів на поточному такті симуляції за заданих початкових умов: популяція, поживна енергетична цінність трави та бур'янів
- вплив на популяцію кроликів поживної енергетичної цінністі трави та бур'янів

### Примітки:
При початковому налаштуванні системи не враховується швидкість зростання та поживна енергія бур'янів

### Недоліки моделі:
Недолік системи в тому, що вона не враховує впливу навколишнього середовища, як, наприклад, хижаки (вовки чи лисиці), вплив температури на розмноження, смерть кроликів від хвороб тощо, чисельність і швидкість розмноження кроликів.

### Налаштування середовища BehaviorSearch:
**Обрана модель**:
<pre>
C:\Program Files\NetLogo 6.4.0\models\Sample Models\Biology\Rabbits Grass Weeds.nlogo
</pre>

**Параметри моделі** (вкладка Model):  
*Параметри та їх модливі діапазони були **автоматично** вилучені середовищем BehaviorSearch із вибраної імітаційної моделі, для цього є кнопка «Завантажити діапазони параметрів із інтерфейсу моделі»*:

*Параметри та їх модливі діапазони були **автоматично** вилучені середовищем BehaviorSearch із вибраної імітаційної моделі, для цього є кнопка «Завантажити діапазони параметрів із інтерфейсу моделі»*:
<pre>
["grass-grow-rate" [0 1 20]]
["weeds-grow-rate" [0 1 20]]
["grass-energy" [0 0.5 10]]
["weed-energy" [0 0.5 10]]
["number" [0 1 500]]
["birth-threshold" [0 1 20]]
</pre>

Використовувана **міра**:  
Для фітнес-функції *(вона ж функція пристосованості або цільова функція)* було обрано **максимальна кількість кроликів**, вираз для її розрахунку взято з налаштувань графіка аналізованої імітаційної моделі в середовищі NetLogo  

![Вкладка налаштувань параметрів моделі](measure.png)

та вказано у параметрі "**Measure**":
<pre>
count rabbits
</pre>
Максимальна кілбькість кролів за весь період симуляції тривалістю, *для приклада*, 200 тактів (адже на кожному такті є своє значення максимальної кількості кролів), починаючи з 0 такту симуляції.  

*Параметр "**Mesure if**" зі значення true, по суті, і означає, що враховуватимуться всі такти симуляції, а чи не частина їх. Іноді має сенс не враховувати деякі такти через хаос в деяких моделях на початку їх використання. Наприклад, це показано в прикладі з документації BehaviorSearch.  
Параметри "**Setup**" та "**Go**" вказують відповідні процедури ініціалізації та запуску в логіці моделі (зазвичай вони так і називаються). BehaviorSearch в процесі роботи, по суті, замість користувача запускає ці процедури.*  
Параметр зупинки за умовою ("**Stop if**") у разі не використовувався.  
Загальний вигляд вкладки налаштувань параметрів моделі:  

![Вкладка налаштувань параметрів моделі](parameters.png)

**Налаштування цільової функції** (вкладка Search Objective):  
Метою підбору параметрів імітаційної моделі, що описує дорожній рух двосмуговим шосе, є **максимізація** значення середньої швидкості машин на трасі – це вказано через параметр "**Goal**" зі значенням **Maximize Fitness**. Тобто необхідно визначити такі параметри налаштувань моделі, у яких машини рухаються з максимальною швидкістю. При цьому цікавить не просто середня швидкість всіх машин у якийсь окремий момент симуляції, а середнє її значення за всю симуляцію (тривалість якої (100 кроків) вказувалася на минулій вкладці). Для цього у параметрі "**Collected measure**", що визначає спосіб обліку значень обраного показника, вказано **MAX_ACROSS_STEPS**.  
Щоб уникнути викривлення результатів через випадкові значення, що використовуються в логіці самої імітаційної моделі, **кожна симуляція повторюється по 10 разів**, результуюче значення розраховується як **середнє арифметичне**. *Якщо вважаєте вплив випадковості на те, що відбувається в обраній вами імітаційній моделі незначним - то повторні симуляції можуть бути і не потрібні.*  
Загальний вигляд вкладки налаштувань цільової функції:  

![Вкладка налаштувань цільової функції](objective.png)

**Налаштування алгоритму пошуку** (вкладка Search Algorithm):  
*На цьому етапі було визначено модель, налаштовано її параметри (тобто вказано, які з них незмінні, а які в процесі пошуку можуть змінюватися і в яких діапазонах), і обрано міру, що лежить в основі функції пристосованості, що дозволяє оцінити якість кожного перевіряємого BehaviorSearch варіантів рішення.  
У ході дослідження на лабораторній роботі використовуються два алгоритми: Випадковий пошук(**RandomSearch**) і Простий генетичний алгоритм (**StandardGA**).  
Для цих алгоритмів, що вирішують завдання пошуку такого набору параметрів імітаційної моделі, щоб задовольнити вимоги користувача (у нашому випадку – максимізувати значення середньої швидкості переміщення агентів у заданій імітаційній моделі), необхідно вказати "**Evaluation limit**" (число ітерацій пошуку, у разі ГА – це буде кількість поколінь), та "**Search Space Encoding Representation**" (спосіб кодування варіанта вирішення). Загальноприйнятого "кращого" способу кодування немає, треба куштувати, які підійдуть саме до вашої моделі.
Параметр "**Use fitness caching**" впливає лише на продуктивність.
Параметри, специфічні для генетичного алгоритму, можна використовувати за замовчанням, якщо це не завадить отримати результат. На захисті їх, звичайно, обговоримо.*  
Загальний вид вкладки налаштувань алгоритму пошуку:  

![Вкладка налаштувань пошуку](search.png)

### Результати використання BehaviorSearch:
Діалогове вікно запуску пошуку:  

![Вікно запуску пошуку](dialog.png)

Результат пошуку параметрів імітаційної моделі, використовуючи **генетичний алгоритм**:  

![Результати пошуку за допомогою ГА](result-GA.png)

Результат пошуку параметрів імітаційної моделі, використовуючи **випадковий пошук**:  

![Результати випадкового пошуку](result-RS.png)
