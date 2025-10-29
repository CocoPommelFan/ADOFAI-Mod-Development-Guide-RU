## Навигация
 - [Настройки проекта](https://github.com/NoBrain0917/)
 - **Патч ???**
 - [Запуск GUI](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - [Окно настроек мода](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - [Создание проекта](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [Просмотр кода игры](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

# Патч
Все моды используют `0Harmony.dll` для исправления (изменения) методов (функций).     

# Добавляем новый класс
![Выбор класса](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/class.png?raw=true)    
Выберите название проекта (я назвал свой ClassLibrary2) -> Добавить -> Новый элемент
<br>
![Выберите элемент](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/cselect.png?raw=true)

Выберите класс и нажмите «Добавить», чтобы добавить новый класс.

## 1. HarmonyPatch 
`Harmony` — это библиотека, которая помогает изменять код .NET во время выполнения.

Она поддерживает возможность изменения порядка выполнения нескольких патчей и внутреннего кода самой функции.

Обычно атрибут `HarmonyPatch` используется для изменения метода.   
```c#
[HarmonyPatch(typeof(имя_класса),"имя_метода")]
```

## 2. Prefix? Postfix??
Если вы когда-либо смотрели код других разработчиков, вы, вероятно, видели это.

`Prefix` выполняет определённый метод до выполнения соответствующего метода.

И наоборот, `Postfix` выполняет определённый метод после выполнения соответствующего метода.

```c#
[HarmonyPatch(typeof(имя_класса),"имя_метода")]
public static class Test {
  public static void Prefix() {
  }
}
```
Для классов, подобных Test, приведенному выше, вы можете назвать их как угодно.

## 3. Тип возвращаемого значения метода Harmony
Обычно при разработке модов тип возвращаемого значения метода — `void`.
Однако, в зависимости от ситуации, это может быть и `bool`.
Возврат `false` завершает процесс; исходный метод не будет выполнен. (При использовании префикса)

```c#
public class TestClass {
  //Тестовый метод
  public void Test(){
    Console.WriteLine("Hello World!");
  }
}

public static class PatchTest {

  [HarmonyPatch(typeof(TestClass),"Test")]
  public static class TestReturn {
    public static bool Prefix() {
      //any code
      return false;
      //Если предотвратить выполнение исходного метода, сообщение «Hello world!» не будет записано в журнал.
    }
  }

}
```
       
Тогда вы можете задаться вопросом: «Зачем нам это нужно делать в `Prefix`?»
Как я уже упоминал ранее, `Prefix` используется до выполнения исходного метода. Использование `Postfix` после того, как исходный метод уже был выполнен, делает возврат `false` бессмысленным.

## 4. Параметры метода Harmony (измеритель параметров)
Методы Harmony могут иметь множество параметров.

- `__instance`, наиболее часто используемый, буквально извлекает экземпляр.
- `___fieldname`, извлекает поле, даже если оно `private`.
- `original-method-parameter-name`, извлекает аргумент.
```c#
public class OriginalClass {
  public int a = 1;
  private string pri = "private";

  public void start() {
    Test(1);
  }
  public void Test(int n){
  }
  public void ASDF(){
    Console.WriteLine("asdf");
  }
}

public static class PatchClass {

  [HarmonyPatch(typeof(OriginalClass),"Test")]
  public static class Test {
    public static void Prefix(OriginalClass __instance, string ___pri, int n) {
      __instance.ASDF();
      Console.WriteLine(__instance.a); //result - 1
      Console.WriteLine(___pri); //result - private
      Console.WriteLine(n); //result - 1
    }
  }
}
```
 - `__result`, 원본 메소드의 리턴값을 바꿀수 있습니다.
```c#
public class OriginalClass {
  public int Add(int a, int b){
    return a+b;
  }
}

public static class PatchTest {
  [HarmonyPatch(typeof(OriginalClass),"Add")]
  public static class Test {
    //return false
    public static bool Prefix(ref int __result) {
      __result = 5;
      return false;
    }
    //Это также возможно с использованием Postfix
    public static void Postfix(ref int __result) {
      __result = 5;
    }
    //Любой из вариантов хорош.
  }
}
```
Причина, по которой мы используем `ref` в `__result`, заключается в том, что нам нужно использовать ключевое слово `ref` для передачи измененного значения.

## «И как же мне найти класс и метод для "???"?»
Я объясню пошагово, но если хотите узнать всё сразу, см. [здесь](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md).

### Совет
При загрузке приватных полей вместо параметров можно использовать рефлексию.
```cs
typeof(T).GetField(Method_Name, AccessTools.all)?.GetValue(Class_Instance);
```
Также можно задавать значения, даже если они не являются полями.
Подробнее см. в [официальной документации](https://docs.microsoft.com/ko-kr/dotnet/api/system.reflection?view=net-5.0).




[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md) (2/6)
