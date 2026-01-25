📖 Manual de Instalación de Nuevas Investigaciones
Introducción
Este manual te guía paso a paso para añadir una nueva investigación de una empresa al portal de Investment Research. El proceso es simple y solo requiere seguir 4 pasos principales.

✅ Requisitos Previos
Antes de comenzar, asegúrate de tener:

Una carpeta con los archivos HTML de tu investigación (como puuilo/index.html)

Acceso a GitHub (o tu repositorio)

Los datos clave de la empresa:

Ticker (símbolo de la bolsa, ej: PUUILO.HE)

Nombre de la empresa

Sector

Fair Value (valuación)

Precio Actual

Upside % (potencial de ganancia)

Nivel de Riesgo

Tipo de inversión (ver tabla abajo)

📋 Tipos de Inversión Disponibles
Cada investigación debe asignarse a UNO de estos tipos:

Tipo	Código	Icono	Descripción
Long Value-Growth	long-value-growth	📈	Compañías con crecimiento sólido y valuación atractiva
Spin-offs	spin-offs	🔀	Separación de unidades de negocios
Short Situations	shorts-situations	⬇️	Oportunidades de venta corta
Uplisting	uplisting	⬆️	Cambios de bolsa o índice
Demergers	demergers	📊	Escisiones y separaciones de empresas
Tender Offers	tender-offers	🎯	Ofertas públicas de compra
Turnaround	turnaround	🔄	Empresas en recuperación
Takeover	takeover	🏢	Adquisiciones y fusiones
Odd Lots	odd-lots	🎲	Pequeños números de acciones
🚀 PASO 1: Preparar el archivo HTML de la investigación
Estructura de carpeta recomendada:
text
SpreadHunters.researchs/
├── index.html (página principal)
├── puuilo/
│   └── index.html (investigación de Puuilo)
├── [nueva-empresa]/
│   └── index.html (tu nueva investigación)
Requisito OBLIGATORIO en el HTML:
Tu archivo index.html DEBE contener estos elementos ocultos para que funcione la integración:

xml
<!-- METADATOS PARA EL INDEX (estos elementos serán leídos por index.html) -->
<div style="display: none;">
    <span data-ticker="EMPRESA.XX"></span>
    <span data-company="Nombre de la Empresa"></span>
    <span data-sector="Sector"></span>
    <span data-fair-value="€XX,XX"></span>
    <span data-risk-level="Bajo/Medio/Alto"></span>
    <span data-analysis-date="Mes Año"></span>
</div>
⚠️ IMPORTANTE: Coloca estos datos al inicio del <body>, ANTES de cualquier otro contenido visible.

Ejemplo real (Puuilo):
xml
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    ...
</head>
<body>
    <!-- METADATOS PARA EL INDEX -->
    <div style="display: none;">
        <span data-ticker="PUUILO.HE"></span>
        <span data-company="Puuilo"></span>
        <span data-sector="Retail - Home Décor & Hobby"></span>
        <span data-fair-value="€26,62"></span>
        <span data-risk-level="Medio"></span>
        <span data-analysis-date="Enero 2026"></span>
    </div>

    <header>
        <h1>🏪 PUUILO OYJ - EQUITY RESEARCH</h1>
        ...
    </header>
    
    <!-- Resto del contenido -->
</body>
</html>
📤 PASO 2: Subir la carpeta a GitHub
Opción A: Usar GitHub Web (Más Fácil)
Ve a tu repositorio: https://github.com/tu-usuario/SpreadHunters.researchs

Haz clic en "Add file" → "Create new file"

En la ruta, escribe: nombre-empresa/index.html (GitHub creará la carpeta automáticamente)

Pega el contenido de tu HTML

Haz clic en "Commit changes" con mensaje: Add: Análisis de [Nombre Empresa]

Opción B: Usar Git desde terminal (Para usuarios avanzados)
bash
# 1. Clona el repositorio
git clone https://github.com/tu-usuario/SpreadHunters.researchs.git
cd SpreadHunters.researchs

# 2. Crea la carpeta
mkdir nombre-empresa

# 3. Copia tu archivo HTML
cp tu-archivo.html nombre-empresa/index.html

# 4. Sube a GitHub
git add nombre-empresa/
git commit -m "Add: Análisis de [Nombre Empresa]"
git push origin main
🔧 PASO 3: Actualizar el archivo index.html principal
Ubicación:
/index.html (en la raíz del repositorio)

