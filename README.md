# 🗝️ maproxylib — Mapping Proxy Library§§
§
> Transparent access to nested objects dictionary fields via descriptors.

🇷🇺 [Читать на русском](README.ru.md)

`maproxylib` is a lightweight Python library that allows you to **transparently access dictionary fields as class attributes**, using the power of **descriptors**. Especially useful when working with JSON models, DTOs, complex nested structures, and API responses.

[![PyPI version](https://img.shields.io/pypi/v/maproxylib)](https://pypi.org/project/maproxylib/)
[![Python versions](https://img.shields.io/pypi/pyversions/maproxylib)](https://pypi.org/project/maproxylib/)
[![License: MIT](https://img.shields.io/github/license/yourname/maproxylib)](https://opensource.org/licenses/MIT)
[![Build Status](https://github.com/yourname/maproxylib/actions/workflows/publish.yml/badge.svg)](https://github.com/yourname/maproxylib/actions)

---

## ✨ Features

- Simple dot-style access to dictionary values  
- Support for deeply nested structures (via `path`)  
- Type hint support (`typing`, `TypeVar`)  
- Integration with `dataclasses`  
- Extensible architecture (via mixins)

---

## 🚀 Installation

```bash
pip install maproxylib
```

---

## 💡 Usage Examples

### 1. Basic Usage

```python
from dataclasses import dataclass
from maproxylib import ProxyField, DefaultMixin

@dataclass
class MyModel(DefaultMixin):
    params: dict = field(default_factory=dict)  # Dictionary storage
    name = ProxyField[str](storage_name="params", key="name", default="Guest")
    age = ProxyField[int](storage_name="params", key="age", default=30)

model = MyModel()
print(model.name)  # Guest
model.name = "Alice"
print(model.params)  # {'name': 'Alice', 'age': 30}
```

### 2. Nested Fields

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

## 📦 Key Components

| Component | Description |
|----------|-------------|
| `ProxyField[T]` | Descriptor providing access to dictionary fields |
| `get_storage_field(...)` | Factory for creating convenient fields by path or storage |
| `ProxyMixin` | Base mixin to extend behavior |
| `DefaultMixin` | Mixin that automatically applies defaults to all fields |

---

## 🧪 Testing

You can easily test with `pytest`:

```bash
pip install pytest
pytest tests/
```

---

## 🛠️ Development

To install the package locally in development mode:

```bash
uv install -e .
```

---

## 🤝 Contributing

Any suggestions, feature requests, and PRs are welcome!  
Feel free to open issues on GitHub 👉 [issues](https://github.com/yourname/maproxylib/issues)

---

## ⚖️ License

MIT License – see the [`LICENSE`](LICENSE) file for details.

---

## 📬 Author

- [@yourgithub](https://github.com/yourgithub)

---

## 🔗 Links

- PyPI: https://pypi.org/project/maproxylib/
- GitHub: https://github.com/yourname/maproxylib
```
