# Troubleshooting

## Цель задания

Устранить неисправности при деплое приложения `web-consumer` и восстановить его подключение к `auth-db`.

## Troubleshooting

В ходе выполнения задания были обнаружены и устранены две неисправности.

### Проблема №1 — устаревший образ

Использовался образ:

```text
radial/busyboxplus:curl
```

Из-за использования Docker Schema 1 современный `containerd` не смог его загрузить.

Образ был заменён на:

```text
curlimages/curl
```

### Проблема №2 — неправильное DNS-имя Service

`web-consumer` обращался к:

```text
auth-db
```

Однако Service находится в другом namespace — `data`.

Правильное DNS-имя:

```text
auth-db.data
```
После внесения изменений оба Pod `web-consumer` успешно запустились и начали получать ответы от `auth-db`.

**В результате неисправность устранена, а подключение `web-consumer` к `auth-db` восстановлено.**

<img width="1552" height="856" alt="hw-kub-12-1" src="https://github.com/user-attachments/assets/7b50b92c-2693-458f-a45f-625e3023fe28" />

<img width="1528" height="4582" alt="hw-kub-12-2" src="https://github.com/user-attachments/assets/c1817b63-30bb-4273-b28c-9ac5be0647e1" />



