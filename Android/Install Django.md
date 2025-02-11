## 完整 Django 项目（支持 Android 端的登录、注册接口，数据存储在 MySQL，本地部署）

------

#### 虚拟环境搭建

**创建虚拟环境和安装依赖**

```bash
# 创建虚拟环境并激活
python -m venv myenv
source myenv/bin/activate  # macOS/Linux

# 安装 Django、DRF 和 MySQL 驱动
pip install django djangorestframework mysqlclient
```

**创建 Django 项目和应用**

```bash
# 创建 Django 项目 myproject
django-admin startproject myproject
cd myproject

# 创建用户管理应用 users
python manage.py startapp users
```



#### MySQL 中创建新的数据库和用户

**登录 MySQL**

```
mysql -u root -p
```

**创建新数据库**

```
CREATE DATABASE database_alex CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

**创建新用户并设置密码**

```
CREATE USER 'alexander'@'localhost' IDENTIFIED BY 'yang1996';
```

**赋予新用户权限**

```
GRANT ALL PRIVILEGES ON database_alex.* TO 'alexander'@'localhost';
FLUSH PRIVILEGES;
```

在 `myproject/settings.py` 文件中，将 `users` 和 `rest_framework` 添加到 `INSTALLED_APPS`：

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework.authtoken',
    'rest_framework',
    'users',
]
```

------

#### 配置 MySQL 数据库

在 `myproject/settings.py` 中，配置 MySQL 连接：

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',       # 替换为你的数据库名称
        'USER': 'myuser',           # 替换为你的 MySQL 用户名
        'PASSWORD': 'mypassword',   # 替换为你的 MySQL 密码
        'HOST': '127.0.0.1',        # 数据库主机
        'PORT': '3306',             # 数据库端口
        'OPTIONS': {
            'charset': 'utf8mb4',
        },
    }
}
```

------

### **3. 编写用户模型**

在 `users/models.py` 中使用 Django 自带的用户系统：

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    phone = models.CharField(max_length=15, blank=True, null=True)

    def __str__(self):
        return self.username
```

在 `myproject/settings.py` 中指定自定义用户模型：

```python
AUTH_USER_MODEL = 'users.CustomUser'
```

------

### **4. 创建序列化和视图**

**4.1 `users/serializers.py`**

```python
from rest_framework import serializers
from .models import CustomUser

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = CustomUser
        fields = ('id', 'username', 'email', 'phone')
```

------

**4.2 `users/views.py`**

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from rest_framework.authtoken.models import Token
from django.contrib.auth import authenticate
from .models import CustomUser
from .serializers import UserSerializer

class RegisterView(APIView):
    def post(self, request):
        username = request.data.get('username')
        password = request.data.get('password')
        email = request.data.get('email')
        phone = request.data.get('phone')

        if CustomUser.objects.filter(username=username).exists():
            return Response({"error": "Username already exists."}, status=status.HTTP_400_BAD_REQUEST)
        
        user = CustomUser.objects.create_user(username=username, password=password, email=email, phone=phone)
        token, created = Token.objects.get_or_create(user=user)
        return Response({"token": token.key}, status=status.HTTP_201_CREATED)

class LoginView(APIView):
    def post(self, request):
        username = request.data.get('username')
        password = request.data.get('password')

        user = authenticate(username=username, password=password)
        if user:
            token, created = Token.objects.get_or_create(user=user)
            return Response({"token": token.key})
        return Response({"error": "Invalid username or password"}, status=status.HTTP_400_BAD_REQUEST)
```

------

### **5. 配置路由**

**5.1 创建 `users/urls.py`**

```python
from django.urls import path
from .views import RegisterView, LoginView

urlpatterns = [
    path('register/', RegisterView.as_view(), name='register'),
    path('login/', LoginView.as_view(), name='login'),
]
```

**5.2 修改 `myproject/urls.py`**

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/users/', include('users.urls')),
]
```

------

### **6. 数据库迁移**

执行以下命令以创建数据库表结构：

```bash
python manage.py makemigrations
python manage.py migrate
```

------

### **7. 创建超级用户**

```bash
python manage.py createsuperuser
```

------

### **8. 启动服务器**

```bash
python manage.py runserver
```

访问 http://127.0.0.1:8000/ 确保项目正常运行。

------

### **9. 测试接口**

使用 Postman 或其他 API 工具测试：

#### **注册用户接口**

- **POST** `http://127.0.0.1:8000/api/users/register/`

- Request Body

  ：

  ```json
  {
    "username": "alexander",
    "password": "password123",
    "email": "alex@example.com",
    "phone": "123456789"
  }
  ```

- Response

  ：

  ```json
  {
    "token": "generated_token_here"
  }
  ```

#### **登录接口**

- **POST** `http://127.0.0.1:8000/api/users/login/`

- Request Body

  ：

  ```json
  {
    "username": "alexander",
    "password": "password123"
  }
  ```

- Response

  ：

  ```json
  {
    "token": "generated_token_here"
  }
  ```

------

### **总结**

这就是一个完整的 Django 项目，支持 Android 客户端登录和注册接口，数据存储在 MySQL 中并且可以本地部署。

需要我帮你添加 JWT 认证，或者将项目打包成 Docker 镜像吗？ 😊