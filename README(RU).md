# GitHub API

## Авторизация

API гитхаба предоставляет несколько возможных вариантов аутентификации.

1) **OAuth Authorizing**.

2) **Basic Authentication**.
   

Для реализации `OAuth` авторизации, требуется взаимодействовать с сервером через элемент `WKWebView`.
Подход с использованием `OAuth` авторизации является более безопасным для пользователя, т.к. разработчики приложения физический не могут получить доступ к вводимым данным.
Также для данного подхода вам нужно создать свое приложение в своем кабинете по этой ссылке
[https://github.com/settings/developers](https://github.com/settings/developers) в разделе `OAuth Apps`.   



Схема работы через `Basic Authentication` позволяет вам предоставлять пользователю для ввода собственные поля UITextField, после чего строку `"username:password"` требуется зашифровать методом `base64`.

Далее полученный `access_token` или зашифрованный логин и пароль следует прикреплять к заголовкам каждого сетевого запроса.


Обратите внимание что если вы используете Basic, вы явно должны указать это в строке с зашифрованным паролем.

```objectivec
NSString* basicAuthValue = [NSString stringWithFormat:@"Basic jkas3j3iJ8jDhfs42fswRg2g1"];
```




Также если вы используете `access_token` от `OAuth`, вы должны предупредить об этом.

```objectivec
NSString* authValue = [NSString stringWithFormat:@"token DETHLXRYWC254TXLI74ECS6VKMGU"];


```

### Реализация  Basic аутентификации

[Copy code](Documentation/text-snippetsbasicAuthentication.txt)

![](Documentation/Carbon-scene/basicAuthentication.png)

## 

## Получения списка содержимого папки

Обратите внимание, если обычно сервер всегда возвращает данные в формате словаря, то GitHub API часто возвращает массив, как в данном случае. 

[Copy code](Documentation/text-snippets/contentsOfFolder.txt)

![](Documentation/Carbon-scene/contentsOfFolder.png)





## Создание файла

Файлы создаются путем `PUT` запроса. 
Название и расширение файла вы указываете в `URL` строке, в данном примере это `book.txt`.
Содержимое будущего файла в должны зашифровать в строку методом `base64`.

Затем содержимое вставить в словарь параметров по ключу `content`.

```objectivec
NSDictionary* params = @{ @"message" : @"here enter name of this commit",
                          @"content" : base64Encoded};
```




[Copy code](Documentation/text-snippets/creatingFile.txt)

![](Documentation/Carbon-scene/creatingFile.png)



### Выгрузка изображения в папку репозитория

[Copy code](Documentation/text-snippets/uploadImage.txt)

![](Documentation/Carbon-scene/uploadImage.png)





### Создание папки


Особенность API заключается в том, что нельзя просто создать папку, чтобы папка была создана на сервере,она должна хранить хотя бы один файл.
Поэтому для создания папки, вы должны загрузить в нее по крайней мере один файл.



[Copy code](Documentation/text-snippets/creatingFolder.png)

![](Documentation/Carbon-scene/creatingFolder.png)





### Удаления файла

Чтобы удалить какой-либо файл из репозитория, вам нужно знать его `sha` значение. Для того чтобы узнать `sha` значение вы должны совершить сетевой запрос с целью получения словаря с информацией о файле, где будет находиться `sha`.

[Copy code](Documentation/text-snippets/deletingFile.txt)

![](Documentation/Carbon-scene/deletingFile.png)

### 



### Обновление содержимого файла

Для того чтобы обновить какой-либо существующий файл на репозитории, вам нужно знать sha значение данного файла.
Для того чтобы узнать `sha` значение вы должны совершить сетевой запрос с целью получения словаря с информацией о файле, где будет находиться `sha`.

[Copy code](Documentation/text-snippets/FileUpdate.txt)

![](Documentation/Carbon-scene/FileUpdate.png)

### 



### Получение информации о файле

[Copy code](Documentation/text-snippets/gettingInformationAboutFile.txt)

![](Documentation/Carbon-scene/gettingInformationAboutFile.png)





### Получение списка репозиториев с помощью (RXNetworkOperation)

[Copy code](Documentation/text-snippets/gettingListOfRepositories-RXNetworkOperation.txt)

![](Documentation/Carbon-scene/gettingListOfRepositories-RXNetworkOperation.png)





### Получение списка репозиториев с помощью (NSURLSession)

Так как все примеры взаимодействия с сервером были выполнены с помощью фраемворка `RXNetworkOperation`.
В целях демонстрации был создан сниппет как достичь такого же результата с помощью технологии `NSURLSession`.

[Copy code](Documentation/text-snippets/gettingListOFRepositories.txt)

![](Documentation/Carbon-scene/gettingListOFRepositories.png)





## Полезные ссылки


[GitHub API v3 | GitHub Developer Guide](https://developer.github.com/v3/)

[Authorizing OAuth Apps | GitHub Developer Guide](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/)

[Other Authentication Methods | GitHub Developer Guide](https://developer.github.com/v3/auth/)



## Рекомендации

Во время разработки клиент-серверных приложений важно эффективно отслеживать все исходящий запросы с устройва.
Приложение [Bagel](https://github.com/yagiz/Bagel) является простым сетевым отладчиком который перехватывает все запросы с устройства.

![](Documentation/Carbon-scene/bagel.png)

## Дополнительно

[🇬🇧 English Readme](README.md)
