# 🚀 FastAPI Hands-On Project

## 📌 Project Overview

This is a practical FastAPI hands-on project covering:

* GET endpoints
* POST requests with validation
* Path parameters
* File uploads
* In-memory database
* API testing with Swagger & curl

This project demonstrates a complete beginner-to-intermediate backend workflow.

---

# 🛠️ Tech Stack

* Python 3.10+
* FastAPI
* Uvicorn
* Pydantic
* python-multipart

---

# 📂 Project Structure

```
fastapi-handson/
│
├── app.py
├── venv/
└── README.md
```

---

# ⚙️ Setup Instructions

## 1️⃣ Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

## 2️⃣ Install Dependencies

```bash
pip install fastapi uvicorn python-multipart
```

---

# ▶️ Run the Server

```bash
uvicorn app:app --reload
```

Server URL:

```
http://127.0.0.1:8000
```

Swagger Documentation:

```
http://127.0.0.1:8000/docs
```

---

# 📄 Application Code (app.py)

```python
from fastapi import FastAPI, UploadFile, File
from pydantic import BaseModel
from typing import List

app = FastAPI()

# In-memory database
product_db = {}

class Product(BaseModel):
    name: str
    price: float
    brand: str

@app.get("/")
def home():
    return {"message": "FastAPI Hands-on Running!"}

@app.get("/products")
def get_products():
    return product_db

@app.get("/products/{product_id}")
def get_product(product_id: int):
    product = product_db.get(product_id)
    if product:
        return product
    return {"error": "Product not found"}

@app.post("/products/{product_id}")
def create_product(product_id: int, product: Product):
    product_db[product_id] = product
    return {"message": "Product created", "data": product}

@app.post("/upload")
def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

---

# 🧪 API Testing

## Using Swagger

1. Open `/docs`
2. Test POST `/products/{product_id}`
3. Test GET `/products`
4. Test file upload endpoint

---

## Using curl

### Test Home

```bash
curl http://127.0.0.1:8000/
```

### Get All Products

```bash
curl http://127.0.0.1:8000/products
```

---

# 📤 Example POST Request Body

```json
{
  "name": "Laptop",
  "price": 50000,
  "brand": "HP"
}
```

---

# 🎯 Features Implemented

* ✅ REST API structure
* ✅ Path parameters
* ✅ JSON validation with Pydantic
* ✅ In-memory storage
* ✅ File upload handling
* ✅ Interactive API documentation

---

# 🏁 Learning Outcomes

After completing this hands-on project, you will understand:

* How FastAPI handles requests and responses
* Data validation using Pydantic
* How to structure a backend API
* Testing APIs via Swagger & curl
* Handling file uploads

---

# 🚀 Next Improvements (Optional)

* Add PUT endpoint (Update Product)
* Add DELETE endpoint
* Connect to real database (MongoDB / PostgreSQL)
* Add Authentication (JWT)
* Dockerize the application

---

# 👩‍💻 Author
Vaishnavi Deshpande
Backend Learning – FastAPI Hands-On Project
