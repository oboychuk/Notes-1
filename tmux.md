# Краткая инструкция по `tmux`

[<= Вернуться назад](https://github.com/GnuriaN/Notes/blob/master/README.md)

_`tmux` — свободная консольная утилита-мультиплексор, предоставляющая пользователю доступ к нескольким терминалам в рамках одного экрана. `tmux` может быть отключен от экрана: в этом случае он продолжит исполняться в фоновом режиме; имеется возможность вновь подключиться к `tmux`, находящемуся в фоне._

Github:[tmux](https://github.com/tmux) Web:[tmux.github.io](https://tmux.github.io)

Очень хорошая книга по `tmux`, но она на английском языке: [The Tao of tmux](https://leanpub.com/the-tao-of-tmux/read)

### Запуск `tmux`
Посмотреть список сессий:
```Bash
tmux ls 
``` 
Пытаемся подключиться к уже существующему серверу `tmux`, если он существует, если такого ещё нет — создаёте новый:
```bash
tmux attach || tmux new 
```
После этого вы попадаете в полноценную консоль.

### Комбинации клавиш для управления:

`Ctrl+b d` - Отключиться (выйти) из текущей сессии

В одной сессии может быть сколько угодно окн:
- `Ctrl+b c` — создать окно;
- `Ctrl+b 0...9` — перейти в такое-то окно;
- `Ctrl+b p` — перейти в предыдущее окно;
- `Ctrl+b n` — перейти в следующее окно;
- `Ctrl+b l` — перейти в предыдущее активное окно (из которого вы переключились в текущее);
- `Ctrl+b &` — закрыть окно (а можно просто набрать `exit` в терминале).

В одном окне может быть много панелей:
- `Ctrl+b %` — разделить текущую панель на две, по вертикали;
- `Ctrl+b "` — разделить текущую панель на две, по горизонтали (это кавычка, которая около Enter, а не Shift+2);
- `Ctrl+b →←↑↓` — переходить между панелями;
- `Ctrl+b x` — закрыть панель (а можно просто набрать exit в терминале);
- `Ctrl+b Ctrl+(→|←|↑|↓)` — изменение размеров панели.

Недостаток — непривычным становится скроллинг:
- `Ctrl+b PgUp` — вход в «режим копирования», после чего:
- `PgUp, PgDown` — скроллинг;
- `q` — выход из «режима копирования».

### Пример файла конфигурации
```conf
# Поместите файл в домашнюю директорию, или его содержимое в файл ~/.tmux.conf

# Основные настройки  --------------------------------------------------------------

set -g set-titles on                      # Разрешить смену заголовков в оконном менеджере
set -g set-titles-string "tmux.#I.#W"     # Формат строки заголовка

set -g base-index 1                       # Начинать отсчёт окон с первого

set -g history-limit 5000                 # Размер буфера в линиях

set -g bell-action any                    # Следить за активностью на всех окнах

setw -g monitor-activity on               # Информировать когда есть активность в окнах
set -g visual-activity on                 # Показывать статусное сообщение при активности в каком либо окне

bind-key k confirm kill-window            # Подтверждать уничтожение окна
bind-key K confirm kill-server            # Подтверждать уничтожение сервера

# Статусбар -------------------------------------------------------------------

set -g display-time 2000                 # Время в миллисекундах, сколько будут отображаться сообщения (в статусбаре к примеру)

# Цвета  ---------------------------------------------------------------------

# Цвета статусбара
set -g status-fg white
set -g status-bg default
set -g status-attr default

# Цвета заголовков окон
set-window-option -g window-status-fg cyan
set-window-option -g window-status-bg default
set-window-option -g window-status-attr dim

# Цвета активных окон
set-window-option -g window-status-current-fg white
set-window-option -g window-status-current-bg default         # Выделение активного окна белым цветом
set-window-option -g window-status-current-attr bright

# Цвета командной строки
set -g message-fg white
set -g message-bg black
set -g message-attr bright
```
