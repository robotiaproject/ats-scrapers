# 10 ideas de productos basados en datos para VíaLatam

Estas ideas se apoyan en el dataset de `ats-scrapers`: **4.2M+ vacantes vivas**,
**63,000+ empresas** y **49 fuentes** (Workday, Greenhouse, Lever, Ashby,
SmartRecruiters, SuccessFactors, etc.), normalizadas en un esquema único con
rol, empresa, ubicación y geo (`country_iso`, `region`, `lat`/`lon`), salario
(`salary_min`/`salary_max`/`currency`/`period`), remoto (`is_remote`),
seniority (`experience`), departamento/equipo, fecha de publicación
(`posted_at`) e idioma. El enfoque es **Latinoamérica**: talento tech,
nearshoring y movilidad laboral.

> Para cada idea: **problema**, **datos que usa**, **forma del producto**,
> **cliente / monetización** y **MVP**.

---

## 1. Índice de demanda de talento tech LatAm

- **Problema:** no existe un termómetro público y confiable de cómo evoluciona
  la contratación tech por país, rol y seniority en la región.
- **Datos:** `posted_at` (serie de tiempo) × `country_iso`/`region` × `title`
  normalizado × `experience`. Conteo de vacantes por semana/mes.
- **Producto:** índice mensual (base 100) por país y familia de rol, con
  dashboard interactivo y descarga CSV.
- **Cliente / monetización:** medios, gobiernos, VCs, prensa (lead gen +
  suscripción a la serie histórica y a la API).
- **MVP:** notebook que agrega el dataset por país/mes/rol y publica 3–4
  gráficos + un CSV versionado.

## 2. Radar de nearshoring

- **Problema:** empresas de EE. UU./Europa contratan cada vez más talento
  remoto elegible para LatAm, pero esa señal está dispersa entre 49 fuentes.
- **Datos:** `is_remote`, texto de `description` (menciones de "LATAM",
  "remote — Americas", zonas horarias), `company`, `posted_at`.
- **Producto:** lista viva de empresas y roles "LatAm-eligible", con filtros
  por rol, timezone y crecimiento de headcount.
- **Cliente / monetización:** candidatos (freemium), bootcamps y staffing
  (suscripción), employer branding.
- **MVP:** clasificador de elegibilidad LatAm sobre `is_remote` + reglas de
  texto; ranking de las 100 empresas que más publican roles elegibles.

## 3. Benchmark salarial LatAm

- **Problema:** los rangos salariales tech en la región son opacos y
  fragmentados.
- **Datos:** `salary_min`/`salary_max`/`salary_currency`/`salary_period`
  cruzados con `title`, `experience`, `country_iso` y `is_remote`.
- **Producto:** explorador de percentiles (p25/p50/p75) por rol × seniority ×
  país, normalizado a USD, distinguiendo local vs. remoto internacional.
- **Cliente / monetización:** áreas de People/Compensación, reclutadoras,
  candidatos (informe premium + API de benchmarking).
- **MVP:** normalización de moneda y periodo a USD/año y tablas de percentiles
  para los 15 roles con mayor cobertura salarial.

## 4. Alertas de empresas en expansión (hiring signals)

- **Problema:** equipos de ventas B2B y de reclutamiento no detectan a tiempo
  qué empresas están escalando su contratación.
- **Datos:** derivada de volumen de vacantes por `company` y `department` en el
  tiempo (`posted_at`); picos y nuevas aperturas por área/país.
