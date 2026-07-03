---
name: env-secrets-setup
description: Skill para generar automáticamente el archivo de configuración local .env y el script de PowerShell upload-secrets.ps1 para subir las credenciales como secretos de GitHub.
---

# Configuración de Variables de Entorno y Secretos

Este skill permite aprovisionar la configuración local y automatizar la carga de secretos de entorno a GitHub de forma segura.

## 📋 Archivos Generados

### 1. Archivo `.env` (Configuración Local)
Crea una plantilla local `.env` con las variables de base de datos de desarrollo y Flask por defecto.

### 2. Script `upload-secrets.ps1` (Automatización PowerShell)
Script para procesar el archivo `.env` línea por línea y subir de manera automática cada clave-valor como secreto al repositorio de GitHub mediante la herramienta CLI de GitHub (`gh`).

```powershell
Get-Content .env | ForEach-Object {
    if ($_ -match "^(.*?)=(.*)$") {
        $key = $matches[1]
        $value = $matches[2]
        Write-Host "Subiendo $key"
        gh secret set $key --body $value
    }
}
```

## 🚀 Instrucciones de Uso
1. Ejecuta el script de PowerShell en una consola con permisos adecuados y con el CLI de GitHub configurado (`gh auth login`):
   ```powershell
   ./upload-secrets.ps1
   ```
