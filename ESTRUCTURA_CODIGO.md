# 📚 Estructura del Código - entrada_aceituna.html

## 📋 Resumen General
Este archivo contiene toda la aplicación de gestión de aceitunas de Corporación Costa Verde.
Es un archivo HTML único que incluye CSS y JavaScript inline.

---

## 🏗️ Estructura del Archivo

### SECCIÓN 1: HTML HEAD (Líneas 1-10)
- Meta tags
- Importación de fuentes (Google Fonts - Inter)
- Título de la página

### SECCIÓN 2: ESTILOS CSS (Líneas 11-1800 aprox.)
Los estilos están organizados por componentes:

| Sección | Descripción |
|---------|-------------|
| Layout General | `.main-container`, `.sidebar`, `.content-area` |
| Header | `.header`, `.user-info`, `.btn-logout` |
| Navegación | `.nav-item`, `.nav-icon` |
| Tarjetas | `.card`, `.entry-card` |
| Formularios | `.form-group`, `.form-input`, `.form-select` |
| Modal | `.modal-overlay`, `.modal-content` |
| Reportes | `.reporte-table`, estilos de tabla |
| Responsivo | Media queries para móviles |

### SECCIÓN 3: HTML BODY (Líneas 1800-3100 aprox.)
Estructura principal de la interfaz:

```
<body>
├── <header>              → Barra superior con logo y usuario
├── <div.main-container>
│   ├── <aside.sidebar>   → Menú lateral de navegación
│   └── <main.content-area>
│       ├── section-registro    → Formulario de entrada
│       ├── section-historial   → Listado de tarjetas
│       └── section-reportes    → Tabla de reportes
├── <div.modal-overlay>   → Modal para crear/editar
├── <div.confirmOverlay>  → Modal de confirmación
└── <div.detailModal>     → Modal de vista detallada
```

### SECCIÓN 4: JAVASCRIPT (Líneas 3100-8446)
Todo el código JavaScript está dentro de `<script>` tags.

---

## 🔧 Funciones JavaScript Principales

### 🔐 AUTENTICACIÓN Y ROLES
| Función | Descripción |
|---------|-------------|
| `puedeVerPrecios()` | Verifica si el usuario puede ver precios (solo admin) |
| `ocultarElementosSegunRol()` | Oculta secciones según el rol del usuario |
| `logout()` | Cierra sesión y redirige al login |

### 📋 GESTIÓN DE ENTRADAS
| Función | Descripción |
|---------|-------------|
| `saveEntry()` | Guarda o actualiza una entrada en localStorage |
| `editEntry(id)` | Carga datos de una entrada para editar |
| `confirmDelete()` | Elimina una entrada después de confirmación |
| `renderEntries()` | Renderiza las tarjetas de entradas |

### 🎯 CALIBRES
| Función | Descripción |
|---------|-------------|
| `agregarCalibre()` | Agrega un nuevo calibre al lote |
| `eliminarCalibre(id)` | Elimina un calibre específico |
| `actualizarTotalCalibres()` | Recalcula totales de todos los calibres |
| `obtenerCalibresData()` | Obtiene array de calibres para guardar |
| `cargarCalibres(array)` | Carga calibres existentes al editar |
| `llenadoRapidoCalibres()` | Genera calibres en un rango |

### 🧮 CÁLCULOS
| Función | Descripción |
|---------|-------------|
| `calcularTotalKg()` | Calcula kg totales del envase |
| `calcularTotalTransporte()` | Calcula costo de transporte |
| `calcularCostoVarones()` | Calcula costo de personal varones |
| `calcularCostoMujeres()` | Calcula costo de personal mujeres |
| `calcularCostoTraspaleadores()` | Calcula costo de traspaleadores |
| `calcularTotalPersonal()` | Suma todos los costos de personal |

### 📊 REPORTES
| Función | Descripción |
|---------|-------------|
| `filtrarReportes()` | Filtra y renderiza la tabla de reportes |
| `renderReporteTable(entries)` | Genera HTML de la tabla de reportes |
| `exportarReporteExcel()` | Exporta reportes a Excel (.xls) |
| `exportarLoteExcel()` | Exporta un lote específico a Excel |

### 💰 SIMULACIÓN DE VENTA
| Función | Descripción |
|---------|-------------|
| `toggleSimularVenta()` | Activa/desactiva modo simulación |
| `llenarTodosPrecios()` | Rellena todos los precios con un valor |
| `llenarPreciosPorRango()` | Rellena precios en un rango |
| `limpiarTodosPrecios()` | Limpia todos los precios simulados |

