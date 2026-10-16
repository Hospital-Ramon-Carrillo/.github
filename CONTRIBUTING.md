# Buenas prácticas de trabajo en GitHub

## 1. Rama principal y producción

- La rama `main` representa siempre la versión del código desplegada en **producción**.
- No se permite realizar cambios directamente sobre `main`.
- Todo cambio debe incorporarse mediante un **Pull Request (PR)**.
- Cada despliegue a producción debe estar identificado mediante un tag de versión.
- Si un cambio fue incorporado a `main`, debe desplegarse a producción como parte del mismo proceso controlado. No debe quedar código pendiente de despliegue en `main`.

## 2. Desarrollo en ramas independientes

Toda nueva funcionalidad, corrección o modificación debe desarrollarse en una rama independiente, creada a partir de `main` actualizado.

Nomenclatura recomendada:

- `feature/nueva-funcionalidad`
- `fix/correccion-error`
- `hotfix/error-critico`
- `refactor/mejora-codigo`

Ejemplo:

```bash
git checkout main
git pull origin main
git checkout -b feature/nuevo-tablero
```

No deben desarrollarse funcionalidades directamente sobre `main`.

## 3. Uso obligatorio de Issues

La sección **Issues** de GitHub será el espacio centralizado para registrar y organizar el trabajo.

Se deben crear Issues para:

- Nuevas funcionalidades.
- Errores detectados (*bugs*).
- Correcciones pendientes.
- Mejoras técnicas y refactorizaciones.
- Tareas de mantenimiento y documentación.

Cada Issue debe incluir una descripción clara, el resultado esperado y, cuando corresponda, un responsable.

Etiquetas recomendadas: `bug`, `feature`, `enhancement`, `documentation`, `maintenance` y `priority-high`.

No es necesario que cada tarea tenga un Issue extremadamente detallado, pero el trabajo debe ser trazable.

## 4. Pull Requests y revisión de código

- Cada rama debe integrarse a `main` mediante un Pull Request.
- El PR debe indicar qué se modificó, por qué y cómo se probó.
- Cuando corresponda, debe vincularse con su Issue mediante `Closes #123`.
- Se recomienda contar con al menos una aprobación de otro integrante del equipo.
- El código debe compilar y superar las pruebas correspondientes antes de integrarse.
- No deben fusionarse cambios con conflictos pendientes.

Una vez integrado el PR, se recomienda eliminar la rama de trabajo remota.

## 5. Commits claros y descriptivos

Los mensajes de commit deben describir brevemente el cambio realizado.

Ejemplos:

```text
feat: agregar nuevo tablero de indicadores
fix: corregir cálculo de estadísticas
refactor: optimizar consultas a base de datos
docs: actualizar documentación de instalación
```

Evitar mensajes como `cambios`, `arreglo`, `update` o `final`.

## 6. Entornos de desarrollo, pruebas y producción

- **LOCAL/DEV:** entorno utilizado para desarrollar y probar cambios individuales.
- **TEST:** entorno donde se integran y validan las modificaciones antes de su publicación.
- **PROD:** entorno que debe ejecutar exclusivamente una versión aprobada e identificable de `main`.

El código se despliega a producción después de completar las pruebas y aprobaciones necesarias. La actualización de `main` y el despliegue deben coordinarse para mantener la correspondencia entre ambos.

No se deben realizar modificaciones manuales al código en producción.

## 7. Seguridad y configuración

- Nunca subir contraseñas, tokens, credenciales, certificados privados ni archivos `.env` con valores reales.
- Mantener las configuraciones sensibles fuera del repositorio.
- Utilizar `.gitignore` para excluir archivos locales y secretos.
- No incluir datos personales de pacientes ni información clínica identificable en código, Issues, Pull Requests o logs publicados.
- Reportar cualquier exposición accidental de credenciales y proceder a su revocación o rotación.

## 8. Documentación mínima

Cada repositorio debe incluir un `README.md` que explique:

- Objetivo del proyecto.
- Tecnologías utilizadas.
- Requisitos para ejecutarlo.
- Instalación y configuración local.
- Procedimiento básico de pruebas y despliegue.

La documentación debe actualizarse cuando cambie el funcionamiento o la configuración del proyecto.

---

**Principio general:** todo cambio debe ser trazable desde un Issue hasta una rama, un Pull Request y, cuando corresponda, una versión desplegada a producción.

**Flujo de trabajo:** Issue → Rama independiente → Desarrollo local → Pruebas → Pull Request → Revisión → Validación en TEST → Integración a `main` y despliegue coordinado a PROD.
