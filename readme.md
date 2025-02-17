🚀 **Hello-World Project with UV & Docker**

===========================================

This guide will walk you through setting up a **Python project** using **UV** for package management and running it inside a **Docker container**.

**🛠 Prerequisites**

--------------------

Before you start, ensure you have the following installed:

* **MacOS** with **Homebrew** installed (brew)

* **Docker** (for containerization)

**📌 Setting Up the Project Using UV**

--------------------------------------

UV is a fast Python package manager that helps manage dependencies efficiently.

### **1️⃣ Install UV**

` brew install uv `

### **2️⃣ Create a New UV Project**

` uv init hello-world ` # Creates a new project named "hello-world" 

` cd hello-world ` # To go inside the directory

### **3️⃣ Project Structure**

After initialization, your project structure will look like this:
```
├── .python-version 
├── README.md 
├── main.py 
└── pyproject.toml 
```

### **4️⃣ Running the Project**

Run the project using uv:

` uv run main.py `

**📦 Managing Dependencies in UV**

----------------------------------

UV allows you to manage dependencies in your **pyproject.toml** file.

### **5️⃣ Installing Dependencies**

To add a package (e.g., requests):

` uv add requests `

### **6️⃣ Removing Dependencies**

To remove a package (e.g., requests):

` uv remove requests `

### **7️⃣ Install Dependencies from requirements.txt**

If you have a requirements.txt file, install all dependencies at once:

` uv add -r requirements.txt `

**🛠 Virtual Environment & Project Structure**

----------------------------------------------

Once you start adding dependencies, UV will create a **virtual environment (.venv)**, and your project structure will update:

```
├── .venv 
│   ├── bin 
│   ├── lib 
│   └── pyvenv.cfg 
├── .python-version 
├── README.md 
├── main.py 
├── pyproject.toml 
└── uv.lock 
```

### **8️⃣ Example pyproject.toml Configuration**

This file defines the project metadata and dependencies.

``` 
[project] 
name = "hello-world" 
version = "0.1.0" 
description = "Add your description here" 
readme = "README.md" 
dependencies = [] 
```

**🐳 Running the Project Inside a Docker Container**

----------------------------------------------------

If you want to **containerize the project** using **Docker**, follow these steps:

### **9️⃣ Create a Dockerfile**

Run:

` touch Dockerfile `

Then, add the following content:
```
FROM python:3.12-slim
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

COPY . /app

WORKDIR /app
RUN uv add -r requirements.txt
RUN uv sync --frozen --no-cache 

CMD ["/app/.venv/bin/uvicorn", "main:app", "--port", "8000", "--host","0.0.0.0", "--port", "8000"]
```

**🔨 Build & Run the Docker Container**

---------------------------------------

### **🔹 10️⃣ Build the Docker Image**

` docker build -t fastapi-app . `

Here, **fastapi-app** is the name of your Docker image.

### **🔹 11️⃣ Run the Container**

` docker run -p 8000:8000 fastapi-app `

Your FastAPI app will now be accessible at:👉 **http://localhost:8000**

To view API documentation, open:

* **Swagger UI:** http://localhost:8000/docs

* **Redoc UI:** http://localhost:8000/redoc

**🎯 Conclusion**

-----------------

With **UV** and **Docker**, managing dependencies and containerizing your Python applications becomes **faster, lighter, and more efficient**. 🚀

Let me know if you need any modifications! 😃