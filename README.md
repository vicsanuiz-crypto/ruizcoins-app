# 🏛️ RuizCoins — Economía de aula

**RuizCoins** es una plataforma de educación financiera para Primaria y Secundaria: convierte el aula en una economía real donde cada alumno gana un sueldo por su trabajo de clase, paga impuestos, ahorra con interés, evita multas… y aprende a resistir tentaciones de consumo.

> Desarrollado y probado en aula real (CEIP, Canarias). Versión 2.0.

---

## ✨ Características

### Para el profesorado (panel de administración)
- **Multi-clase**: cada clase (1ºA, 3º, 5ºB…) es un mundo independiente, con sus alumnos, su tarifario y su tablón. Crear una clase nueva puede copiar el tarifario de otra.
- **Tarifario por especialidades**: Impuestos, Multas, Consumibles, Pupitres, Salario y Empleos, organizados con cabeceras y contador.
- **Empleos con sueldo automático**: cada alumno puede tener un trabajo (Banquero/a, Cartero/a…) que le paga solo en su periodo (semanal, quincenal…).
- **Pagos/cobros recurrentes** a toda la clase (impuestos diarios, salario semanal…), aplicables con un botón o con una tarea programada diaria (idempotente: nunca duplica).
- **Transacción masiva** con conceptos del tarifario autocompletados.
- **Interés de la caja fuerte** configurable por clase (fomenta el ahorro).
- **Modo avanzado por clase**: céntimos (2 decimales) e **IRPF**: un impuesto proporcional al saldo que el alumno debe pagar él mismo antes de una fecha; si no, recargo automático.
- Reordenación de la lista, números de lista editables (preparado para CIAL), historial completo por alumno.

### Para el alumnado (app móvil-first)
- Acceso por **clase + número de lista** (sesión recordada en su dispositivo).
- Cuenta corriente, **caja fuerte con proyección de intereses**, historial de movimientos.
- **Mercado** con el tarifario de su clase organizado por categorías, incluidas tentaciones de consumo (PS5, bici, patineta…) para trabajar el ahorro frente al impulso.
- **Impuestos por pagar** con fecha límite visible y aviso de recargo.

---

## 🏗️ Arquitectura

| Pieza | Tecnología | Alojamiento |
|---|---|---|
| Panel del profesor (`admin.html`) | HTML/CSS/JS sin dependencias | GitHub Pages |
| App del alumno (`index.html`) | HTML/CSS/JS sin dependencias | GitHub Pages |
| API REST (`flask_app.py`) | Python + Flask + SQLite | PythonAnywhere |
| Tarea diaria (`cron_recurrentes.py`) | Python | PythonAnywhere (Tasks) |

Sin frameworks, sin build, sin base de datos externa: **coste de infraestructura cero** en los planes gratuitos, y desplegable en cualquier hosting estático + cualquier servidor Python en minutos.

## 🔐 Seguridad

- Las rutas de administración exigen una **clave** (cabecera `X-Admin-Key`), que el panel pide una vez y recuerda. Se cambia editando `ADMIN_KEY` en `flask_app.py`.
- Los **precios de compra se validan en el servidor** (se ignora cualquier precio manipulado desde el navegador) y solo se venden artículos marcados comprables.
- Texto escapado en las webs (anti-XSS básico).
- **Protección de datos**: se recomienda registrar a los alumnos solo con nombre de pila o alias y su número de lista (minimización de datos, RGPD/LOPDGDD).

## 🚀 Puesta en marcha (resumen)

1. **Backend**: subir `flask_app.py` (y opcionalmente `cron_recurrentes.py`) a PythonAnywhere → pestaña *Web* → *Reload*. La base de datos y sus migraciones se crean solas.
2. **Frontend**: publicar `admin.html` + `index.html` en GitHub Pages (o cualquier hosting estático). Ajustar `API_BASE_URL` en ambos si cambia el dominio del backend.
3. Abrir el panel, introducir la clave de administración y crear la primera clase.

## 🗺️ Hoja de ruta comercial (hacia colegios)

Pendiente para una versión vendible a centros:

- [ ] **Cuentas de profesor** (email + contraseña) en lugar de clave única compartida.
- [ ] **PIN por alumno**: hoy cualquier alumno que conozca otro número podría entrar en esa cuenta.
- [ ] **Multi-centro (multi-tenant)**: un despliegue que sirva a varios colegios aislados entre sí, con panel de super-administrador.
- [ ] **Migrar SQLite → PostgreSQL** y hosting con copia de seguridad automática diaria.
- [ ] **Marca blanca**: nombre, moneda, logo y colores configurables por centro (que cada cole tenga "sus" monedas).
- [ ] **Cumplimiento RGPD formal**: contrato de encargado de tratamiento, registro de actividades, política de retención y borrado a fin de curso.
- [ ] Exportación de informes (PDF/Excel) para familias y evaluación competencial (LOMLOE: competencia emprendedora y matemática).
- [ ] Dominio propio + página de producto con demo y precios (p. ej. licencia por aula/curso).

## 📄 Licencia

© 2026 Víctor Sánchez Ruiz. Todos los derechos reservados.
Software propietario en desarrollo: no se permite su copia, redistribución ni uso comercial sin autorización expresa del autor.
