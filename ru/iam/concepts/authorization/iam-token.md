# IAM-токен

IAM-токен (токен) — уникальная последовательность символов, которая выдается пользователю после прохождения аутентификации. С помощью этого токена пользователь авторизуется в API Яндекс.Облака и выполняет запросы к ресурсам.

Если пользователь работает через консоль управления или интерфейса командной строки (CLI), то процесс получения и использования токена незаметен для пользователя. При этом пользователь может воспользоваться CLI для получения IAM-токена.

Полученный IAM-токен указывается в каждом HTTP-запросе, кроме запроса на получение самого IAM-токена. IAM-токен передается в заголовке `Authorization` в следующем формате:

```
Authorization: Bearer [IAM-token]
```

#### См. также
- [[!TITLE]](authorization.md)
