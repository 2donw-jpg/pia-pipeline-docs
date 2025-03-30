---
sidebar_position: 1
---

# Introducción

**Bitbucket Pipelines** es un servicio potente y basado en la nube de integración continua (CI) y entrega continua (CD) completamente integrado en Bitbucket. Te permite automatizar los flujos de trabajo del desarrollo de software, desde la construcción y prueba de tu código hasta su despliegue en producción. Con Pipelines, puedes definir una serie de pasos que se ejecutan automáticamente cada vez que se realizan cambios en tu base de código, lo que asegura lanzamientos más rápidos y confiables.

En esta guía, te mostraremos los conceptos básicos de Bitbucket Pipelines y cómo configurar tu primer pipeline.

## Conceptos clave

Antes de comenzar con la configuración, es útil entender algunos conceptos clave en Bitbucket Pipelines:

1. **Pipelines**: Un pipeline es un conjunto de procesos automatizados que se activan por eventos, como hacer un "push" de nuevo código en tu repositorio. Estos procesos pueden incluir tareas como ejecutar pruebas, construir el proyecto o desplegar la aplicación.
  
2. **bitbucket-pipelines.yml**: Este es el archivo de configuración donde defines tu pipeline. Es un archivo YAML que se encuentra en la raíz de tu repositorio. Este archivo le indica a Bitbucket Pipelines qué pasos ejecutar y en qué orden.

3. **Steps (Pasos)**: Cada paso de un pipeline es un comando o script que se ejecuta dentro de un contenedor Docker. Los pasos pueden ejecutarse de forma secuencial o en paralelo.

4. **Branches (Ramas)**: Puedes configurar pipelines para que se ejecuten en ramas específicas, lo que permite flujos de trabajo diferentes para entornos de desarrollo, pruebas y producción.

## Configuración de tu primer Pipeline

Para comenzar con Bitbucket Pipelines, sigue estos pasos:

### Paso 1: Habilitar Bitbucket Pipelines

1. Dirígete a tu repositorio en Bitbucket.
2. En la barra lateral izquierda, haz clic en **Pipelines**.
3. Haz clic en el botón **Enable Pipelines** (Habilitar Pipelines). Esto creará automáticamente un archivo `bitbucket-pipelines.yml` en tu repositorio.

### Paso 2: Configurar el archivo `bitbucket-pipelines.yml`

El archivo `bitbucket-pipelines.yml` define los pasos de tu pipeline. Aquí tienes un ejemplo de configuración simple para empezar:

```yaml
image: node:14  # Usa una imagen Docker con Node.js instalado

pipelines:
  default:
    - step:
        name: Build and Test
        caches:
          - node
        script:
          - npm install  # Instalar dependencias
          - npm test      # Ejecutar pruebas
    - step:
        name: Deploy to Staging
        script:
          - echo "Desplegando en Staging..."
          - ./deploy.sh  # Script de despliegue personalizado