### 🎨 SELECCIÓN DE OPCIONES
| Función | Descripción |
|---------|-------------|
| `selectColor(color)` | Selecciona color de aceituna |
| `selectVariety(variety)` | Selecciona variedad |
| `selectProcess(process)` | Selecciona proceso |
| `selectDestination(dest)` | Selecciona destino (exportación) |
| `toggleEnvaseFields()` | Muestra/oculta campos de envase |

### 🔄 NAVEGACIÓN Y UI
| Función | Descripción |
|---------|-------------|
| `showSection(section)` | Cambia entre secciones principales |
| `openModal()` | Abre modal de nueva entrada |
| `closeModal()` | Cierra modal con confirmación |
| `resetForm()` | Limpia todos los campos del formulario |
| `updateTitleBar()` | Actualiza hora y nombre de usuario |

---

## 💾 ALMACENAMIENTO DE DATOS

### localStorage
Los datos se guardan en `localStorage` bajo la clave `aceitunaEntries`.

### Estructura de una Entrada
```javascript
{
    id: 1234567890,           // Timestamp único
    codigoLote: "LOTE-001",   // Código del lote
    fecha: "2024-12-10",      // Fecha de entrada
    vendedor: "Juan Pérez",   // Nombre del vendedor
    supervisor: "María López", // Nombre del supervisor
    precio: "6.50",           // Precio de compra por Kg
    
    // Tipo de Envase
    tipoEnvase: "bidones",
    envase_cantidad: "10",
    envase_kilos: "60",
    cantidad: "600",          // Total Kg calculado
    
    // Color y Variedad
    color: "verde",
    variedad: "sal",
    proceso: "entera",
    
    // Calibres (array)
    calibres: [
        {
            calibre: "180-200",
            bidones: 5,
            kilosPorBidon: 60,
            sobras: 10,
            subtotal: 310,
            precio: 8.50,
            valorTotal: 2635
        }
    ],
    
    // Transporte
    transporteConductor: "mario",
    transporteViajes: "2",
    transporteCostoViaje: "150",
    transporteTotal: "300",
    
    // Personal - Varones
    varonesQty: "4",
    varonesHoraHombre: "12",
    varonesHorasTrabajadas: "8",
    varonesCostoTotal: "384",
    
    // Personal - Mujeres
    mujeresQty: "6",
    mujeresHoraHombre: "10",
    mujeresHorasTrabajadas: "8",
    mujeresCostoTotal: "480",
    
    // Traspaleadores
    traspaleadoresQty: "2",
    traspaleadoresCostoDia: "80",
    traspaleadoresDias: "1",
    traspaleadoresCostoTotal: "160",
    
    // Otros Gastos
    otrosGastos: [...],
    totalOtrosGastos: "50"
}
```

---

## 📈 FÓRMULAS DE CÁLCULO

### Kilos Totales
```
Cantidad Total = (Envase_Cantidad × Envase_Kilos) + Envase_Puchos
```

### Subtotal por Calibre
```
Subtotal = (Bidones × Kg_Por_Bidon) + Sobras
```

### Valor Total por Calibre
```
Valor = Subtotal × Precio_Por_Kg
```

### Gastos Operativos
```
Gastos_Op = Transporte + Varones + Mujeres + Traspaleadores + Otros
```

### Ganancia por Calibre
```
Ganancia = (Precio_Venta - Precio_Compra) × Subtotal
```

### Ganancia Neta del Lote
```
Ganancia_Neta = Suma(Ganancias_Calibres) - Gastos_Operativos
```

---

## 👥 ROLES DE USUARIO

| Rol | Ver Precios | Ver Reportes | Editar |
|-----|-------------|--------------|--------|
| admin | ✅ | ✅ | ✅ |
| ing_yeny | ❌ | ❌ | ✅ |
| trabajador | ❌ | ❌ | ✅ |

---

## 📝 NOTAS IMPORTANTES

1. **Bidones de Exportación**: Cuando se selecciona, Kg/Bidón = 60 automáticamente
2. **Simulación de Venta**: Los precios simulados NO se guardan
3. **Sincronización**: Al editar/eliminar, los reportes se actualizan automáticamente
4. **Excel Export**: Incluye Gastos Operativos y Ganancias Netas

---

*Última actualización: Diciembre 2024*
