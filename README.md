## git-hooks-practice

**Descripción del Proyecto**

Este proyecto tiene como objetivo implementar un flujo de despliegue continuo (CD) utilizando prácticas de GitOps. Se utiliza Kubernetes como plataforma de orquestación de contenedores y Argo CD como herramienta de GitOps para automatizar y sincronizar el estado del clúster con el repositorio Git.

Con GitOps, la infraestructura y las aplicaciones son declaradas en un repositorio Git, lo cual permite trazabilidad, control de versiones y despliegues automáticos.

**Requisitos**

Antes de comenzar, asegúrese de tener instaladas las siguientes herramientas:

**Herramientas Necesarias**

Git

Instalación: `https://git-scm.com/downloads`

Minikube (para correr Kubernetes localmente)

Instalación:` https://minikube.sigs.k8s.io/docs/start/`

Kubectl (CLI para interactuar con Kubernetes)

Instalación:` https://kubernetes.io/docs/tasks/tools/`

Argo CD (Herramienta para despliegues GitOps)

Instalación: `https://argo-cd.readthedocs.io/`

Docker

Instalación: `https://www.docker.com/get-started`

**Configuraciones Requeridas**

Repositorio Git: Debe clonar el repositorio que contiene los manifiestos de configuración de Kubernetes y los recursos necesarios para la aplicación.

Clonar el Proyecto

Para descargar el código fuente del repositorio, ejecute el siguiente comando en su terminal:

### Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/tu-repositorio-gitops.git
```
### Acceder a la carpeta del proyecto
```bash
cd tu-repositorio-gitops
```
Instalación de Requisitos y Configuración

**1. Configurar Minikube y Kubernetes**

Inicie Minikube para crear un clúster Kubernetes local:

# Iniciar Minikube
```bash
minikube start
```
# Verificar el estado del clúster
```bash
minikube status
```
**2. Configurar Argo CD**

Instale Argo CD en el clúster local:

# Crear el namespace de Argo CD
```bash
kubectl create namespace argocd
```
# Instalar Argo CD en el namespace
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
# Verificar los pods de Argo CD
```bash
kubectl get pods -n argocd
```
Exponer el servicio de Argo CD en su máquina local:
```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```
# Acceder a Argo CD en el navegador
```bash
minikube service argocd-server -n argocd
```
Por defecto, las credenciales de acceso a Argo CD son:

**Usuario: admin**

Contraseña: obtenida con el siguiente comando:
```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```
**3. Sincronizar la Aplicación con Argo CD**

Cree una aplicación en Argo CD que sincronice el clúster Kubernetes con el repositorio Git:
```bash
kubectl apply -f infra/app-config.yaml
```
Este archivo YAML debe contener los manifiestos necesarios para el despliegue de la aplicación.

Ejecutar el Proyecto

Paso 1: Validar la Aplicación en Kubernetes

Ejecute el siguiente comando para verificar que los pods están activos:
```bash
kubectl get pods -n default
```
Paso 2: Exponer la Aplicación

Si la aplicación está configurada como un servicio, puede exponerla de la siguiente manera:
```bash
kubectl expose deployment gitops-app --type=NodePort --name=gitops-app-service
```
### Acceder a la aplicación
```bash
minikube service gitops-app-service
```
**Paso 3: Validar la Sincronización de Argo CD**

Desde el panel de Argo CD, asegúrese de que el estado de la aplicación sea Synced.

Contribuciones

Las contribuciones son bienvenidas. Si encuentras problemas o deseas mejorar el proyecto, por favor abre un issue o envía un pull request.

Licencia

**Este proyecto está licenciado bajo la MIT License.**

