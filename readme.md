echo ===== Step 1: Compile Java =====
javac Sample.java
if %errorlevel% neq 0 exit /b %errorlevel%

echo ===== Step 2: Build Docker Image =====
docker build -t cicd-java-app .

if %errorlevel% neq 0 exit /b %errorlevel%

echo ===== Step 3: Remove Old Container =====
docker rm -f cicd-container 2>nul

echo ===== Step 4: Run New Container =====
docker run -d --name cicd-container cicd-java-app

echo ===== Pipeline Completed Successfully =====
