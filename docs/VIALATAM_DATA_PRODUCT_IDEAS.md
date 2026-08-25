# 10 ideas de productos basados en datos para VíaLatam

**Contexto de negocio.** VíaLatam es la marca matriz; **ViaLatam Viagens** es la
agencia de viajes (Brasil, primer producto comercial) que busca **posicionarse
en el sector migratorio**, con foco inicial en la **migración venezolana en
Brasil, Latinoamérica y el mundo**. **ViaLatam Academy** es la línea de
formación. El diferencial no es vender un tiquete: es **acompañar el viaje
migratorio de punta a punta** (decidir destino, viajar, documentarse, instalarse,
trabajar, enviar remesas, reunificar familia).

**Fuentes de datos disponibles / accionables:**

- **Propias:** portales de proveedores y consolidadoras ya aprobados (Öner/BeFly,
  BDS, SkyTeam, Pátria, Comprar Viagem) → tarifas, inventario y rutas aéreas y
  terrestres; **reservas y CRM de clientes**; datos de **Academy** (roadmap,
  cursos, avance).
- **Públicas de migración:** Plataforma **R4V** (ACNUR/OIM), **DTM** de OIM,
  **CONARE / Operação Acolhida** (Brasil), **IBGE**, **Banco Mundial** (remesas),
  requisitos consulares por país.
- **Mercado laboral:** el dataset de este repo (`ats-scrapers`, 4.2M+ vacantes /
  63k+ empresas) para conectar migración con empleo en el destino.

> Para cada idea: **problema**, **datos que usa**, **forma del producto**,
> **valor / monetización** y **MVP**.

---

## 1. Índice de rutas y precios migratorios

- **Problema:** los corredores que usan los migrantes venezolanos (p. ej. Boa
  Vista/Manaus → São Paulo/Curitiba; Venezuela → Colombia/Perú/Chile; salidas a
  España/EE. UU.) tienen ventanas de precio y disponibilidad que la agencia hoy
  no monitorea de forma sistemática.
- **Datos:** tarifas e inventario de los portales de proveedores × ruta × fecha,
  serie de tiempo de precios; cruce con calendarios de alta demanda migratoria.
- **Producto:** panel interno de "mejor momento y mejor proveedor por corredor"
  + paquetes migratorios con precio óptimo y alertas de baja de tarifa.
- **Valor / monetización:** mejores márgenes y conversión; base para paquetes
  "reubicación" en vez de tiquete suelto.
- **MVP:** hoja/ETL que consolida tarifas de 2–3 consolidadoras para los 10
  corredores prioritarios y marca la opción más barata por semana.

## 2. Radar de demanda migratoria (dónde se mueve la diáspora)

- **Problema:** la agencia reacciona a la demanda en vez de anticiparla; no sabe
  qué corredores crecerán el próximo trimestre.
- **Datos:** R4V / DTM (OIM) sobre flujos y stock de venezolanos por país y
  ciudad, programas de regularización, datos de Acolhida/interiorización;
  combinados con las propias reservas.
- **Producto:** mapa y pronóstico de demanda por corredor (origen→destino) con
  score de crecimiento, para planear inventario, marketing y apertura de rutas.
- **Valor / monetización:** decisiones de inventario y pauta con base en
  evidencia; insumo para el reporte #10 y para alianzas B2B (ONGs, gobiernos).
- **MVP:** tablero trimestral con top-15 corredores por volumen y variación,
  cruzado con las reservas reales de VíaLatam.

## 3. Base de datos de trámites y documentación por destino

- **Problema:** el mayor dolor del migrante venezolano no es el vuelo, es el
  papeleo (visa, residencia, refugio, revalidación, pasaporte vencido) — y varía
  por país y cambia seguido.
- **Datos:** requisitos consulares/migratorios estructurados por país de destino
  para venezolanos (visa, residencia temporal, refugio, documentos aceptados),
  con fecha de verificación y fuente oficial.
- **Producto:** base de conocimiento estructurada que alimenta una **guía + un
  asistente/chatbot** "¿qué necesito para migrar a X?" y checklists por caso.
- **Valor / monetización:** captación (contenido/SEO), servicio de asesoría
  premium, y reducción de fricción en la venta del paquete.
- **MVP:** base con 8–10 destinos clave (Brasil, Colombia, Perú, Chile, España,
  EE. UU., México, Argentina) + checklist descargable por país.

## 4. Bolsa de empleo para migrantes en destino

- **Problema:** el migrante decide a dónde ir en función de dónde hay trabajo;
  la agencia puede ser el puente viaje ↔ empleo.
