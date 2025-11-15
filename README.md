# Sistema de Inventario

Sistema de gestión de inventario desarrollado con Next.js 14, Prisma, PostgreSQL y NextAuth.

## 🚀 Características

- Gestión de productos
- Gestión de clientes
- Gestión de órdenes
- Facturación
- Reportes y dashboard
- Autenticación con NextAuth
- Almacenamiento de imágenes en AWS S3

## 📋 Requisitos Previos

- Node.js 18+ 
- PostgreSQL
- Cuenta de AWS (para S3, opcional)

## 🔧 Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/UnCarnaval/inventario.git
cd inventario
```

2. Instala las dependencias:
```bash
npm install
```

3. Configura las variables de entorno:
Crea un archivo `.env` en la raíz del proyecto con las siguientes variables:

```env
# Database
DATABASE_URL="postgresql://usuario:password@localhost:5432/nombre_db?schema=public"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="tu-secret-key-aqui"

# AWS S3 (opcional)
AWS_ACCESS_KEY_ID="tu-access-key"
AWS_SECRET_ACCESS_KEY="tu-secret-key"
AWS_REGION="us-east-1"
AWS_S3_BUCKET_NAME="tu-bucket-name"
```

4. Configura la base de datos:
```bash
npx prisma migrate dev
npx prisma generate
```

5. (Opcional) Ejecuta el seed para datos de prueba:
```bash
npm run prisma:seed
```

## 🏃 Desarrollo

```bash
npm run dev
```

La aplicación estará disponible en [http://localhost:3000](http://localhost:3000)

## 🚢 Despliegue en Vercel

1. Conecta tu repositorio de GitHub a Vercel
2. Configura las variables de entorno en el dashboard de Vercel:
   - `DATABASE_URL`
   - `NEXTAUTH_URL` (tu dominio de Vercel)
   - `NEXTAUTH_SECRET`
   - Variables de AWS S3 (si las usas)

3. Vercel detectará automáticamente Next.js y ejecutará el build

## 📝 Credenciales por Defecto

Después de ejecutar el seed:
- **Email:** john@doe.com
- **Username:** admin
- **Password:** Camila24

## 🛠️ Tecnologías

- **Next.js 14** - Framework React
- **TypeScript** - Tipado estático
- **Prisma** - ORM para PostgreSQL
- **NextAuth.js** - Autenticación
- **Tailwind CSS** - Estilos
- **shadcn/ui** - Componentes UI
- **AWS S3** - Almacenamiento de archivos

## 📄 Licencia

Este proyecto es privado.


# Last build: 2025-11-15 00:29:53
