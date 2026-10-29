# Quickstart: Flask Backend with Docker

## Prerequisites
-Focker installed
- Docker Compose installed (recommended)

## Quick Commands

### Build and Run
```bash
# Build the Docker image
docker build -t simple_py_service .

# Run the container
docker run -d --name simple_py_service -p 3000:3000 simple_py_service
```

### Using Docker Compose (Recommended)
```bash
# Start with docker-compose
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs -f

# Stop
docker-compose down
```

### Using Management Script
```bash
# Make script executable
chmod +x docker-manage.sh

# Build image
./docker-manage.sh build

# Start services
./docker-manage.sh up

# Test endpoints
./docker-manage.sh test

# Check status
./docker-manage.sh status

# View logs
./docker-manage.sh logs

# Stop services
./docker-manage.sh down
```

## Testing the Application

Once running, test these endpoints:
- `http://localhost:3000/` - Main page
-nttp://localhost:3000/api/health - Health check
- `http://localhost:3000/api/test` - Test endpoint
- `http://localhost:3000/api/echo/hello` - Echo endpoint

### Quick Test Commands
```bash
# Test main endpoint
curl http://localhost:3000/

# Test health endpoint
curl http://localhost:3000/api/health

# Test echo endpoint
curl http://localhost:3000/api/echo/test-message
```

## Troubleshooting

### Port Already in Use
If port 3000 is already in use:
```bash
# Stop local server first
./manage.sh stop

# Or kill process on port 3000
lsof -ti:3000 | xargs kill -9 2>/dev/null || true
```

### Docker Build Issues
```bash
# Clean Docker cache
docker system prune -a

# Rebuild without cache
docker build --no-cache -t simple_py_service .
```

### Container Won't Start
```bash
# Check Docker logs
docker logs simple_py_service

# Or docker-compose logs
docker-compose logs simple_py_service

# Restart container
docker restart simple_py_service
```

## Development with Docker

### Mount Code for Development
```bash
# Run with volume mount for live code updates
docker run -d --name simple_py_service \
  -p 3000:3000 \
  -v $(pwd):/app \
  simple_py_service
```

### Shell Access to Container
```bash
# Open shell in running container
docker exec -it simple_py_service /bin/bash

# Or with docker-compose
docker-compose exec simple_py_service /bin/bash
```

## Production Notes

For production, consider:
1. Using more workers in gunicorn command
2. Adding environment variables for configuration
3. Setting up proper logging
4. Using a reverse proxy (nginx) in front of gunicorn