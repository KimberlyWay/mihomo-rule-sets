# 🌌 Ultimate Mihomo Routing & Rulesets

![Mihomo](https://img.shields.io/badge/Mihomo-Optimized-550AEC?style=for-the-badge&logo=c)
![Remnawave](https://img.shields.io/badge/Remnawave-Ready-550AEC?style=for-the-badge)
![Routing](https://img.shields.io/badge/Smart_Routing-Enabled-550AEC?style=for-the-badge)

В этом репозитории хранится оптимизированный шаблон конфигурации для Mihomo (Clash). Сами списки и базы маршрутизации загружаются напрямую от оригинального автора, а этот конфиг грамотно объединяет их для обеспечения максимальной скорости, стабильного обхода блокировок и умного выбора серверов.

---

## 🚀 Шаблон конфигурации: `Ultimate Mihomo Ru`

Ультимативный шаблон для Remnawave и других панелей, заточенный под использование внутри РФ. Исчерпывающее техническое описание можно прочитать в [комментариях к самому коду](https://github.com/Davoyan/mihomo-rule-sets/blob/main/remnawave-templates/ultimate-mihomo-ru.yaml#L1). 

Если вы используете этот конфиг не как учебный пример, а напрямую в продакшене — **рекомендуется периодически его обновлять**.

### ✨ Ключевые особенности конфига
* **Умный выбор (LightGBM):** Автоматический подбор оптимального сервера на основе кэшированной телеметрии.
* **Тонкая настройка сервисов:** Выделенные прокси-группы и правила для:
  * 💬 **Мессенджеров:** Discord (включая разблокировку голосовых IP-диапазонов), Telegram, TeamSpeak.
  * ▶️ **Медиа:** YouTube, Twitch, Spotify.
  * 🎮 **Игр и платформ:** Steam (с прямой загрузкой контента мимо VPN для экономии трафика), osu!.
  * 🤖 **Нейросетей:** ChatGPT, Claude, Midjourney, Google DeepMind и др.
  * ☁️ **Инфраструктуры:** Cloudflare.
* **Раздельное туннелирование:** Весь внутрироссийский трафик (RU-сайты, локальные сети, торренты) направляется напрямую (**Без VPN**), снижая нагрузку на ваши VDS.
* **Фильтрация мусора:** Встроена блокировка рекламы (OISD), блокировка QUIC (для стабильности) и устранение спама от телеметрии Windows в логах.

### 📲 Рекомендуемые клиенты
* **Android / Windows / Linux / macOS:** [Prizrak Box](https://github.com/legiz-ru/Prizrak-Box), [FlClashX](https://github.com/pluralplay/FlClashX) или [Koala Clash](https://github.com/coolcoala/koala-clash)
* **iOS:** [Rabbit Hole](https://apps.apple.com/app/rabbithole-vpn-client/id6683309629)

---

## 📖 Инструкция по импорту в Remnawave

<details>
<summary><kbd>Развернуть пошаговую инструкцию в картинках</kbd></summary>

<br>

**1. Открываем панель, ищем редактор пользовательского конфига Mihomo**
<br><img src="https://github.com/user-attachments/assets/4a21f2ae-e8a4-41d5-a0f4-989a7a4bf2d7" width="300" style="border-radius: 8px; margin-top: 10px; margin-bottom: 20px;"/>

**2. Редактируем шаблон `По умолчанию`, который отдаётся пользователям подписки**
<br><img src="https://github.com/user-attachments/assets/bc1cad1b-af2b-425f-959d-dcfeb9cdca69" width="400" style="border-radius: 8px; margin-top: 10px; margin-bottom: 20px;"/>

**3. Открываем меню с готовыми шаблонами конфигураций**
<br><img src="https://github.com/user-attachments/assets/9def91bf-65d3-4abd-a22e-9359d95a642b" width="500" style="border-radius: 8px; margin-top: 10px; margin-bottom: 20px;"/>

**4. Загружаем шаблон**
<br><img src="https://github.com/user-attachments/assets/4f75c3e7-3bb3-4b8c-a5f5-4921edcd465b" width="700" style="border-radius: 8px; margin-top: 10px; margin-bottom: 20px;"/>

**5. Сохраняем, применяя изменения**
<br><img src="https://github.com/user-attachments/assets/5218f05c-23b9-4f49-8e83-b0e12defb061" width="450" style="border-radius: 8px; margin-top: 10px; margin-bottom: 20px;"/>

</details>

---

## 🗂 Используемые списки маршрутизации (Rulesets)

Списки собираются из различных проверенных источников и **обновляются раз в сутки**.

### 🇷🇺 IP-адреса внутри России
Компактный и оптимизированный список подсетей. За счет агрегации конечный вес снижен до ~1 МБ (~40к строк), что решает проблему с нехваткой оперативной памяти на клиентах под iOS.
* **Источники баз:** [IPinfo](https://ipinfo.io/data) + [MaxMind](https://github.com/P3TERX/GeoLite.mmdb/).
* **Алгоритм формирования:** Включает подсети с флагами 🇷🇺 `RU` или 🇧🇾 `BY`. Также собираются данные из AS российских операторов и компаний (по ключевым словам и доменам).
* **Файлы в [`ip-for-ru/lists`](https://github.com/Davoyan/mihomo-rule-sets/tree/main/ip-for-ru/lists):**
  * `.json` / `.srs` — для Singbox
  * `.mrs` / `.yaml` — для Clash/Mihomo
  * `.txt` / `.lst` — сырые списки сетей
  * `snippet.json` — сниппет для Remnawave

### 🌐 Домены внутри России
Сгенерированный список доменов (с удалением повторов) для прямого роутинга без участия VPN-сервера.
* **Источники баз:**
  * `category-ru` и российские компании от MetaCubeX.
  * Список `outside` от itdoginfo.
  * Списки `category-ru` и `whitelist` от hydraponique.
  * `Legacy` домены, которые резолвятся в RU IP.
* **Файлы в [`rules`](https://github.com/Davoyan/mihomo-rule-sets/tree/main/rules):** Доступны форматы `.lst`, `.mrs` и `.yaml`.
