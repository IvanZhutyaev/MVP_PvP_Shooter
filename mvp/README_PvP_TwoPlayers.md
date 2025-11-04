### README — Запуск двух игроков (PIE и локальная сеть)

#### Вариант 1: PIE (два окна прямо в редакторе)
1. Откройте карту PvP: `Content/FPS/Maps/GameModes/TeamDeathmatch` или `.../FreeForAll`.
2. В панели Play (иконка ▶ в тулбаре) выставьте:
   - Number of Players: 2
   - Net Mode: Play As Listen Server
   - Spawn Separate Windows: On
   - Use Single Process: Off
3. Нажмите Play — откроются 2 окна, один инстанс как listen‑server, второй как клиент.

Если второй инстанс не подключается (часто из‑за Steam):
- Временный вариант на время теста PIE:
  - Edit → Plugins → отключить “Online Subsystem Steam” и перезапустить редактор; или
  - Запускать редактор/проект с параметром `-nosteam`; или
  - Во время теста сменить сервис на Null: в `DefaultEngine.ini` в секции `[OnlineSubsystem]` поставить `DefaultPlatformService=Null`, после теста вернуть `Steam`.

#### Вариант 2: Локальная сеть (Standalone/консольные команды)
- Сервер (в консоли в редакторе или в отдельном окне Standalone):
  - Открыть карту как listen:
    ```
    open /Game/FPS/Maps/GameModes/TeamDeathmatch?listen
    ```
    или
    ```
    open /Game/FPS/Maps/GameModes/FreeForAll?listen
    ```
- Клиент (на той же машине):
  - Подключиться к серверу:
    ```
    open 127.0.0.1
    ```
- Клиент в одной локалке, но на другой машине:
  - Подключиться по IP сервера:
    ```
    open <IP_сервера>
    ```

#### Вариант 3: Упакованные билды (.exe)
- Сервер:
  ```
  FPSMT606.exe /Game/FPS/Maps/GameModes/TeamDeathmatch?listen -log -windowed -ResX=1280 -ResY=720
  ```
- Клиент (на той же машине):
  ```
  FPSMT606.exe 127.0.0.1 -log -windowed -ResX=1280 -ResY=720
  ```
- Клиент в сети:
  ```
  FPSMT606.exe <IP_сервера> -log -windowed -ResX=1280 -ResY=720
  ```

#### Примечания
- GameMode глобально не задан — он выбирается в настройках карт. Карты `TeamDeathmatch`/`FreeForAll` уже сконфигурированы под PvP.
- Если игрок не спавнится, проверьте наличие достаточного числа `PlayerStart` на карте и World Settings → GameMode Override.
- Если подключение не идёт:
  - Для PIE используйте `-nosteam` или `DefaultPlatformService=Null`.
  - В Windows разрешите приложению сетевой доступ в брандмауэре.
  - Убедитесь, что сервер запущен с `?listen`.
- В конфигурации проекта включён Steam Sockets (для онлайна это плюс). Для чистого LAN/PIE удобнее временно выключать Steam, как описано выше.
