## Навигация
 - **Настройки проекта**
- [Патч ???](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [Запуск GUI](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - [Окно настроек мода](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - [Сборка проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [Просмотр кода игры](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## 1. Подготовка
 - [Visual Studio 2019](https://visualstudio.microsoft.com/ko/vs/)
 - 얼불춤 ( С установленным UMM )
 - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517)
 - [dnSpy](https://github.com/dnSpy/dnSpy/releases/download/v6.1.8/dnSpy-net-win64.zip)

## 2. Создание проекта
![Создание проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/make.png?raw=true)
Нажмите «Создать новый проект»     
    <br>
![선택](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/select2.png?raw=true)
Библиотека классов (.NET Framework) После выбора нажмите «Далее»  
Рамочная рекомендация 4.8 (?)   
Если у вас нет библиотеки классов, установите `.NET Desktop Development` из установщика Visual Studio.  

## 3. См. ссылки
![См. ссылки](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/add.png?raw=true)      
Щёлкните правой кнопкой мыши по вкладке «Ссылки» справа и выберите «Добавить ссылку».

Нажмите «Обзор» и добавьте ссылки на все элементы, перечисленные ниже.
- /A Dance of Fire and Ice_Data/Managed/UnityModManager/0Harmony.dll
- /A Dance of Fire and Ice_Data/Managed/UnityModManager/UnityModManager.dll
- /A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll


## 4. Создание настройки (точки входа?)
![탭들](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/tabs.png?raw=true)     
Щёлкните правой кнопкой мыши по файлу Class1.cs, созданному при создании проекта, и переименуйте его в Main.cs. (Называть его Main не обязательно)
```cs
public static class Main
{
}
```
Также создайте методы Setup и OnToggle.
Setup — это первый метод, который UMM запускает при запуске этого мода.

```cs
public static class Main
{
  public static UnityModManager.ModEntry.ModLogger Logger;
  public static Harmony harmony;
  public static bool IsEnabled = false;
  
  public static void Setup(UnityModManager.ModEntry modEntry)
  {
    Logger = modEntry.Logger;
    modEntry.OnToggle = OnToggle;
  }
  
  private static bool OnToggle(UnityModManager.ModEntry modEntry, bool value)
  {
    IsEnabled = value;
    
    if (value)
    {
      //При включении
      harmony = new Harmony(modEntry.Info.Id);
      harmony.PatchAll(Assembly.GetExecutingAssembly());
    }
    else
    {
      //При выключении
      harmony.UnpatchAll(modEntry.Info.Id);
    }
    return true;
  }
}
```

  

### Советы
![Красный](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/redline.png?raw=true)     
Если появилась красная линия, как указано выше, поместите указатель мыши на текст с красной линией и нажмите `Alt` + `Enter`.
![Кончик](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/altenter.png?raw=true)     

[X] [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md) (1/6)
