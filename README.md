# Spring Boot API – Azure Cloud Deployment

Dự án môn học: xây dựng REST API backend bằng Spring Boot và triển khai lên Microsoft Azure, tập trung vào quy trình deploy và CI/CD.

## Công nghệ sử dụng
- **Backend**: Java 17, Spring Boot, Spring Data JPA
- **Database**: H2 (in-memory)
- **Containerization**: Docker
- **Cloud Platform**: Microsoft Azure
  - Azure Container Registry (ACR)
  - Azure App Service (Web App for Containers)
- **CI/CD**: GitHub Actions (tự động build image, push ACR, deploy App Service khi push code)

## Kiến trúc triển khai

GitHub Repo → GitHub Actions → Build Docker Image → Push to Azure Container Registry → Deploy to Azure App Service


## Chạy local
```bash
mvn clean package
java -jar target/*.jar
```
API chạy tại `http://localhost:8080`

## Chạy bằng Docker
```bash
docker build -t springboot-azure-api .
docker run -p 8080:8080 springboot-azure-api
```

## Triển khai
Ứng dụng được deploy tự động lên Azure App Service qua GitHub Actions mỗi khi có commit mới trên nhánh `main`.

**Live URL**: `https://springboot-azure-api-26972.azurewebsites.net`

## Endpoints
| Method | Endpoint | Mô tả |
|--------|----------|-------|
| GET | `/api/health` | Kiểm tra trạng thái server |
| GET | `/api/products` | Lấy danh sách sản phẩm |
| POST | `/api/products` | Tạo sản phẩm mới |
| GET | `/api/products/{id}` | Lấy chi tiết sản phẩm |
| PUT | `/api/products/{id}` | Cập nhật sản phẩm |
| DELETE | `/api/products/{id}` | Xóa sản phẩm |

## Cấu hình Azure
Để deploy thành công, bạn cần tạo các tài nguyên sau trên Azure:
1. Azure Container Registry (ACR) – lưu Docker image
2. Azure App Service (Web App for Containers) – chạy ứng dụng
3. Cấu hình deployment: GitHub Actions → ACR → App Service
