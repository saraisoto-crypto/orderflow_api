# OrderFlow API

API REST para la gestión de pedidos y clientes, desarrollada con Django y Django REST Framework.

## Tecnologías usadas

- Python 3.x
- Django 4.x
- Django REST Framework (DRF)
- SQLite (base de datos por defecto)

## Instrucciones para ejecutar el servidor

### 1. Clonar el repositorio
```bash
git clone https://github.com/saraisoto-crypto/orderflow_api.git
cd orderflow_api
```

### 2. Crear y activar el entorno virtual
```bash
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows
```

### 3. Instalar dependencias
```bash
pip install django djangorestframework
```

### 4. Aplicar migraciones
```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Ejecutar el servidor
```bash
python manage.py runserver
```

La API estará disponible en: `http://127.0.0.1:8000/api/`

---

## Endpoints disponibles

### Clientes (`/api/clientes/`)

#### Listar todos los clientes
```bash
curl -X GET http://127.0.0.1:8000/api/clientes/
```
**Respuesta:**
```json
[
  {
    "id": 1,
    "nombre": "Juan Pérez",
    "direccion": "Av. Lima 123"
  }
]
```

#### Crear un cliente
```bash
curl -X POST http://127.0.0.1:8000/api/clientes/ \
  -H "Content-Type: application/json" \
  -d '{"nombre": "Juan Pérez", "direccion": "Av. Lima 123"}'
```

#### Editar un cliente
```bash
curl -X PUT http://127.0.0.1:8000/api/clientes/1/ \
  -H "Content-Type: application/json" \
  -d '{"nombre": "Juan Actualizado", "direccion": "Av. Nueva 456"}'
```

#### Eliminar un cliente
```bash
curl -X DELETE http://127.0.0.1:8000/api/clientes/1/
```

---

### Pedidos (`/api/pedidos/`)

#### Listar todos los pedidos
```bash
curl -X GET http://127.0.0.1:8000/api/pedidos/
```
**Respuesta:**
```json
[
  {
    "id": 1,
    "fecha": "2025-05-09",
    "monto_total": "150.00",
    "estado": "pendiente",
    "cliente": 1,
    "cliente_nombre": "Juan Pérez"
  }
]
```

#### Crear un pedido
```bash
curl -X POST http://127.0.0.1:8000/api/pedidos/ \
  -H "Content-Type: application/json" \
  -d '{"monto_total": "150.00", "estado": "pendiente", "cliente": 1}'
```

#### Editar un pedido
```bash
curl -X PUT http://127.0.0.1:8000/api/pedidos/1/ \
  -H "Content-Type: application/json" \
  -d '{"monto_total": "200.00", "estado": "completado", "cliente": 1}'
```

#### Eliminar un pedido
```bash
curl -X DELETE http://127.0.0.1:8000/api/pedidos/1/
```

#### Buscar pedidos
```bash
curl -X GET "http://127.0.0.1:8000/api/pedidos/?search=pendiente"
curl -X GET "http://127.0.0.1:8000/api/pedidos/?search=Juan"
```

---

## Relación entre entidades

Cada pedido está asociado a un cliente mediante una ForeignKey.
El campo `cliente_nombre` se muestra directamente en la respuesta del pedido.

---

## Estructura del proyecto

```
orderflow_api/
├── orderflow_api/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── orders/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
└── manage.py
```