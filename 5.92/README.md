# VK API for Golang 5.92

Внимание - этот репозиторий в **очень ранней разработке**.

## Установка

```shell
go get -u github.com/SevereCloud/vksdk
```

## Модули

- [API](https://github.com/SevereCloud/vksdk/tree/master/5.92/api)
- [Callback](https://github.com/SevereCloud/vksdk/tree/master/5.92/callback)
- [Bots Long Poll API](https://github.com/SevereCloud/vksdk/tree/master/5.92/longpoll-bot)

## Пример

```go
package main

import (
	"fmt"
	"log"

	vksdk "github.com/SevereCloud/vksdk/5.92/api"
)

func main() {
	vk := vksdk.Init("<TOKEN>")

	params := make(map[string]string)
	params["user_ids"] = "1"

	users, vkErr := vk.UsersGet(params)
	if vkErr.Code != 0 {
		log.Fatal(vkErr.Message)
	}

	for _, user := range users {
		fmt.Printf("Пользователя с id%d зовут %s %s\n", user.ID, user.FirstName, user.LastName)
	}
}
```

## Известные проблемы

- [VK API JSON Schema](https://github.com/VKCOM/vk-api-schema) кишит ошибками и не обновляется
- Документация VK имеет ошибки и не обновляется 
- На некоторые методы, API возвращает динамический JSON

### Костыли

[StorageGet](https://vk.com/dev/storage.get) если нет параметра `keys`, вернет массив из одного объекта.
...

## TODO

- [ ] Большенство методов API
- [x] Ограничитель на запросы
- [x] Callback
- [x] LongPoll bots
- [ ] LongPoll users
- [ ] Streaming API
- [x] HTTP client
- [ ] Получение токена
- [ ] Загрузка файлов
- [ ] Тесты
- [ ] Англоязычный README
- [ ] Версионирование
- [ ] Поддержка следующих версий API