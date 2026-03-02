# Fractal Bitcoin Solo Node — Umbrel Community App Store (UmbrelOS 1.5)

Этот репозиторий — Community App Store для UmbrelOS 1.5.

## Как добавить в Umbrel

1. Открой Umbrel → **App Store**
2. Пролистай вниз → **Add Community App Store**
3. Вставь URL репозитория:

- https://github.com/Gidenysh/kardan_umbrel

После добавления появится приложение **Fractal Bitcoin Node**.

## Установка

Нажми **Install** в Umbrel.

## Подключение майнера

Важно: это приложение предоставляет **RPC** (не Stratum). Для Antminer S19* обычно нужен Stratum-пул/прокси.

RPC (из приложения):
- Host: umbrel.local (или IP Umbrel)
- Port: 10332
- User: fractal
- Password: задаётся Umbrel как APP_PASSWORD

Ссылки:
- Releases: https://github.com/fractal-bitcoin/fractald-release/releases
- Docs: https://docs.fractalbitcoin.io/
- UniSat: https://unisat.io/
