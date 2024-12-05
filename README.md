Aplicación Web Simple con CI/CD y Monitoreo

Descripción del Proyecto
Este proyecto es una aplicación web básica diseñada para demostrar la implementación de un pipeline CI/CD completo, pruebas automatizadas y monitoreo básico. Es ideal para comprender cómo integrar herramientas modernas como Docker y GitHub Actions en un flujo de desarrollo eficiente.

Contenido
Características del Proyecto
Requisitos Previos
Guía de Instalación
Uso
Estructura del Proyecto
Pipeline CI/CD
Pruebas
Monitoreo
Contribuciones
Licencia

Características del Proyecto
Frontend: Interfaz sencilla con HTML, CSS y JavaScript.
Backend: API desarrollada con Node.js y Express.
CI/CD: Pipeline automatizado con GitHub Actions y Docker.
Pruebas: Automatización de pruebas unitarias e integración.
Monitoreo: Logs centralizados y métricas básicas.

Requisitos Previos
Antes de instalar el proyecto, asegúrate de tener instalados los siguientes programas:

Node.js: Versión 16 o superior.
Docker: Versión 20.10 o superior.
Git: Última versión.
MongoDB: Local o servicio en la nube como MongoDB Atlas.
Cuenta en Docker Hub: Para manejar imágenes de contenedores.

Guía de Instalación

1. Clonar el Repositorio
bash
Copiar código
git clone https://github.com/jeancarlos04/proyecto-web.git
cd proyecto-web

3. Configurar Variables de Entorno
Crea un archivo .env en la raíz del proyecto con las siguientes variables:

bash
Copiar código
PORT=3000
DB_URI=mongodb://localhost:27017/nombre_base_de_datos

3. Instalar Dependencias
Ejecuta el siguiente comando para instalar las dependencias del proyecto:

bash
Copiar código
npm install

4. Construir la Imagen Docker
bash
Copiar código
docker build -t jeancarlos04/proyecto-web:latest .

6. Ejecutar el Contenedor Docker
bash
Copiar código
docker run -p 3000:3000 --env-file .env jeancarlos04/proyecto-web:latest

8. Acceder a la Aplicación
Abre tu navegador y ve a:
http://localhost:3000

Uso
La aplicación permite realizar operaciones básicas como:

Registrar y listar datos desde el frontend.
Consultar y manipular la base de datos a través del backend.

Estructura del Proyecto

bash
Copiar código
proyecto-web/
│
├── frontend/          # Archivos HTML, CSS, y JavaScript
├── backend/           # API desarrollada con Node.js y Express
├── database/          # Configuración de MongoDB
├── Dockerfile         # Configuración para construir la imagen Docker
├── .github/workflows/ # Configuración del pipeline CI/CD
├── .env.example       # Ejemplo de configuración de variables de entorno
├── package.json       # Dependencias del proyecto
└── README.md          # Documentación del proyecto

Pipeline CI/CD

El pipeline automatiza el desarrollo del proyecto:

Construcción: GitHub Actions construye la imagen Docker.
Pruebas: Ejecución de pruebas unitarias e integración.
Despliegue: La imagen se sube automáticamente a Docker Hub bajo el nombre jeancarlos04/proyecto-web.

Archivo YAML de GitHub Actions

yaml
Copiar código
name: Build and Deploy

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and push Docker image
        run: |
          docker build -t jeancarlos04/proyecto-web:latest .
          docker push jeancarlos04/proyecto-web:latest
          
Pruebas

Pruebas Unitarias: Validan funcionalidades individuales.
Pruebas de Integración: Validan el flujo entre componentes.
Análisis de Código Estático: Se recomienda usar ESLint para mantener la calidad del código.
Para ejecutar las pruebas:

bash
Copiar código
npm test
Monitoreo
El backend incluye un sistema de logs para rastrear errores y eventos importantes. Los logs se guardan en un archivo local (logs/error.log) y se muestran en la consola para facilitar el debugging.

