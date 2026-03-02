# Fractal Bitcoin Solo Node — Umbrel Community App Store

Запустите полноценный узел Fractal Bitcoin (FB) на Umbrel со встроенной панелью управления и RPC-эндпоинтом для соло-майнинга на алгоритме SHA-256.

---

## ✅ Correct File Structure

Ваш репозиторий на GitHub должен иметь точно такую структуру:

```
your-repo/
├── umbrel-app-store.yml               ← store metadata (id + name)
└── fractal-store-solo-node/           ← folder name MUST match app id
    ├── umbrel-app.yml                 ← app listing details
    ├── docker-compose.yml             ← services definition
    ├── icon.svg                       ← 256x256 SVG icon (NO rounded corners)
    ├── 1.jpg                          ← gallery screenshots (1440x900)
    ├── 2.jpg
    ├── 3.jpg
    └── data/                          ← persisted volume data
        ├── bitcoin.conf               ← node config (copied on first run)
        └── dashboard/                 ← dashboard app files
            ├── server.js
            └── public/
                └── index.html
```

---

## 🚀 How to Install on Umbrel
# Step 1 — Put files on GitHub

    Создайте новый публичный репозиторий на GitHub (например, my-umbrel-apps)
    Загрузите все файлы из этого архива, соблюдая структуру выше
    URL вашего репозитория будет: https://github.com/YOUR_USERNAME/my-umbrel-apps
```
    ⚠️ Critical naming rules Umbrel enforces:

        В umbrel-app-store.yml обязательно должно быть поле id: (например, id: fractal-store)
        Имя папки приложения должно точно совпадать со значением id: в его umbrel-app.yml
        Значение id: приложения должно иметь префикс id: стора — например, fractal-store-solo-node
        icon.svg должен быть локальным файлом в папке приложения — удалённые URL не работают
        Изображения галереи должны быть локальными файлами .jpg в папке приложения — не URL
```
# Step 2 — Add to Umbrel

    Откройте Umbrel → App Store
    Прокрутите вниз → нажмите "Add Community App Store"
    Вставьте URL вашего репозитория на GitHub → нажмите Add
    Приложение "Fractal Bitcoin Node" появится в списке со своей иконкой

# Step 3 — Install & configure

    Нажмите на приложение → Install
    Дождитесь начальной синхронизации блокчейна (несколько часов)
    Откройте панель управления по адресу http://umbrel.local:8380
---

## ⛏️ Connecting a Miner

Once synced, point your SHA-256 miner at:

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

## 🔧 Customizing the Node

Edit `data/bitcoin.conf` and restart the app:
- Change `rpcpassword` to something personal (update docker-compose.yml env vars too)
- Set `prune=0` to keep full chain history (~100+ GB)
- Increase `maxconnections=50` for better peering

---

## 🔗 Resources

- [Fractal Bitcoin Docs](https://docs.fractalbitcoin.io)
- [fractald GitHub Releases](https://github.com/fractal-bitcoin/fractald-release/releases)
- [Fractal Block Explorer](https://explorer.fractalbitcoin.io)
- [UniSat Wallet](https://unisat.io) — for your FB coinbase address
- [Umbrel Community App Store Template](https://github.com/getumbrel/umbrel-community-app-store)
