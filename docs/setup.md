# Установка и настройка

## Установка pipx и virtualenv

1. Установить `pipx`:
    ```sh
    python -m pip install --user pipx
    python -m pipx ensurepath
    ```

2. Установить `virtualenv`:
    ```sh
    pipx install virtualenv
    ```

## Установка MkDocs

1. Создать виртуальное окружение:
    ```sh
    virtualenv env
    source env/bin/activate
    ```

2. Установить MkDocs:
    ```sh
    pip install mkdocs
    ```

## Настройка GitHub Actions и GitHub Pages

1. Создать файл `.github/workflows/actions.yml` со следующим содержимым:
    ```yaml
    name: mkdocs-deploy

    on:
      push:
        branches:
          - main

    jobs:
      build-deploy:
        runs-on: ubuntu-latest

        steps:
          - name: Checkout repository
            uses: actions/checkout@v2

          - name: Set up Python
            uses: actions/setup-python@v2
            with:
              python-version: '3.12.5'

          - name: Install dependencies
            run: |
              python -m pip install --upgrade pip
              pip install mkdocs

          - name: Build MkDocs site
            run: mkdocs build

          - name: Deploy to GitHub Pages
            uses: peaceiris/actions-gh-pages@v3
            with:
              personal_token: ${{ secrets.ACTIONS_DEPLOY_KEY }}
              publish_branch: gh-pages
              publish_dir: ./site
    ```
2. Настроить секреты в репозитории GitHub:
    - Перейти в настройки репозитория.
    - В разделе "Secrets" добавить новый секрет с именем `ACTIONS_DEPLOY_KEY` и значением токена доступа. Токен доступа можно получить, в разделе "Настройки" -> "Разработчик" -> "Личные токены доступа" на GitHub.

Результат:

Документация будет доступна по адресу `https://benqqa.github.io/mkdocs_sitw/`.

Репозиторий: https://github.com/benqqa/mkdocs_sitw.git
