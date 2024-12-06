# Проект banki.shop

## Ссылка на приложение
https://test-banki-shop.vercel.app/

## Описание
Этот проект представляет собой веб-приложение, использующее Vue.js версии 2 и инструменты сборки на основе Webpack. Проект стилизован с использованием SCSS.

## Системные требования

Перед началом убедитесь, что у вас установлены следующие программы:
- **Node.js** (рекомендуемая версия: >= 16)
- **npm** (устанавливается вместе с Node.js)

## Установка

1. Склонируйте репозиторий на свой компьютер:
   ```bash
   gh repo clone kuznetsovkr/test_banki_shop
   ```

2. Перейдите в папку с проектом:
   ```bash
   cd test_banki_shop
   ```

3. Установите зависимости проекта:
   ```bash
   npm install
   ```

## Скрипты

### Запуск в режиме разработки

Для запуска проекта в режиме разработки с горячей перезагрузкой используйте команду:
```bash
npm start
```
Это запустит локальный сервер разработки, доступный по адресу `http://localhost:8080` (по умолчанию).

### Сборка проекта для продакшена

Чтобы собрать проект для продакшена, выполните команду:
```bash
npm run build
```
Итоговые файлы будут помещены в папку `dist` (по умолчанию).


## Структура проекта

- **src/**: Исходный код проекта.
    - `index.js`: Точка входа приложения.
    - `App.vue`: Основной компонент приложения.
- **dist/**: Сборка проекта (создается после выполнения команды `npm run build`).
- **webpack.config.js**: Конфигурация Webpack.

## Основные зависимости

- **Vue.js**: Фреймворк для построения пользовательских интерфейсов.
- **Webpack**: Инструмент для сборки модулей.
- **SCSS**: Препроцессор CSS для стилизации.
