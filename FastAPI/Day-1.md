# 🚀 **Ngày 1**

### **📌 Mục tiêu**

- Cài đặt FastAPI và Uvicorn
- Tạo API cơ bản với `GET`, `POST`
- Xuất artifacts file Markdown mô tả API

---

## **1️⃣ Cài đặt FastAPI**

Trước tiên, bạn cần tạo môi trường ảo và cài đặt FastAPI cùng Uvicorn.

```bash
# Tạo virtual environment
python -m venv venv
source venv/bin/activate  # Trên macOS/Linux
venv\Scripts\activate     # Trên Windows

# Cài đặt FastAPI và Uvicorn
pip install fastapi uvicorn
```

---

## **2️⃣ Viết API đơn giản**

Tạo file **`main.py`**:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello, FastAPI!"}

@app.post("/items/")
def create_item(name: str):
    return {"name": name, "status": "created"}
```

Chạy API:

```bash
uvicorn main:app --reload
```

Sau đó truy cập Swagger UI tại:  
📌 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## **3️⃣ Xuất API Documentation ra Markdown**

FastAPI hỗ trợ xuất tài liệu API bằng cách gọi OpenAPI schema.

Tạo file **`export_docs.py`** để lưu API schema vào Markdown:

```python
import requests

url = "http://127.0.0.1:8000/openapi.json"
response = requests.get(url)

if response.status_code == 200:
    schema = response.json()
    with open("api_docs.md", "w", encoding="utf-8") as f:
        f.write("# API Documentation\n\n")
        for path, methods in schema["paths"].items():
            f.write(f"## Endpoint: `{path}`\n\n")
            for method, details in methods.items():
                f.write(f"### {method.upper()}\n")
                f.write(f"- **Summary**: {details.get('summary', 'No description')}\n")
                f.write(f"- **Operation ID**: {details.get('operationId', 'N/A')}\n\n")
else:
    print("Failed to fetch OpenAPI schema")
```

Chạy lệnh:

```bash
python export_docs.py
```

File **`api_docs.md`** sẽ chứa tài liệu API theo format Markdown.

---

## **4️⃣ Kết quả mong đợi**

📄 **`api_docs.md`** (ví dụ nội dung):

```md
# API Documentation

## Endpoint: `/`

### GET

- **Summary**: No description
- **Operation ID**: home

## Endpoint: `/items/`

### POST

- **Summary**: No description
- **Operation ID**: create_item
```

---

## **🎯 Tổng kết Ngày 1 - Phần 1**

✅ Cài đặt FastAPI và Uvicorn  
✅ Viết API cơ bản
