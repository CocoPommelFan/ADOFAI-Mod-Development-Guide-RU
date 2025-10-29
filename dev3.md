## Навигация
 - [Настройки проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [Патч ???](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - **Запуск GUI**
 - [Окно настроек мода](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - [Сборка проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [Просмотр кода игры](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## Запуск графического интерфейса
Для запуска графического интерфейса необходимо указать файлы `UnityEngine.dll`, `UnityEngine.CoreModule.dll`, `UnityEngine.IMGUIModule.dll` и `UnityEngine.UI.dll`.

## 1. Создать новый файл C#

Вам необходимо создать класс, наследующий от [MonoBehaviour](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html).
Затем добавьте в него метод OnGUI.
```c#
public class TestGUI : MonoBehaviour {
  public void OnGUI() {
  }
}
```

## 2. GUI, GUILayout
`GUI` и `GUILayout` доступны только в `OnGUI`.
`GUI` требует отдельного позиционирования, тогда как `GUILayout` автоматически устанавливает положение внутри макета.
     
Если вы добавляете текст с помощью `GUI`, вам необходимо задать положение и размер с помощью `Rect`.  
```cs
//GUI
GUI.Label(new Rect(x, y, width, height), text);
//GUILayout
GUILayout.Label(텍스트);
```
Генерируется на основе верхнего левого угла.

Для кнопок, переключателей или ползунков, значения которых могут изменяться в режиме реального времени, возвращаемым значением является изменённое значение.
```cs
//Код, выполняемый при нажатии кнопки
if(GUI.Button(new Rect(x,y,width,height)), text) {
//любой код
}

float val = value; // Установить значение как глобальную переменную

// Выполнить код при изменении значения ползунка
float newVal = GUI.HorizontalSlider(new Rect(x,y,width,height),val,min,max);
if(newVal!=val) {
val = newVal;
// Любой код
}
```
Вы можете выполнить такой код при изменении значения.

Существует так много методов, что сложно описать их все по отдельности. Если вам интересно, обратитесь к [документации GUILayout](https://docs.unity3d.com/ScriptReference/GUILayout.html) и [документации GUI](https://docs.unity3d.com/ScriptReference/GUI.html).

## 3. GUIStyle
Это не обязательно, но его следует использовать, если вы хотите задать стиль пользовательского интерфейса.
- Установите цвет текста с помощью `<GUIStyle>.normal.textColor`
- Установите размер текста с помощью `<GUIStyle>.fontSize`
- Установите шрифт текста с помощью `<GUIStyle>.font`
```cs
GUIStyle textStyle = new GUIStyle();
textStyle.fontSize = 50;
textStyle.alignment = TextAnchor.UpperCenter;
textStyle.normal.textColor = Color.white;
textStyle.font = RDString.GetFontDataForLanguage(RDString.language).font;
GUI.Label(new Rect(x,y,width,height), text, textStyle);
```

Это может быть что угодно, кроме текста. Более подробную информацию см. в [документации](https://docs.unity3d.com/ScriptReference/GUIStyle.html).

## 4. Создание
```cs
TestGUI test = new GameObject().AddComponent<TestGUI>();
UnityEngine.Object.DontDestroyOnLoad(test);
```
С другой стороны, когда вы его удалите,
```cs
UnityEngine.Object.DestroyImmediate(test);
```

## Совет
OnGUI может быть относительно медленным, но позволяет легко создавать пользовательский интерфейс.

Набравшись опыта, попробуйте использовать Canvas вместо OnGUI — это уменьшит задержку.

[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md) (3/6)
