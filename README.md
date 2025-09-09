# 🎣 FshPro (FISHWORLD) - Ecommerce de Pesca

Proyecto Fullstack de eCommerce internacional para la venta de artículos de pesca.  
Stack utilizado: **Laravel (Backend)** + **Vue.js con TailwindCSS v4 (Frontend)**.

---

## 📂 Estructura del Proyecto

FISHWORLD/
│── BACKEND/ → Laravel (API + Autenticación con Fortify + JWT + Stripe)
│── FRONTEND/ → Vue.js (TailwindCSS v4 + Axios + Vue Router + AOS)

yaml

---

## 🔧 Requisitos Previos

- [Node.js](https://nodejs.org/) (v18 o superior recomendado)  
- [NPM](https://www.npmjs.com/), [PNPM](https://pnpm.io/) o [Yarn](https://yarnpkg.com/)  
- [PHP](https://www.php.net/) (>= 8.1)  
- [Composer](https://getcomposer.org/)  
- [MySQL](https://www.mysql.com/) o [SQLite](https://www.sqlite.org/)  
- [Laravel](https://laravel.com/) CLI  

---

## 🚀 Instalación y Arranque del Proyecto

# Clonar repositorio

git clone <repo-url>

cd FISHWORLD

# ============================
# BACKEND - Laravel
# ============================

cd BACKEND
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
php artisan serve &

# ============================
# FRONTEND - Vue.js
# ============================

cd ../FRONTEND
npm install
npm run dev

# ============================
# URLs del Proyecto
# ============================
# Backend → http://127.0.0.1:8000
# Frontend → http://localhost:5173


🔗 Conexión Frontend ↔ Backend
Editar el archivo FRONTEND/src/axios.js:


import axios from "axios"

const instance = axios.create({
  baseURL: "http://127.0.0.1:8000/api", // URL del backend Laravel
})

export default instance


📜 Scripts Útiles

# ============================
# BACKEND
# ============================
php artisan migrate       # Ejecutar migraciones
php artisan db:seed       # Poblar datos iniciales
php artisan serve         # Levantar servidor
php artisan route:list    # Listar rutas registradas

# ============================
# FRONTEND
# ============================
npm run dev               # Servidor local
npm run build             # Build de producción
npm run lint              # Revisar errores de lint