Encuentra esta sección:
javascript
const researchesData = [
    {
        id: 'puuilo',
        path: './puuilo/index.html',
        type: 'long-value-growth',
        ticker: 'PUUILO.HE',
        company: 'Puuilo',
        sector: 'Retail - Home Décor',
        fairValue: '€26,62',
        currentPrice: '€12,52',
        upside: '+113%',
        riskLevel: 'Medio',
        date: 'Enero 2026'
    }
    // ← AÑADE AQUÍ TU NUEVA EMPRESA
];
Añade tu empresa así:
javascript
const researchesData = [
    {
        id: 'puuilo',
        path: './puuilo/index.html',
        type: 'long-value-growth',
        ticker: 'PUUILO.HE',
        company: 'Puuilo',
        sector: 'Retail - Home Décor',
        fairValue: '€26,62',
        currentPrice: '€12,52',
        upside: '+113%',
        riskLevel: 'Medio',
        date: 'Enero 2026'
    },
    {
        id: 'telefonica',  // ← Tu nueva empresa
        path: './telefonica/index.html',  // ← Ruta a tu carpeta
        type: 'turnaround',  // ← Tipo de inversión (ver tabla)
        ticker: 'TEF.MC',  // ← Tu ticker
        company: 'Telefónica',  // ← Nombre empresa
        sector: 'Telecomunicaciones',  // ← Tu sector
        fairValue: '€3,50',  // ← Fair value
        currentPrice: '€2,80',  // ← Precio actual
        upside: '+25%',  // ← Potencial (Fair Value - Precio Actual) / Precio Actual * 100
        riskLevel: 'Medio-Alto',  // ← Bajo/Medio/Alto
        date: 'Enero 2026'  // ← Mes y año del análisis
    }
];
Guía de campos:
Campo	Formato	Ejemplo
id	lowercase, sin espacios	telefonica, nestle, tesla-inc
path	./nombre-carpeta/index.html	./telefonica/index.html
type	Código de la tabla de tipos	turnaround, long-value-growth
ticker	Símbolo de bolsa (puede incluir punto)	TEF.MC, NESN.VX, TSLA
company	Nombre completo	Telefónica, Nestlé, Tesla Inc.
sector	Industria/sector	Telecomunicaciones, FMCG, Automoción
fairValue	Con símbolo € o $	€3,50, $150,00
currentPrice	Con símbolo € o $	€2,80, $145,25
upside	Con % y signo	+25%, -10%, +150%
riskLevel	Bajo/Medio/Alto/Medio-Alto	Medio, Alto
date	Mes y año	Enero 2026, Diciembre 2025
✅ PASO 4: Verificar que funciona
Abre tu navegador: https://tu-usuario.github.io/SpreadHunters.researchs/

Espera a que cargue (puede tardar unos segundos)

Haz Ctrl + Shift + R (fuerza actualización)

Deberías ver tu nueva empresa en la tarjeta correspondiente

Si no aparece, revisa:
✓ ¿El archivo index.html principal está actualizado en GitHub?

✓ ¿La ruta en path coincide exactamente con tu carpeta?

✓ ¿El nombre de la carpeta es correcto en id?

✓ ¿Los metadatos están en el HTML de la investigación?

✓ ¿Esperaste a que GitHub Pages regenerara el sitio (puede tardar 1-2 min)?

🎨 Ejemplo Completo: Añadir "Telefónica"
Paso 1: Crear carpeta telefonica con index.html
xml
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Telefónica - Equity Research</title>
</head>
<body>
    <!-- METADATOS PARA EL INDEX -->
    <div style="display: none;">
        <span data-ticker="TEF.MC"></span>
        <span data-company="Telefónica"></span>
        <span data-sector="Telecomunicaciones"></span>
        <span data-fair-value="€3,50"></span>
        <span data-risk-level="Medio-Alto"></span>
        <span data-analysis-date="Enero 2026"></span>
    </div>

    <h1>📱 TELEFÓNICA - EQUITY RESEARCH</h1>
    <!-- Resto de tu análisis -->
</body>
</html>
Paso 2: Actualizar index.html principal
Añadir a researchesData:

javascript
{
    id: 'telefonica',
    path: './telefonica/index.html',
    type: 'turnaround',
    ticker: 'TEF.MC',
    company: 'Telefónica',
    sector: 'Telecomunicaciones',
    fairValue: '€3,50',
    currentPrice: '€2,80',
    upside: '+25%',
    riskLevel: 'Medio-Alto',
    date: 'Enero 2026'
}
Paso 3: Subir y verificar
Git → Commit → Push → Esperar 1-2 min → ¡Hecho! ✅

🔴 Checklist Final
Antes de hacer commit, verifica:

 El archivo HTML está en la carpeta correcta

 Los metadatos están presentes en el HTML (div style="display: none;")

 El index.html principal está actualizado con los datos de tu empresa

 Todos los campos están rellenos (sin campos vacíos)

 El upside es un número + %

 El type es uno de los 9 tipos válidos

 La ruta en path es correcta

❓ Preguntas Frecuentes
¿Puedo cambiar el diseño del HTML de mi investigación?
Sí. El HTML de tu investigación es completamente personalizable. Solo asegúrate de mantener los metadatos.

¿Qué pasa si me equivoco en los datos?
Edita de nuevo. Abre el archivo en GitHub, haz clic en Edit (lápiz), modifica y haz commit.

¿Cómo calculo el Upside?
text
Upside % = (Fair Value - Precio Actual) / Precio Actual * 100
Ejemplo: (€3,50 - €2,80) / €2,80 * 100 = +25%
¿Puedo añadir múltiples empresas a la vez?
Sí, pero hazlo de una en una. Así es más fácil detectar errores.

¿El sitio se actualiza automáticamente?
No. Después de hacer commit, GitHub Pages tarda 1-2 minutos en regenerar. Haz Ctrl+Shift+R después.

¿Necesito conocer programación?
No. Solo copiar-pegar y llenar los campos. Es todo muy estructurado.

📞 Soporte
Si tienes problemas:

Revisa la consola del navegador (F12 → Console) para ver errores

Verifica que los datos estén en el formato correcto

Comprueba que GitHub haya procesado el commit (espera 2 minutos)

¡Listo! Ya sabes cómo añadir nuevas investigaciones. 🚀
