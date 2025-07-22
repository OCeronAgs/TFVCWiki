# 📁 Fundamentos de TFVC para Colaboración

## Objetivo

Empoderar a los desarrolladores para colaborar eficientemente con TFVC, dominando ramas, fusiones, y revisiones de código.

## 🔧 Fundamentos de TFVC

**Conceptos clave**

- Modelo centralizado: todos los cambios van al servidor directamente.
- Workspaces:
  - Local: detecta cambios por escaneo local.
  - Server: comunica cambios directamente con TFVC.
- Changesets: registros de cambios confirmados.
- Shelvesets: cambios guardados temporalmente para revisión.

**Comandos útiles**

```powershell
tf workspaces /owner:tu_usuario
tf history '$/Proyecto/src/login.cs /recursive'
tf shelve "LoginFix_Oscar" /replace
```

### Qué es TFVC y cómo se diferencia de Git

- TFVC (Team Foundation Version Control) usa un modelo centralizado.
- Permite control granular por archivo, ideal para entornos empresariales con flujos estables.
- **Diferencias con Git:**
  - Git es distribuido; TFVC es centralizado.
  - En TFVC, solo una rama puede estar en tu workspace activa a la vez.
  - TFVC tiene "shelvesets", una ventaja para revisiones internas sin afectación al repositorio.

| Git         | TFVC              |
|-------------|-------------------|
| Distribuido | Centralizado       |
| Pull/Merge  | Shelve/Check-in    |
| Múltiples ramas locales | Workspace activo único |

### Estructura típica

```plaintext
$/Project/
├── Main
├── Feature/
└── Bugfix/
```

### 🌿 Creación y Manejo de Ramas

**Estrategia de ramas:**

- Feature branches: para nuevas funcionalidades
- Bugfix branches: para correcciones
- Release branches: para estabilización
**Command**

- Ver cambios pendientes

```powershell
tf vc stat
```

- Crear un feature branch

```powershell
tf branch '$/MiProyecto/Main' '$/MiProyecto/Feature/featureName'
```

**Buenas prácticas:**

- Prefijo claro: Feature_, Bugfix_, Hotfix_
- Mantener ramas cortas en vida
- Sincronizar con Main frecuentemente si hay múltiples contribuidores

### 🔀 Realizar Merges Eficientes

**Validación previa**

- Una construcción exitosa

**Pasos recomendados**

- Actualiza tu workspace
- Ejecuta el merge
- Resuelve conflictos
- Valida y haz check-in

```powershell
tf merge '$/MiProyecto/Main' '$/MiProyecto/Feature/featureName'
tf resolve /auto:all
tf checkin /comment:'Merge de NuevaFuncion a Main'
```

**Conflictos:**

- Recomendar estrategia de “early merge” desde Main
- Alias o hooks para verificar que no hay conflictos antes de merge

### 🕵️‍♂️ Revisiones de Código

**Shelvesets para revisión:**

```powershell
tf shelve "Feature_NuevaFuncion_Oscar" /replace
```

- Este shelveset puede incluirse en Azure DevOps como item de revisión manual.

**Ejemplo de checklist:**

- [ ] Naming consistente
- [ ] No hay secretos expuestos
- [ ] Cumple estándares de rendimiento
- [ ] Tests asociados o evidencia de validación

### 🧰 Buenas Prácticas

**Flujo ideal:**

Branch → Development → Shelve → Review → Merge → Checkin → Integración

**Buenas practicas:**

- Crea branch
- Prepara carpeta local
- Respertar la convención de nombres
- Siempre usar branches
- Usar el .tfignore

### 🔧 Automatización

- Powershell
- tf.exe viene con el Visual Studio
- Configurarlo en el PATH

### References
- https://learn.microsoft.com/en-us/azure/devops/repos/tfvc/?view=azure-devops

```powershell
tf vc msdn
tf vc help
```