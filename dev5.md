## Навигация
 - [Настройки проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [Патч ???](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [Запуск GUI](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - [Окно настроек мода](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - **Сборка проекта**
 - [Просмотр кода игры](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## Сборка проекта
После создания всех модов необходимо собрать проект.
> В шаблоне от [PizzaLovers007](https://github.com/PizzaLovers007) см. [README.md](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/README.md) есть .bat файл для сборки проекта в .zip

## 1. Сборка
> В шаблоне от [PizzaLovers007](https://github.com/PizzaLovers007) см. [README.md](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/README.md) есть батник для сборки мода в сразу в .zip с info.json, так что этот способ можно пропустить

![Сборка](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/build.png?raw=true)
Нажмите «Сборка» на верхней вкладке, затем «Сборка решения», чтобы начать сборку.
Если это слишком сложно, нажмите «Ctrl» + «Shift» + «B», чтобы начать сборку немедленно. 
<br>
![Успех](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/comp.png?raw=true)
Как показано на изображении выше, если отображается сообщение «1 успешно, 0 неудач», сборка прошла успешно. В противном случае сборка не удалась.
Даже если сборка завершится неудачей, проблема всё равно будет отображаться, поэтому, пожалуйста, устраняйте её поэтапно.

Созданному DLL-файлу будет присвоено имя «<путь к проекту>/bin/Debug/имя_проекта.dll».

## 2. Создайте Info.json
> Info.json уже присутствует в шаблоне от [PizzaLovers007](https://github.com/PizzaLovers007) см. [README.md](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/README.md) и так же собирается в .zip

UMM необходим Info.json для чтения мода.
Щёлкните правой кнопкой мыши по рабочему столу -> Создать -> Текстовый документ
Назовите только что созданный документ «Info.json».
|Ключ|Описание|

|------|---|

|Id| Имя, отображаемое в журнале, идентификатор, идентифицирующий мод|

|DisplayName| Фактическое отображаемое имя мода| 

|Author| Имя разработчика мода| 

|Version| Отображаемая версия мода| 

|AssemblyName| Имя загружаемой сборки| 

|EntryMethod| Выполняемый метод в сборке|

Здесь находится установочный файл с первой страницы.

### Пример
```json
{
  "Id": "TestMOD",
  "DisplayName": "TestMOD",
  "Author": "Flower",
  "Version": "1.0.0",
  "AssemblyName": "Test.dll",
  "EntryMethod": "Test.Main.Setup"
}
```
다 작성했다면 저장합니다.

## 3. Создайте папку
Щёлкните правой кнопкой мыши по рабочему столу -> Создать -> Папка
Назовите её именем желаемого мода.

Войдите в созданную папку, щёлкните правой кнопкой мыши -> Создать -> Папка
Снова назовите папку именем желаемого мода.

Переместите созданный ранее файл Info.json и файл сборки в эту папку.
Итоговая папка должна выглядеть так: 
    
Имя мода<br>
├── Имя мода<br>
│ &nbsp; &nbsp; ├── Info.json<br>
│ &nbsp; &nbsp; └── mod-name.dll <br>
<br>
Вернитесь на рабочий стол, где вы изначально создали папку, и сожмите созданную папку.

## 4. Применить
![Apply](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/apply.png?raw=true) <br>
Включите UMM и примените сжатый файл как мод.





[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md) (5/6)
