# 🗝️ maproxylib — Mapping Proxy Library

> Прозрачный доступ к словарным полям объектов через дескрипторы.

🇬🇧 [Read in English](README.md)

`maproxylib` — это легковесная Python-библиотека, которая позволяет тебе **прозрачно обращаться к полям словаря как к атрибутам класса**, используя мощь **дескрипторов**. Особенно удобна при работе с JSON-моделями, DTO, сложными вложенными структурами и API-ответами.

[![PyPI version](https://img.shields.io/pypi/v/maproxylib)](https://pypi.org/project/maproxylib/)
[![Python versions](https://img.shields.io/pypi/pyversions/maproxylib)](https://pypi.org/project/maproxylib/)
[![License: MIT](https://img.shields.io/github/license/yourname/maproxylib)](https://opensource.org/licenses/MIT)
[![Build Status](https://github.com/yourname/maproxylib/actions/workflows/publish.yml/badge.svg)](https://github.com/yourname/maproxylib/actions)

---

## ✨ Возможности

- Простой доступ к значениям словаря через точечную нотацию
- Работа с вложенными структурами (через `path`)
- Поддержка аннотаций типов (`typing`, `TypeVar`)
- Интеграция с `dataclasses`
- Расширяемая архитектура (через миксины)

---

## 🚀 Установка
Поддерживаются разные инструменты управления зависимостями:

### pip
```bash
pip install maproxylib
```

### poetry
```bash
poetry add maproxylib
```

### uv
```bash
uv add maproxylib
```

---

## 💡 Примеры использования

### 1. Базовое использование

```python
from dataclasses import dataclass
from maproxylib import ProxyField, DefaultMixin

@dataclass
class MyModel(DefaultMixin):
    params: dict = field(default_factory=dict)  # "Хранилище" данных
    name = ProxyField[str](storage_name="params", key="name", default="Guest")
    age = ProxyField[int](storage_name="params", key="age", default=30)

model = MyModel()
print(model.name)  # Guest
model.name = "Alice"
print(model.params)  # {'name': 'Alice', 'age': 30}
```

### 2. Вложенные поля

```python
from maproxylib import get_storage_field

address_field = get_storage_field("data", path=["address"])

@dataclass
class User:
    data: dict = field(default_factory=dict)
    city = address_field[str](key="city", default="Unknown")

user = User()
user.city = "Moscow"
print(user.data)
# {'address': {'city': 'Moscow'}}
```

---

## 📦 Ключевые компоненты

| Компонент | Описание |
|----------|----------|
| `ProxyField[T]` | Дескриптор, предоставляющий доступ к полю словаря |
| `get_storage_field(...)` | Фабрика для создания удобных полей по пути или хранилищу |
| `ProxyMixin` | Базовый миксин для расширения поведения |
| `DefaultMixin` | Миксин, автоматически применяющий дефолты ко всем полям |

---

## 🧪 Тестирование

Можно легко тестировать с помощью `pytest`:

```bash
pip install pytest
pytest tests/
```

---

## 🛠️ Разработка

Для разработки установи локально в режиме редактирования:

```bash
uv install -e .
```

---

## 🤝 Участие в проекте

Любые предложения, фич-реквесты и PR'ы приветствуются!  
Смело открывайте issues на GitHub 👉 [issues](https://github.com/yourname/maproxylib/issues)

---

## ⚖️ Лицензия

MIT License – см. файл [`LICENSE`](LICENSE) для подробностей.

---

## 📬 Автор

- [@yourgithub](https://github.com/yourgithub)

---

## 🔗 Ссылки

- PyPI: https://pypi.org/project/maproxylib/
- GitHub: https://github.com/yourname/maproxylib

