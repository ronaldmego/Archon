# Quick Tips

Para Scrapear, usar llm.txt, ejemplo:

```bash
https://ai.pydantic.dev/llms-full.txt
```

## Para actualizar

### Actulizar fork
Backup (opcional)
```bash
cp .env .env.backup
cp docker-compose.yml docker-compose.yml.backup
```

Ver qué cambios tienes actualmente
```bash
# Ver el estado de tu repositorio
git status

# Ver qué archivos has modificado
git diff --name-only
```
Guardar tus cambios en tu fork
```bash
# Agregar tus archivos modificados
git add .

# Hacer commit con un mensaje descriptivo
git commit -m "add local configuration persistence"

# Subir a tu fork
git push origin main

# Verificar que no hay cambios pendientes
git status

# Ver el último commit
git log --oneline -1
```

### Mezclar
Ver status del upstream
```bash
# 1. Obtener los últimos cambios del upstream
git fetch upstream

# 2. Ver qué commits nuevos hay en el upstream que no tienes
git log --oneline HEAD..upstream/main

# 3. Ver las diferencias en archivos (sin mostrar el contenido completo)
git diff --name-only HEAD upstream/main

# 4. Ver el estado actual de tu repositorio
git status
```

Ahora sí, hacer el merge
```bash
# Obtener últimos cambios del upstream
git fetch upstream

# Hacer el merge
git merge upstream/main

# Subir el resultado a tu fork
git push origin main
```

Opción 2: Rebase en vez de merge (historial más limpio)
```bash
git checkout main
git rebase upstream/main
```