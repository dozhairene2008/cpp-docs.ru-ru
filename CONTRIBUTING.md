# <a name="contributing"></a>Добавление данных

Благодарим вас за проявленный интерес к процессу участия в разработке документации по Visual C++!

В этом разделе содержатся сведения о базовом процессе добавления или обновления содержимого на [сайте документации по Visual C++](https://docs.microsoft.com/cpp).

В этом разделе мы рассмотрим следующие темы.

* [Процесс добавления данных](#process-for-contributing)
* [Правила](#dos-and-donts)
* [Создание документации](#building-the-docs)
* [Добавление данных в примеры](#contributing-to-samples)
* [Лицензионное соглашение с участником](#contributor-license-agreement)

## <a name="process-for-contributing"></a>Процесс добавления данных

**Шаг 1.** Создайте запрос с описанием будущей статьи и информацией о том, как предмет статьи отражен в существующем содержимом.
Содержимое в папке **docs** сгруппировано по разделам, которые упорядочены по области содержимого (например, содержимое по отладчику). Попробуйте определить правильную папку для нового содержимого. Получите отзыв по своему предложению.

При внесении незначительных изменений первый шаг можно пропустить.

**Шаг 2.** Создайте вилку репозитория `MicrosoftDocs/cpp-docs`.

**Шаг 3.** Создайте `branch` для статьи.

**Шаг 4.** Напишите статью.

Если вы затрагиваете новую тему, этот [файл шаблона](./styleguide/template.md) будет хорошей отправной точкой. Он содержит рекомендации по написанию статьи, а также пояснения по необходимым для каждой статьи метаданным, таким как сведения об авторе.

Перейдите в папку, соответствующую расположению оглавления, определенного для статьи на шаге 1.
В этой папке содержатся файлы Markdown для всех статей в этом разделе. При необходимости создайте папку для размещения файлов содержимого.

Изображения и другие статические ресурсы добавьте во вложенную папку `media`. Если вы создаете папку для содержимого, добавьте в нее папку media.

Обязательно используйте правильный синтаксис Markdown. Дополнительные сведения см. в [руководстве по стилю](./styleguide/template.md).

### <a name="example-structure"></a>Пример структуры

    docs
        /standard-library
            wstring-convert-class.md
            /media
                wstring-conversion.png

**Шаг 5.** Отправьте запрос на вытягивание из своей ветви в `MicrosoftDocs/cpp-docs/master`.

Если запрос на вытягивание относится к существующей проблеме, добавьте ключевое слово `Fixes #Issue_Number` в сообщение фиксации или описание запроса на вытягивание, чтобы автоматически закрыть проблему после слияния запроса на вытягивание. Дополнительные сведения см. в статье о [закрытии запросов с помощью сообщений фиксации](https://help.github.com/articles/closing-issues-via-commit-messages/).

Команда Visual Studio рассмотрит запрос на вытягивание и примет его или сообщит, что для его утверждения требуются другие обновления или изменения.

**Шаг 6.** Внесите необходимые изменения в ветвь в соответствии с указаниями команды.

После выполнения рекомендаций и внесения изменений команда обслуживания введет ваш запрос на вытягивание в главную ветвь.

Мы регулярно отправляем все фиксации из главной ветви в активную ветвь. После этого вы сможете увидеть свои добавления на сайте [docs.microsoft.com](https://docs.microsoft.com/cpp/).

## <a name="dos-and-donts"></a>Правила

Ниже приведен краткий список основных правил, которые следует учитывать при дополнении документации по .NET.

- Запросы на включение внесенных изменений **не должны** быть большими. Просто задайте вопрос по проблеме и начните обсуждение, чтобы мы могли принять ваше предложение и вам не пришлось тратить время.
- **Прочтите** [руководство по стилю](./styleguide/template.md) и рекомендации по [стилю изложения](./styleguide/voice-tone.md).
- **Используйте** файл [шаблона](./styleguide/template.md) в качестве отправной точки.
- **Создайте** отдельную ветвь в вилке перед работой над статьей.
- **Следуйте** [рабочему процессу GitHub Flow](https://guides.github.com/introduction/flow/).
- Регулярно **публикуйте** записи о своей работе по добавлению данных.

> [!NOTE]
> Вы можете заметить, что сейчас в некоторых разделах учитываются не все указанные здесь и в [руководстве по стилю](./styleguide/template.md) рекомендации. Мы работаем над обеспечением согласованности в рамках всего сайта. Ознакомьтесь со списком [нерешенных вопросов](https://github.com/MicrosoftDocs/cpp-docs/issues?q=is%3Aissue+is%3Aopen+label%3Aguidelines-adherence), над которыми мы работаем, чтобы решить эту конкретную задачу.

## <a name="building-the-docs"></a>Создание документации

Документация создается на языке [GitHub Flavored Markdown](https://help.github.com/categories/writing-on-github/) с помощью [DocFX](https://dotnet.github.io/docfx/) и других внутренних средств публикации и разработки. Она размещается на сайте [docs.microsoft.com](https://docs.microsoft.com/).

Чтобы создавать документы локально, необходимо установить [DocFX](https://dotnet.github.io/docfx/). Лучше всего подходят последние версии средства.

Существует несколько способов использования DocFX, и большинство из них описаны в [руководстве по началу работы с DocFX](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html). В следующих инструкциях используется версия средства [на основе командной строки](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool). Если вы знакомы с другими способами, приведенными по ссылке выше, можно воспользоваться ими.

**Примечание.** Сейчас для работы с DocFX требуется .NET Framework в Windows или Mono (для Linux или macOS). В будущем мы планируем перейти на .NET Core.

Для локального создания и предварительного просмотра итогового сайта можно использовать встроенный веб-сервер. Перейдите к папке `cpp-docs\docs` на вашем компьютере и введите следующую команду:

> docfx -t default --serve

Будет запущена локальная предварительная версия по адресу [localhost:8080](http://localhost:8080). Чтобы просмотреть изменения, перейдите к `http://localhost:8080/[path]`, например `http://localhost:8080/cpp/visual-cpp-in-visual-studio.html`.

**Примечание.** Сейчас в локальной предварительной версии отсутствуют темы, поэтому ее внешний вид будет отличаться от сайта документации. Мы работаем над исправлением этой ситуации. Мы также используем пользовательские расширения для внедренного видео, заметок и включенных документов, которые не будут отображаться в предварительной версии.

## <a name="contributing-to-samples"></a>Добавление данных в примеры

Теперь включите в статью необходимые примеры кода в виде встроенных блоков кода. В репозитории есть папка `codesnippets`, но она не готова к использованию в процессе общего добавления данных.

## <a name="contributor-license-agreement"></a>Лицензионное соглашение с участником

Перед введением запроса на включение внесенных изменений нужно подписать [Лицензионное соглашение с участником (CLA)](LICENSE). Это нужно сделать всего один раз для проектов на сайте docs.microsoft.com. Дополнительные сведения о [Лицензионных соглашениях с участником (CLA)](https://en.wikipedia.org/wiki/Contributor_License_Agreement) см. в Википедии.

Вам не нужно подписывать соглашение заранее. Вы можете клонировать запрос на включение внесенных изменений, сделать его вилку и отправить как обычно. После создания запроса на включение внесенных изменений он классифицируется ботом CLA. Если изменение незначительное (например, исправлена опечатка), к запросу добавляется отметка "Лицензионное соглашение с участником не требуется". В противном случае добавляется отметка "Требуется Лицензионное соглашение с участником". После подписания Лицензионного соглашения с участником текущие и будущие запросы на включение внесенных изменений получают отметку "Подписано Лицензионное соглашение с участником".