- **Datos:** dataset de empleos `ats-scrapers` filtrado por ciudades destino y
  roles accesibles/remotos, `is_remote`, salario y `posted_at`; cruce con
  requisitos de documentación (idea #3).
- **Producto:** tablero/boletín de vacantes por ciudad destino para la
  comunidad, como valor agregado del paquete migratorio y captación de leads.
- **Valor / monetización:** diferenciación fuerte, retención, y funnel hacia
  paquetes de reubicación; potencial alianza con empleadores/EOR.
- **MVP:** feed curado de vacantes para 5 ciudades destino (São Paulo, Bogotá,
  Lima, Santiago, Madrid) generado desde el dataset.

## 5. Calculadora de costo total de reubicación

- **Problema:** el migrante no sabe cuánto cuesta *realmente* mudarse (no solo el
  vuelo: documentos, primeros meses de vivienda, costo de vida, traslados).
- **Datos:** tarifas propias (viaje) + costo de vida/vivienda por ciudad (fuentes
  públicas) + tasas de trámites (idea #3) + remesas necesarias.
- **Producto:** calculadora interactiva "¿cuánto cuesta migrar de A a B?" que
  arma un presupuesto y termina en una cotización de VíaLatam.
- **Valor / monetización:** herramienta de captación de altísima intención;
  convierte curiosidad en lead calificado.
- **MVP:** calculadora web con 6 destinos y un desglose (viaje/documentos/
  instalación/colchón) con supuestos transparentes.

## 6. CRM y segmentación del viajero migrante

- **Problema:** un migrante no compra una sola vez: viaja, luego trae familia,
  envía dinero, se reubica de nuevo. La agencia no está capturando ese ciclo de
  vida.
- **Datos:** enriquecimiento de reservas/CRM propios por corredor, tamaño de
  grupo familiar, etapa del viaje migratorio y servicios previos.
- **Producto:** segmentación + modelo de "próximo mejor servicio"
  (reunificación familiar, tramo terrestre, seguro, remesas) con campañas
  automatizadas.
- **Valor / monetización:** aumento de LTV y recompra; marketing dirigido en vez
  de genérico.
- **MVP:** segmentación de la base actual en 4–5 perfiles y una automatización de
  seguimiento post-viaje.

## 7. Alertas de cambios regulatorios y oportunidades migratorias

- **Problema:** los picos de demanda los disparan cambios de política (nuevas
  regularizaciones, TPS, cupos, programas de Acolhida, requisitos de visa) y la
  agencia se entera tarde.
- **Datos:** monitoreo de fuentes oficiales (CONARE, gobiernos, ACNUR/OIM) y
  noticias regulatorias por país → clasificación de impacto por corredor.
- **Producto:** alertas internas + newsletter a la comunidad ("Chile abrió X",
  "nuevo trámite en Brasil") con CTA a asesoría/paquete.
- **Valor / monetización:** reacción rápida a la demanda, autoridad de marca,
  captación.
- **MVP:** monitoreo semanal manual-asistido de 6 países con boletín y registro
  de eventos etiquetados por impacto.

## 8. Índice "¿dónde me conviene migrar?" (comparador de destinos)

- **Problema:** muchos migrantes no tienen destino fijo; deciden por trabajo,
  costo, comunidad y facilidad de trámites.
- **Datos:** combinación de empleo (idea #4), costo de vida (idea #5), facilidad
  de trámites (idea #3), tamaño/redes de la comunidad venezolana (R4V) y costo de
  remesas.
- **Producto:** comparador que puntúa ciudades destino según el perfil del
  usuario y recomienda un plan de viaje VíaLatam.
- **Valor / monetización:** posiciona a VíaLatam como asesor de confianza, no
  vendedor de tiquetes; alto potencial de conversión y contenido.
- **MVP:** índice de 10 ciudades con 4 dimensiones ponderadas y una ficha por
  ciudad.

## 9. Panel de remesas y corredores financieros

- **Problema:** el migrante que viaja con VíaLatam casi siempre necesita enviar o
  recibir dinero; hoy ese valor se lo llevan terceros.
- **Datos:** corredores y costos de remesas (Banco Mundial, proveedores) por par
  origen-destino, cruzados con los corredores de viaje propios.
- **Producto:** panel de costos de remesas por corredor + base para ofrecer/
  aliar servicios financieros (partnership fintech, referidos).
- **Valor / monetización:** nueva línea de ingresos por alianzas/referidos
  alrededor de la base de clientes migrantes.
- **MVP:** tablero con costo promedio de remesas en los 8 corredores principales
  y una hipótesis de alianza.

## 10. Reporte "Estado de la Migración Venezolana" (autoridad + B2B)

- **Problema:** VíaLatam necesita autoridad de marca y una puerta a clientes
  institucionales (ONGs, gobiernos locales, empleadores, medios).
- **Datos:** agregados de todas las ideas anteriores (flujos, corredores,
  precios, empleo, costos, regulación) por trimestre y país.
- **Producto:** reporte trimestral público + widgets embebibles + versión
  ejecutiva para aliados; el activo de contenido insignia de la marca.
- **Valor / monetización:** funnel de captación (reporte con registro → leads),
  patrocinios y contratos B2B; sustenta a la matriz frente a Viagens y Academy.
- **MVP:** primer reporte de 1–2 páginas con 6 gráficos clave y formulario de
  descarga.

---

## Cómo priorizar (sugerencia)

| Horizonte | Ideas | Por qué |
|---|---|---|
| **Captación rápida** | #3, #5, #10 | Alta intención y contenido; convierten curiosidad en leads con poco esfuerzo técnico. |
| **Margen / operación** | #1, #6 | Usan datos que ya tienes (proveedores y CRM) y mejoran conversión y recompra. |
| **Diferencial migratorio** | #4, #8 | Construyen el activo único: viaje ↔ empleo ↔ mejor destino. |
| **Anticipación / B2B** | #2, #7, #9 | Anticipan demanda y abren ingresos por alianzas e institucional. |

**Recomendación de arranque:** empezar por **#3 (trámites)** y **#5
(calculadora de costo)** — son las de mayor intención de compra y menor barrera
técnica— apoyadas en **#1** (que usa datos que ya tienes de proveedores). Con esa
base, **#10** (reporte) le da autoridad a la marca matriz y alimenta las demás.

**Nota transversal:** casi todo se apoya en dos activos compartidos —
(a) una **base de corredores migratorios** (origen→destino normalizados) y
(b) la **base de trámites por país (#3)**— que conviene construir primero porque
habilitan al resto.
