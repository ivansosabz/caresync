# CareSync

> Sistema móvil para la coordinación de cuidadores en la administración de medicamentos y atención de emergencias en pacientes dependientes mediante geolocalización.

Proyecto de Tesis — Ingeniería en Sistemas Informáticos  
Autor: **Iván Sosa**  
Línea de Investigación: **Ingeniería de Software**

---

## Descripción

CareSync es una aplicación móvil diseñada para apoyar el cuidado domiciliario de pacientes dependientes. El sistema coordina automáticamente a un grupo de cuidadores familiares para que la responsabilidad de administrar medicamentos no recaiga siempre sobre la misma persona.

Cuando llega la hora de un medicamento, el sistema detecta qué cuidadores están físicamente cerca del paciente y les envía una notificación. El primero en confirmar asume la tarea, y la notificación desaparece para los demás. Además, el paciente cuenta con un botón físico de emergencia que alerta a todos los cuidadores de forma inmediata.

---

## Problema que resuelve

En muchos hogares, el cuidado de un paciente dependiente recae sobre familiares que deben coordinarse manualmente. Esto genera:

- olvidos en la administración de medicamentos
- sobrecarga sobre el cuidador que vive más cerca
- falta de coordinación entre familiares
- retrasos en la atención de emergencias

CareSync automatiza esta coordinación usando geolocalización en tiempo real.

---

## Funcionalidades del MVP

| Funcionalidad | Descripción |
|---|---|
| Registro y login | Autenticación de cuidadores |
| Gestión de medicamentos | Registro de medicamentos, horarios e instrucciones |
| Geofencing | Detección de cuidadores dentro de un radio de 1 km del paciente |
| Notificaciones push | Alertas automáticas cuando llega la hora de un medicamento |
| Confirmación de administración | El cuidador confirma y la notificación se cancela para los demás |
| Botón de emergencia | Alerta inmediata a todos los cuidadores via Flic 2 |

---

## Tecnologías

### Aplicación móvil
- React Native
- Expo
- TypeScript

### Backend
- Node.js
- Express

### Base de datos
- PostgreSQL

### Notificaciones
- Firebase Cloud Messaging (FCM)

### Geolocalización
- Expo Location
- Google Location API

### Botón de emergencia
- Flic 2 Smart Button (Bluetooth Low Energy)

---

## Arquitectura general

```
Paciente
   │
   ├── Botón Flic 2 (BLE)
   │        │
   │   App del paciente
   │        │
   │    Backend (Node.js + PostgreSQL)
   │        │
   │   Firebase Cloud Messaging
   │        │
   └── Apps de cuidadores (geofencing activo)
```

Flujo de medicamento:
```
Horario programado
   → Backend detecta la hora
   → Consulta cuidadores dentro del radio de 1 km
   → Envía notificación push a los dispositivos cercanos
   → Primer cuidador en confirmar asume la tarea
   → Notificación cancelada para los demás
```

Flujo de emergencia:
```
Paciente presiona Flic 2
   → App recibe evento BLE
   → Backend emite alerta de emergencia
   → Notificación urgente enviada a todos los cuidadores
```

---

## Estructura del proyecto

```
caresync/
│
├── mobile/                  # Aplicación móvil (React Native + Expo)
│   ├── src/
│   │   ├── screens/         # Pantallas de la app
│   │   ├── components/      # Componentes reutilizables
│   │   ├── services/        # Llamadas al backend y FCM
│   │   └── config/          # Variables de entorno y configuración
│   ├── App.tsx
│   └── package.json
│
├── backend/                 # API REST (Node.js + Express)
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   └── middlewares/
│   └── package.json
│
└── README.md
```

---

## Instalación y ejecución

### Requisitos previos

- Node.js 18+
- Expo CLI
- PostgreSQL

### Instalar dependencias (móvil)

```bash
cd mobile
npm install
```

### Ejecutar la app

```bash
npx expo start
```

La app puede ejecutarse en:
- Dispositivo físico Android/iOS con Expo Go
- Emulador Android
- Simulador iOS

### Instalar dependencias (backend)

```bash
cd backend
npm install
```

### Ejecutar el backend

```bash
npm run dev
```

---

## Estado del proyecto

- [x] Inicialización del proyecto móvil con Expo
- [x] Estructura base del repositorio
- [ ] Diseño de base de datos
- [ ] Desarrollo del backend
- [ ] Módulo de autenticación
- [ ] Módulo de medicamentos y horarios
- [ ] Integración de geofencing
- [ ] Integración de notificaciones push (FCM)
- [ ] Integración del botón Flic 2
- [ ] Pruebas del sistema

---

## Alcance del MVP

Este proyecto se limita intencionalmente a un único paciente y un grupo de cuidadores familiares. Las siguientes funcionalidades quedan fuera del alcance de la tesis y se documentan como trabajo futuro:

- Historial detallado de administraciones
- Estadísticas y reportes
- Panel web para médicos o enfermeros
- Soporte para múltiples pacientes
- Integración con sistemas de salud externos

---

## Contexto del proyecto

CareSync surge de una situación real: una paciente con movilidad reducida que requiere múltiples medicamentos diarios a distintos horarios, atendida por un grupo de familiares que deben coordinarse sin ninguna herramienta digital. El sistema busca resolver este problema de forma práctica, funcional y replicable en contextos similares.

---

## Licencia

Proyecto académico — Todos los derechos reservados © Iván Sosa
