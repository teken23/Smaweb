# Guía de Despliegue en Vercel

## Pasos para Desplegar

### 1. Preparar el Repositorio

1. Asegúrate de que todos los cambios estén commiteados:
```bash
git add .
git commit -m "Preparado para Vercel"
```

2. Sube el código a GitHub:
```bash
git remote add origin https://github.com/UnCarnaval/inventario.git
git branch -M main
git push -u origin main
```

### 2. Conectar con Vercel

1. Ve a [vercel.com](https://vercel.com) e inicia sesión
2. Haz clic en "Add New Project"
3. Importa el repositorio `UnCarnaval/inventario`
4. Vercel detectará automáticamente que es un proyecto Next.js

### 3. Configurar Variables de Entorno

En el dashboard de Vercel, ve a **Settings > Environment Variables** y agrega:

#### Variables Requeridas:

```
DATABASE_URL=postgresql://usuario:password@host:5432/database?schema=public
NEXTAUTH_URL=https://tu-dominio.vercel.app
NEXTAUTH_SECRET=genera-un-secret-seguro-aqui
```

#### Variables Opcionales (para AWS S3):

```
AWS_ACCESS_KEY_ID=tu-access-key
AWS_SECRET_ACCESS_KEY=tu-secret-key
AWS_REGION=us-east-1
AWS_BUCKET_NAME=tu-bucket-name
AWS_FOLDER_PREFIX=
```

**Nota:** Para generar un `NEXTAUTH_SECRET` seguro, puedes usar:
```bash
openssl rand -base64 32
```

### 4. Configurar Base de Datos

#### Opción A: Usar Vercel Postgres (Recomendado)

1. En el dashboard de Vercel, ve a **Storage**
2. Crea una nueva base de datos PostgreSQL
3. Copia la `DATABASE_URL` y úsala como variable de entorno
4. Ejecuta las migraciones:
   - Puedes hacerlo desde el dashboard de Vercel en la pestaña "Storage"
   - O conectarte localmente y ejecutar: `npx prisma migrate deploy`

#### Opción B: Usar Base de Datos Externa

1. Configura tu base de datos PostgreSQL (ej: Supabase, Railway, Neon)
2. Copia la `DATABASE_URL` de conexión
3. Agrégala como variable de entorno en Vercel

### 5. Ejecutar Migraciones

Después de configurar la base de datos, ejecuta las migraciones:

```bash
# Desde tu máquina local (conectado a la misma DB)
npx prisma migrate deploy

# O desde el dashboard de Vercel usando la terminal
```

### 6. (Opcional) Ejecutar Seed

Si quieres datos de prueba, ejecuta el seed:

```bash
npm run prisma:seed
```

### 7. Desplegar

1. Vercel desplegará automáticamente cuando hagas push a `main`
2. O puedes hacer clic en "Deploy" manualmente
3. Espera a que el build termine

### 8. Verificar el Despliegue

1. Una vez desplegado, visita tu URL de Vercel
2. Verifica que la aplicación cargue correctamente
3. Prueba iniciar sesión con las credenciales del seed

## Solución de Problemas

### Error: Prisma Client no inicializado

- Asegúrate de que el script `postinstall` esté en `package.json`
- Verifica que `prisma generate` se ejecute durante el build

### Error: No se puede conectar a la base de datos

- Verifica que `DATABASE_URL` esté correctamente configurada
- Asegúrate de que la base de datos permita conexiones desde Vercel
- Verifica que el firewall de la base de datos permita las IPs de Vercel

### Error: NEXTAUTH_SECRET no configurado

- Asegúrate de agregar `NEXTAUTH_SECRET` en las variables de entorno
- El valor debe ser una cadena segura (usa `openssl rand -base64 32`)

## Comandos Útiles

```bash
# Ver logs de Vercel
vercel logs

# Desplegar manualmente
vercel --prod

# Verificar variables de entorno
vercel env ls
```

## Recursos

- [Documentación de Vercel](https://vercel.com/docs)
- [Next.js en Vercel](https://vercel.com/docs/frameworks/nextjs)
- [Prisma con Vercel](https://www.prisma.io/docs/guides/deployment/deployment-guides/deploying-to-vercel)

