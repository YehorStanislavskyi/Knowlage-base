# i3wm

## **Polybar**

Решение для 2 мониторов (пересмотреть, не самое правильное решение )

файл launch.sh

```
#!/usr/bin/env sh

# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -x polybar >/dev/null; do sleep 1; done

# Launch
polybar main &
polybar no-main;

echo "Bar launched..."
```

## i3- Rounded-corners

Установка I3-rounded-corners&#x20;

https://github.com/terroo/i3-radius

```
```
