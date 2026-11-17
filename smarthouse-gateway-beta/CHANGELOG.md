# Журнал изменений

## 0.3.0

Третья бета: хаб готов к переезду на отдельный мини-ПК под HAOS. Включает всё из 0.2.1 (в реестр она не выпускалась).
Шесть новых миграций базы (с 0.2.1 — одиннадцать после 0.2.0) — только новые таблицы и столбцы (новые `NOT NULL` — с `DEFAULT`); перед миграцией Gateway
делает копию базы `before-update`.

- Настройка `env`: флаги хаба строками `Раздел__Ключ=значение`, только для разрешённых разделов (дворецкий, голос, сателлиты, Zigbee и др.). Секреты — только файлом в `/config/secrets/`; значения флагов в журнал не попадают.
- Образ: Python, ffmpeg, мост сателлита S1 и запасной голос на самом хабе.
- Сторож Zigbee: зависший стик — сброс или понятное сообщение семье; «Another job is running» у Supervisor — ждёт чужую задачу и не тратит попытку.
- Живой разговор с дворецким: поток через хаб и relay, конец реплики по смыслу, перебивание и отмена хода, сеансы и продолжение разговора, таймеры. Однозначные команды хаб исполняет сам; без связи — честный ответ и местные команды. Защита разговора в коде: чужой алфавит, арифметика, длина ответа.
- Сателлит S1 в комнате: тот же разговор, что в телефоне; ночью по умолчанию тихий ответ и без света.
- Память жильцов — с отдельным согласием, за флагом `Butler:Memory`; в этой версии выключена.
- Обратная связь: «Сообщить о проблеме» в приложении идёт через сервер; хаб для этого не меняется.
- Кнопки: нажатия физических кнопок запускают сценарии и режимы дома, встроенный сценарий «Прогреть».
- Тревога «холодно», наблюдатель при смене владельца, план визита, типы документов паспорта объекта.

**English.** Third beta: the hub is ready to move to its own mini PC under HAOS. Includes everything from 0.2.1 (it was
never released to the registry). Six new database migrations (eleven since 0.2.0, with 0.2.1) — new tables and columns only (new `NOT NULL` ones with a
`DEFAULT`); the Gateway copies its database (`before-update`) before migrating.

- The `env` option: hub flags as `Section__Key=value` lines, for allowed sections only (butler, voice, satellites, Zigbee and others). Secrets by file only, under `/config/secrets/`; flag values never reach the log.
- The image: Python, ffmpeg, the S1 satellite bridge and the fallback voice on the hub itself.
- The Zigbee watchdog: a hung stick — a reset or a plain message to the family; Supervisor's «Another job is running» — it waits for the other job and does not spend an attempt.
- A live conversation with the butler: streamed through the hub and the relay, end of turn by meaning, barge-in and turn cancel, sessions and follow-ups, timers. Unambiguous commands are run by the hub itself; offline — an honest answer and local commands. Conversation guards in code: a foreign alphabet, arithmetic, reply length.
- The S1 room satellite: the same conversation as on the phone; at night a quiet reply and no light by default.
- Resident memory — with its own consent, behind the `Butler:Memory` flag; off in this version.
- Feedback: «Report a problem» in the app goes through the server; the hub does not change for it.
- Buttons: physical button presses run scenes and home modes, a built-in «Warm up» scene.
- The «cold» alarm, the watcher on a change of owner, the visit plan, document types in the object passport.

## 0.2.1

Вторая бета: проверка обновления с подписью и отката на тестовой ВМ. Пять новых миграций базы — только новые таблицы и
столбцы; перед миграцией Gateway делает копию базы `before-update`.

- Тихий журнал: хаб без Zigbee не повторяет предупреждения (сторож Zigbee спит, пока дополнения нет), меньше шума HTTP; отказ подписки ядра — повтор с паузой, одна строка на эпизод.
- Мастерская: шаг «Ядро: интеграция MQTT». Копия перед обновлением находится под обоими именами Supervisor — `addon_<slug>_<версия>` и `app_<slug>_<версия>` (Supervisor 2026.10).
- Роль «Наблюдатель»: тревоги протечки, лента тревог, push; «Закрыть воду» — если владелец разрешил.
- «Уезжаем надолго»: отопление, вода, реле и свет на время отъезда, возврат уставок к приезду, голос и приложение.
- Напоминания: по времени и по приходу домой, голосом в колонке и push.
- Здоровье устройств: одна беда — одно уведомление, честное «молчит», связь словами.
- Ночь по солнцу: без места дома — ночь 23:00–07:00; часы дома в API; момент правила в карточке.
- Уведомления склеиваются: одна причина — один push, повторы обновляют его («×N»); тревоги протечки — сразу и стопкой эпизода. Подпись дома в push (несколько домов в одном приложении).
- Акт проверки системы (`/api/object/check-report`); сдача и приёмка объекта с перекрытой водой — только с подтверждением.
- «Кто дома»: хаб подтверждает геозону по домашней Wi-Fi.

**English.** Second beta: a signed update and a rollback checked on the test VM. Five new database migrations — new tables
and columns only; the Gateway copies its database (`before-update`) before migrating.

- A quiet log: a hub without Zigbee stops repeating warnings, less HTTP noise; a refused core subscription retries with a pause, one line per episode.
- Workshop: the «Core: MQTT integration» step. The backup before an update is found under both Supervisor names, `addon_<slug>_<version>` and `app_<slug>_<version>`.
- The «Watcher» role: leak alarms, the alarm feed, push; «Close the water» when the owner allows it.
- «Away for long»: heating, water, relays and lights while away, set points back before the return, by voice and in the app.
- Reminders: at a time or on coming home, spoken by the speaker and pushed.
- Device health: one problem — one notification, an honest «silent», link quality in words.
- Night by the sun: a home without a place has night 23:00–07:00; the home's clock in the API; the rule's moment on its card.
- Notifications are merged: one cause — one push, repeats update it («×N»); leak alarms at once, stacked per episode. The home's label in push (several homes in one app).
- The system check report (`/api/object/check-report`); handing over and accepting an object with the water closed only when confirmed.
- «Who is home»: the hub confirms the geofence by the home Wi-Fi.

## 0.2.0

Первая бета, собранная как готовый образ. Ставится только на тестовые хабы.

- Образ берётся из реестра `registry.smart-house.by`, а не собирается на хабе. Голос — русская и английская модели речи.
- Копии системы: перед копией Gateway делает согласованный снимок базы; живая база и закрытый ключ туннеля в копию не попадают.
- Самооткат: версия, которая трижды не запустилась за 30 минут, возвращается на прежнюю из копии «перед обновлением».
- Удалённый доступ: хаб доказывает relay, что владеет своим ключом. Восстановленный из копии хаб делает новый ключ, и доступ из-за дома ждёт подтверждения поддержки.
- Обновления: список проверенных версий ядра и системы подписан; сборка Gateway сверяется с подписанным digest. Хабы клиентов обновляет только владелец.
- Сопряжение и восстановление по этикетке: лимиты по клиентам и каналам, подтверждение «Да, это я», пока владельцы на связи.
- Пульс для поддержки: ошибки по категориям, счётчик неудачных команд.

## 0.1.0

Заготовка: образ не выпускался.
