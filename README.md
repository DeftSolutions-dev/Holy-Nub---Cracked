# Holy-Nub - Cracked Source Code

My contact: [t.me/desirepro](http://t.me/desirepro)

![30k broo](https://raw.githubusercontent.com/DeftSolutions-dev/Holy-Nub---Cracked/main/30k%20broo.png)
![20 year project? xdd](https://raw.githubusercontent.com/DeftSolutions-dev/Holy-Nub---Cracked/refs/heads/main/bruh%20moment%2020year....png)

> Декомпилированный и восстановленный исходный код чекера Holy-Nub, который стоит **30.000₽**.
> Все защиты (LaunchGuard, проверка лицензии) **полностью отключены**.

**Cracked by:** [@desirepro](https://t.me/DesirePro)

---

## Что это

Holy-Nub - инструмент для проверки ПК на следы читов в CS2/CSGO.
Построен на **Avalonia UI 11.2.1 / .NET 8.0**.

**Возможности:**
- Сканирование файлов на 60+ известных читов (имена, prefetch, цифровые подписи, PE-метаданные)
- Проверка DNS-кэша на домены читов
- Анализ Steam userdata
- Отображение Steam-аккаунтов (VAC-статус, SteamID, аватар)
- Детект виртуальных машин (VMware, VirtualBox, Hyper-V и др.)
- Информация о системе (версия Windows, дата установки, GPU)

---

## Версии

В репозитории содержатся **2 версии** чекера:

| | v1 (старая) | v2 (новая) |
|---|---|---|
| **Папка** | [`v1/`](v1/) | [`v2/`](v2/) |
| **Название** | Holy-Nub | HamburgerMenu.Avalonia |
| **Проект** | `Holy-Nub.csproj` | `HamburgerMenu.Avalonia.csproj` |
| **Аккаунты** | `SubmenuAccounts` / `AccountsViewModel` | `SubmenuCustomer` / `CustomerViewModel` |
| **Фреймворк** | .NET 8.0 + Avalonia 11.2.1 | .NET 8.0 + Avalonia 11.2.1 |
| **Защита** | LaunchGuard + LockFiles | LaunchGuard + LockFiles |
| **Статус кряка** | Полностью снят | Полностью снят |

---

## Что снято (кряк)

| Защита | Статус | Файл |
|---|---|---|
| **LaunchGuard** - требует запуск из `%TEMP%\.hm_*` через определённый родительский процесс | **Обойден** (закомментирован) | `App.cs` |
| **Блокировка файлов** - лочит .exe/.dll чтобы нельзя было анализировать | **Отключена** | `App.cs` |
| **LicenseManager** - проверка лицензии через Яндекс.Диск | **Есть в коде, не используется** | `HamburgerMenu.Shared` |
| **SecureAppRunner** - расшифровывает и запускает приложение из temp | **Есть в коде, не используется** | `HamburgerMenu.Shared` |
| **AES-шифрование ассетов** (`Assets.enc`) | **Поддерживается**, ключ: `HolyChecker2025SecretKey32Bytes!!` | `InMemoryImageCache.cs` |

---

## Сборка и запуск

### v1 (старая версия)
```bash
cd v1
dotnet build HolyNub.sln
dotnet run --project Holy-Nub
```

### v2 (новая версия)
```bash
cd v2
dotnet build HolyNub.sln
dotnet run --project HamburgerMenu.Avalonia
```

---

## Структура проекта

### Основное приложение (v1: `Holy-Nub/`, v2: `HamburgerMenu.Avalonia/`)

```
├── HamburgerMenu/
│   ├── App.cs                      - Точка входа, тут обход LaunchGuard
│   ├── MainWindow.cs               - Главное окно, логика показа/скрытия подменю
│   └── Program.cs                  - Запуск Avalonia
│
├── HamburgerMenu.Controls/         - Code-behind + ViewModel'ы
│   ├── MainMenu.cs                 - Гамбургер-меню, кнопки копирования серверов
│   ├── SidePanel.cs                - Навигация между вкладками
│   ├── AppControl.cs               - Управление состоянием окна
│   ├── SubmenuOne.cs               - Запуск приложений (ActivityViewer, SystemInformer и др.)
│   ├── SubmenuAccounts.cs (v1)     - Отображение Steam-аккаунтов
│   ├── SubmenuCustomer.cs (v2)     - Отображение Steam-аккаунтов (переименовано)
│   ├── AccountsViewModel.cs (v1)   - Загрузка аккаунтов, аватарки, проверка VAC
│   ├── CustomerViewModel.cs (v2)   - Загрузка аккаунтов (переименовано)
│   ├── SubmenuAnalytics.cs         - UI сканера читов
│   ├── AnalyticsViewModel.cs       - Логика полного/быстрого сканирования, экспорт
│   ├── SubmenuSettings.cs          - Отображение инфы о системе
│   ├── SettingsViewModel.cs        - WMI-запросы (GPU, детект ВМ), реестр
│   ├── RelayCommand.cs             - Реализация ICommand
│   └── SettingsRelayCommand.cs     - Реализация ICommand
│
├── HamburgerMenu.Services/         - Основная бизнес-логика
│   ├── CheatScanner.cs             - *** ГЛАВНЫЙ СКАНЕР ***
│   │                                  60+ сигнатур читов, prefetch, цифровые подписи,
│   │                                  PE-метаданные, DNS-домены, Steam userdata
│   ├── CheatScanResult.cs          - Модель результата сканирования
│   ├── SteamDiscovery.cs           - Поиск Steam, парсинг loginusers.vdf, VAC через XML API
│   ├── LaunchGuard.cs              - [ЗАЩИТА] Проверка temp + валидация родительского процесса
│   └── InMemoryImageCache.cs       - AES-зашифрованные ассеты (ключ захардкожен)
│
├── HamburgerMenu.Models/
│   └── SteamAccount.cs             - Модель Steam-аккаунта (SteamID64, VAC, аватар)
│
└── Styles/                         - Стили Avalonia (цвета, кнопки, toggle)
```

### HamburgerMenu.Shared (Библиотека - общая для обеих версий)

```
HamburgerMenu.Shared/
├── Crypto/
│   └── AesEncryption.cs            - AES-256-CBC шифрование/дешифрование
├── Models/
│   └── VersionInfo.cs              - Модель версии
└── Services/
    ├── LicenseManager.cs           - [ЗАЩИТА] Проверка лицензии через Яндекс.Диск
    ├── LicenseResult.cs            - Модель результата проверки лицензии
    ├── SecureAppRunner.cs          - [ЗАЩИТА] Расшифровка и запуск из temp
    ├── SecureConfig.cs             - Зашифрованный конфиг
    └── YandexDiskService.cs        - Клиент API Яндекс.Диска
```

---

## Захардкоженные данные

- AES-ключ: `HolyChecker2025SecretKey32Bytes!!`, IV: `HolyChecker2025I`
- Discord автора: `fayin4` (крипа)

---

## Требования

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- Windows (WMI-запросы, реестр, NtQueryInformationProcess)
