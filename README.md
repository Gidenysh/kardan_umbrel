## Перевод `README.md` (с сохранением оригинальных названий файлов, ссылок и названий кнопок)

# Fractal Bitcoin Solo Node — Umbrel Community App Store

Запустите полноценную ноду **Fractal Bitcoin (FB)** на Umbrel со встроенной панелью управления и RPC endpoint’ом для соло-майнинга SHA-256.

---

## ✅ Correct File Structure

Вот как должен выглядеть ваш GitHub-репозиторий (**точно** так):

```
your-repo/
├── umbrel-app-store.yml            ← store metadata (id + name)
└── fractal-store-solo-node/         ← folder name MUST match app id
    ├── umbrel-app.yml               ← app listing details
    ├── docker-compose.yml           ← services definition
    ├── icon.svg                     ← 256x256 SVG icon (NO rounded corners)
    ├── 1.jpg                        ← gallery screenshots (1440x900)
    ├── 2.jpg
    ├── 3.jpg
    └── data/                        ← persisted volume data
        ├── bitcoin.conf             ← node config (copied on first run)
        └── dashboard/               ← dashboard app files
            ├── server.js
            └── public/
                └── index.html
```

---

## 🚀 How to Install on Umbrel

### Step 1 — Put files on GitHub

1. Создайте **новый публичный GitHub-репозиторий** (например, `my-umbrel-apps`)
2. Загрузите **все файлы** из этого архива строго в структуре, показанной выше
3. URL вашего репозитория будет: `https://github.com/YOUR_USERNAME/my-umbrel-apps`

> ⚠️ **Критические правила именования, которые Umbrel строго проверяет:**
> - `umbrel-app-store.yml` должен содержать поле `id:` (например, `id: fractal-store`)
> - Имя папки приложения **должно точно совпадать** с `id:` в её `umbrel-app.yml`
> - `id:` приложения **должен иметь префикс** store `id:` — например, `fractal-store-solo-node`
> - `icon.svg` должен быть **локальным файлом** в папке приложения — удалённые URL не работают
> - Изображения галереи должны быть **локальными `.jpg` файлами** в папке приложения — не URL

### Step 2 — Add to Umbrel

1. Откройте Umbrel → **App Store**
2. Прокрутите вниз → нажмите **"Add Community App Store"**
3. Вставьте URL вашего GitHub-репозитория → нажмите **Add**
4. Приложение **"Fractal Bitcoin Node"** появится в списке со своей иконкой

### Step 3 — Install & configure

1. Нажмите на приложение → **Install**
2. Дождитесь начальной синхронизации блокчейна (несколько часов)
3. Откройте dashboard по адресу `http://umbrel.local:8380`

---

## ⛏️ Connecting a Miner

После синхронизации укажите вашему SHA-256 майнеру:

```
Host:     umbrel.local  (or your Umbrel's LAN IP)
Port:     10332
User:     fractal
Password: fractal_umbrel_node
```

**cpuminer:**
```bash
./minerd -o http://umbrel.local:10332 -u fractal -p fractal_umbrel_node \
  --coinbase-addr=YOUR_FB_ADDRESS -a sha256d
```

**CGMiner:**
```bash
cgminer -o http://umbrel.local:10332 -u fractal -p fractal_umbrel_node \
  --coinbase-addr=YOUR_FB_ADDRESS
```

---

## 🛠️ Customizing the Node

Отредактируйте `data/bitcoin.conf` и перезапустите приложение:

- Измените `rpcpassword` на что-то персональное (обновите также env vars в `docker-compose.yml`)
- Установите `prune=0`, чтобы хранить полную историю цепочки (~100+ GB)
- Увеличьте `maxconnections=50` для лучшего пиринга

---

## 📗 Resources

- [Fractal Bitcoin Docs](https://docs.fractalbitcoin.io)
- [fractald GitHub Releases](https://github.com/fractal-bitcoin/fractald-release/releases)
- [Fractal Block Explorer](https://explorer.fractalbitcoin.io)
- [UniSat Wallet](https://unisat.io) — для вашего FB coinbase address
- [Umbrel Community App Store Template](https://github.com/getumbrel/umbrel-community-app-store)
