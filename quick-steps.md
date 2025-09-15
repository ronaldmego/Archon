# Quick Steps (rutina corta)

Objetivo: traer rápido las mejoras del upstream priorizando sus cambios y luego levantar Docker.

## 0) Opcional: backup local
```bash
cp .env .env.backup
cp docker-compose.yml docker-compose.yml.backup
```

## 1) Guardar tus cambios locales (si los hay)
```bash
git status
git add -A
git commit -m "local: config/docs updates" || true
```

## 2) Traer upstream y mezclar priorizando upstream
```bash
git fetch upstream

# Merge priorizando SIEMPRE upstream
git merge -X theirs upstream/main || true

# Si quedaste en conflictos:
git checkout --theirs .
git add -A
git commit -m "Resolve conflicts preferring upstream"

# Publicar en tu fork
git push origin main
```

Tips útiles:
```bash
# Rehacer el merge actual priorizando upstream
git merge --abort && git merge -X theirs upstream/main

# Ver qué viene del upstream
git log --oneline HEAD..upstream/main
```

## 3) Levantar Docker limpio con los cambios
```bash
docker compose down
docker compose up --build -d

# Verificación
docker compose ps
docker compose logs -f | cat
```

## 4) Reset completo (solo si necesitas volver exactamente al upstream)
```bash
docker compose down -v --rmi all
git fetch upstream
git reset --hard upstream/main
git clean -fd

# Restaurar config local si la usas
cp .env.backup .env 2>/dev/null || true

docker compose up --build -d
```