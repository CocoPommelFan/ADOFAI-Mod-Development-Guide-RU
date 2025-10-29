## Навигация
 - [Настройки проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [Патч ???](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [Запуск GUI](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - **Окно настроек мода**
 - [Создание проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [Просмотр кода игры](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## Окно настроек мода
![Окно настроек](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/setting.png?raw=true)  
Иногда требуется окно настроек мода, как на изображении выше, с возможностью сохранения.
В этом случае используйте `OnGUI` и `OnSaveGUI` в UnityModManager.ModEntry. 

## 1. OnGUI
Вернитесь к файлу Main.cs, созданному в [Основах проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md), и создайте `OnGUI`.
```cs
private static void OnGUI(UnityModManager.ModEntry modEntry)
{
}

```
Я рекомендую использовать GUILayout вместо GUI в `OnGUI`.
В остальном выполните те же действия, что и на предыдущей странице.

## 2. OnSaveGUI
Если вам нужно что-то сохранить, например, `ShowBPM`, используйте OnSaveGUI.
Аналогично добавьте `OnSaveGUI` в Main.cs.
```cs
private static void OnSaveGUI(UnityModManager.ModEntry modEntry)
{
}
```
Затем создайте новый класс, назвав его Setting.
Наследуйте этот недавно созданный класс от UnityModManager.ModSettings и добавьте несколько элементов, как показано ниже.
```cs
public class Setting : UnityModManager.ModSettings
{
  //Тип временный, но не обязательный.
  public string desiredsettingname = default;
  public bool desiredsettingname2 = default2;
  public int desiredsettingname3 = default3;

  public override void Save(UnityModManager.ModEntry modEntry) {
    var filepath = GetPath(modEntry);
    try {
      using (var writer = new StreamWriter(filepath)) {
        var serializer = new XmlSerializer(GetType());
        serializer.Serialize(writer, this);
      }
    } catch {
    }
  }
       
  public override string GetPath(UnityModManager.ModEntry modEntry) {
    return Path.Combine(modEntry.Path, GetType().Name + ".xml");
  }
  
}
```
Вернитесь в Main.cs и создайте глобальную переменную с именем ```public static Setting setting;```.
Добавьте следующее в `Setup`:
```cs
setting = new Setting();
setting = UnityModManager.ModSettings.Load<Setting>(modEntry);
```
Добавьте ```setting.Save(modEntry);``` в `OnSaveGUI`

## 3. Приложение (?)
Очень просто, в `OnToggle`
```cs
modEntry.OnGUI = OnGUI;
modEntry.OnSaveGUI = OnSaveGUI;
```
После его добавления заявка (?) будет завершена.

[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md) (4/6)
