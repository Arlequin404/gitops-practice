## Git Hooks - Automatización de Validaciones

**Descripción del Proyecto**

Este proyecto ilustra cómo implementar Git Hooks para automatizar verificaciones de calidad de código antes de realizar un commit. La configuración incluye un pre-commit hook que ejecuta ESLint, garantizando que el código cumple con los estándares definidos.

**Requisitos**

**Herramientas necesarias:**

Git: Sistema de control de versiones.

Node.js: Entorno de ejecución para JavaScript.

npm: Gestor de dependencias para Node.js.

ESLint: Herramienta para análisis estático de código JavaScript.

### Instalación y Ejecución

**Clonar el repositorio**
```bash
git clone https://github.com/Arlequin404/git-hooks-practice.git
cd tu-repositorio-githooks
```
**Instalación de dependencias**

Inicializar el proyecto Node.js:
```bash
npm init -y
```
Instalar ESLint:
```bash
npm install eslint --save-dev
```
Configurar ESLint:
```bash
npx eslint --init
```
Configurar Git Hook

**Crear un archivo en .git/hooks/pre-commit con el siguiente contenido:**
```bash
#!/bin/sh
echo "Ejecutando ESLint..."
npx eslint src/**/*.js
if [ $? -ne 0 ]; then
  echo "Errores encontrados. Commit cancelado."
  exit 1
fi
```
**Dar permisos de ejecución al archivo:**
```bash
chmod +x .git/hooks/pre-commit
```
Probar el Hook

**Realizar cambios en los archivos JavaScript.**

###Intentar realizar un commit y verificar que ESLint bloquea el commit si encuentra errores.

Corregir errores con:
```bash
npx eslint src/**/*.js --fix
```
Contacto

**Cualquier duda o sugerencia, por favor contacta a tu-email@example.com.**

## Git Hooks - Automation for Validations

**Project Description**

This project demonstrates how to implement Git Hooks to automate code quality checks before committing. The setup includes a pre-commit hook that runs ESLint to ensure code adheres to defined standards.

**Requirements**

**Necessary Tools:**

Git: Version control system.

Node.js: JavaScript runtime environment.

npm: Dependency manager for Node.js.

ESLint: Tool for static code analysis in JavaScript.

**Installation and Execution**

Clone the repository
```bash
git clone https://github.com/your-username/your-githooks-repository.git
cd your-githooks-repository
```
**Install dependencies**

Initialize the Node.js project:
```bash
npm init -y
```
Install ESLint:
```bash
npm install eslint --save-dev
```
Configure ESLint:
```bash
npx eslint --init
```
Set up Git Hook

**Create a file in .git/hooks/pre-commit with the following content:**
```bash
#!/bin/sh
echo "Running ESLint..."
npx eslint src/**/*.js
if [ $? -ne 0 ]; then
  echo "Errors found. Commit aborted."
  exit 1
fi
```
Make the file executable:
```bash
chmod +x .git/hooks/pre-commit
```
Test the Hook

Make changes to JavaScript files.

**Attempt to commit and verify that ESLint blocks the commit if errors are found.**

Fix errors with:
```bash
npx eslint src/**/*.js --fix
```
**Contact**

For any questions or suggestions, please contact your-email@example.com.
