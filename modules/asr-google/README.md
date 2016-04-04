### Распознавание речи Google
Этот модуль необходим для распознавания вашей речи. То есть, чтобы Агрегат смог услышать вас.

[Версия 1.1.0](https://bintray.com/artifact/download/uzyovoys/aggregate/com/aggregate/asr-google/1.1.0/asr-google-1.1.0.jar)
[Версия 1.0.0](https://bintray.com/artifact/download/uzyovoys/aggregate/com/aggregate/asr-google/1.0.0/asr-google-1.0.0.jar)

#### Установка
Перед использованием вам необходимо получить персональный ключ доступа к онлайн сервису распознавания речи Google.

**Ключ доступа**
Для его получения вам, во-первых, нужно иметь учетную запись Google. Во-вторых, вам нужно подписаться на chromium-dev@chromium.org (подписаться нужно [здесь](https://groups.google.com/a/chromium.org/forum/?fromgroups#!forum/chromium-dev)).

Теперь вы можете получить свой Google API ключ. Для этого зайдите в [Google developer console](http://cloud.google.com/console). Здесь вам нужно создать проект. После создания проекта нужно активировать Speech API.  

Наберите в поле поиска в консоли слово Speech. Появится пункт Speech API. Нажмите на него и актвируйте.  
Здесь нужно создать ключ. **Нужен ключ под названием Server key**.

**Настройка модуля**
Перед установкой данного модуля создайте файл _asr-google.json_ в директории _conf_. В нем укажите ваш ключ доступа. Пример:

```javascript
{
  "key" : "ваш ключ доступа"
}
```

#### Использование
После установки вы можете активировать Агрегат любым удобным способом (например с клавиатуры), и сразу начинать говорить. Агрегат будет слушать вашу речь сразу, не дожидаясь соединения с сервисом распознавания, как это происходит на смартфоне. Поэтому скорость

#### Ограничение на количество запросов
В документации Google сказано, что на данный сервис действует ограничение в 50 запросов в сутки. Но, как показывает практика, Google может не учитывать этот лимит.

### Дополнительные настройки
Вы можете использовать некоторые дополнительные настройки, чтобы более тонко управлять процессом распознавания и точно настроить его под свое оборудование и свои условия.

**lang** - язык распознавания (например "ru-ru" или "en-us")

**length** - время отбоя в миллисекундах (например 400). Если сигнал окончания распознавания (asr.stop) приходит раньше этого времени (после начала распознавания), то модуль не будет распознавать речь.

**minSpeech** - минимальное время говорения в миллисекундах (например 1000). При сигнале asr.listen модуль будет слушать как мининмум minSpeech миллисекунд.

**silenceTimeout** - время тишины в миллисекундах. После окончания говорения (только при сигнале asr.listen) модуль будет слушать еще silenceTimeout миллисекунд прежде чем вернуть результат. Если за это время он не услышит еще что-то.

Последние два параметра применяются только для случаев, когда используется автоматическое детектирования окончания говорения.

### Список изменений
#### 1.1.0

- Автоматическое детектирование окончания говорения
- Исправлен баг #15