- **Producto:** alertas ("Empresa X abrió 20 roles de Ingeniería en México
  este mes") vía email/Slack/webhook, con score de momentum.
- **Cliente / monetización:** ventas B2B, agencias de talento, proveedores SaaS
  (suscripción por alertas + créditos de API).
- **MVP:** job diario que compara conteos por empresa vs. media móvil y dispara
  las anomalías top.

## 5. Mapa de skills demandadas y skills emergentes

- **Problema:** universidades, bootcamps y ministerios de trabajo carecen de
  evidencia actualizada de qué habilidades pide el mercado.
- **Datos:** extracción de skills desde `description` (NLP/LLM) × `country_iso`
  × `posted_at` × `title`.
- **Producto:** dashboard de skills con tendencia (en alza/baja), co-ocurrencia
  de habilidades y "brechas" por rol.
- **Cliente / monetización:** edtech, sector público, RR. HH. (informes,
  licencias de datos, contenido co-branded).
- **MVP:** diccionario de ~300 skills + extracción por regex/embeddings sobre un
  muestreo, con top 20 skills en alza por país.

## 6. Job board curado remote-first para LatAm

- **Problema:** los grandes portales están saturados de vacantes no elegibles o
  duplicadas para el talento latinoamericano.
- **Datos:** dataset completo filtrado por elegibilidad LatAm (idea #2),
  deduplicado por `url`/`global_id`, con `apply_url` directo.
- **Producto:** portal + newsletter con vacantes verificadas remote-friendly,
  filtros por rol/timezone/salario en USD.
- **Cliente / monetización:** candidatos (gratis), empresas (destacar vacantes),
  afiliación/partners de reubicación.
- **MVP:** feed estático generado desde el dataset con 500 vacantes curadas y
  suscripción por email.

## 7. Score de "remote-friendliness" y elegibilidad por vacante

- **Problema:** un candidato en LatAm no sabe si una vacante remota realmente lo
  acepta desde su país.
- **Datos:** `is_remote` + señales de `description` (país permitido, contratación
  vía contractor/EOR, timezone) → modelo de scoring 0–100.
- **Producto:** API/librería que enriquece cualquier vacante con un
  `latam_eligibility_score` y las razones detectadas.
- **Cliente / monetización:** job boards, EOR/payroll (Deel-like), HR-tech
  (API por volumen).
- **MVP:** función de scoring basada en reglas + validación manual sobre 200
  vacantes etiquetadas.

## 8. API y dataset normalizado para HR-tech y reclutadoras

- **Problema:** construir y mantener scrapers de 49 fuentes es caro; muchas
  empresas solo quieren datos limpios y frescos.
- **Datos:** todo el esquema normalizado (`docs/JOB_SCHEMA.md`) más búsqueda por
  rol/ubicación/salario/remoto.
- **Producto:** API comercial + snapshots Parquet con SLA de frescura, filtrada a
  mercados/roles LatAm.
- **Cliente / monetización:** ATS, marketplaces de talento, agencias
  (suscripción por asientos/volumen + tier enterprise con histórico).
- **MVP:** endpoint de búsqueda sobre el snapshot Parquet con auth por API key y
  cuotas.

## 9. Firmographics y enriquecimiento de empresas para ventas

- **Problema:** los equipos comerciales necesitan señales accionables sobre las
  63k+ empresas (qué stack de contratación usan, en qué crecen).
- **Datos:** `company` × `ats_type` (qué ATS usa) × distribución de
  `department`/`country_iso` × tendencia de headcount (vacantes en el tiempo).
- **Producto:** ficha enriquecida por empresa (ATS, áreas que contrata, países,
  momentum) exportable a CRM.
- **Cliente / monetización:** SaaS que le vende a RR. HH. (p. ej. quien vende un
  add-on de Workday), agencias, ABM (créditos de enriquecimiento).
- **MVP:** tabla empresa→ATS→áreas→países desde el directorio + conteos, con
  export CSV.

## 10. Reporte de tendencias del mercado laboral LatAm (content & lead gen)

- **Problema:** VíaLatam necesita autoridad de marca y captación orgánica en un
  mercado ruidoso.
- **Datos:** agregados trimestrales de todas las ideas anteriores (demanda,
  salarios, skills, nearshoring, remoto) por país.
- **Producto:** informe trimestral "Estado del Talento Tech en LatAm" + widgets
  embebibles y dashboard público con datos destacados.
- **Cliente / monetización:** funnel de captación (gated report → leads),
  patrocinios, base para upsell a la API (#8) y benchmark (#3).
- **MVP:** primer informe de una página con 6 gráficos clave y formulario de
  descarga.

---

## Cómo priorizar (sugerencia)

| Horizonte | Ideas | Por qué |
|---|---|---|
| **Rápido / marketing** | #1, #10 | Alta visibilidad, bajo esfuerzo, generan tráfico y leads. |
| **Monetización directa** | #3, #8, #9 | Clientes B2B con disposición a pagar por datos limpios. |
| **Producto core LatAm** | #2, #6, #7 | Construyen el activo diferencial: elegibilidad y curaduría. |
| **Datos avanzados** | #4, #5 | Requieren NLP/series de tiempo; alto valor a mediano plazo. |

**Base técnica común:** todas se construyen sobre el mismo pipeline —
normalización del esquema `Job`, filtro de elegibilidad LatAm, y agregaciones
por país/rol/tiempo— por lo que conviene invertir primero en esa capa
compartida (ideas #2 y #7 son habilitadoras del resto).
