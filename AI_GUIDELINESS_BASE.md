# Guías de desarrollo asistido por IA

Fuente de verdad compartida para iniciar y trabajar en cualquier proyecto juntos.
Estas reglas son independientes del producto, stack, infraestructura y estructura
de carpetas. Aplicar cada regla cuando corresponda al tipo de trabajo.

## Alcance y adaptación

- Leer este documento completo antes de analizar o modificar un proyecto.
- Registrar arquitectura, comandos, idiomas del producto y decisiones particulares
  en un documento separado de guías del proyecto, sin mezclarlos con esta base.
- Las adaptaciones explícitas del proyecto prevalecen sobre esta base en su ámbito;
  las instrucciones directas del usuario y las de mayor prioridad prevalecen siempre.
- Mantener aquí las reglas generales y evitar duplicarlas en otros documentos.
- Al reutilizar esta base en otro repositorio, revisar sus instrucciones existentes
  y resolver contradicciones antes de implementar. Las copias no se sincronizan
  automáticamente entre repositorios.

## 1. Antes de implementar

- Leer las instrucciones del repositorio y revisar el estado de Git.
- Inspeccionar código, datos, componentes y documentación relacionados.
- Identificar qué reutilizar, extender o crear. Preservar cambios ajenos.
- Mantener los cambios enfocados; registrar mejoras ajenas como seguimiento.
- Evitar refactors, renombres, formateos masivos o dependencias sin relación con la tarea.

## 2. Claridad y diseño del código

- Mantener el flujo principal fácil de seguir; preferir guard clauses cuando
  reduzcan anidamientos. No fragmentar operaciones sencillas en abstracciones vacías.
- Nombrar por significado del dominio y responsabilidad. Los booleanos deben
  expresar afirmaciones o preguntas, como `isAvailable` o `canPublish`.
- Usar el mismo término para un mismo concepto en interfaz, contratos y datos.
- Separar composición, reglas de negocio y efectos. Las páginas o rutas coordinan;
  las responsabilidades específicas viven en módulos adecuados al framework.
- Encapsular integraciones externas tras fronteras claras cuando aporten aislamiento
  o testabilidad. No crear capas, interfaces o clases sin una necesidad concreta.
- Validar entradas en las fronteras de confianza y representar estados con tipos
  precisos; evitar combinaciones contradictorias de booleanos y valores ambiguos.
- Mantener contratos explícitos y tipados cuando el lenguaje lo permita. Evitar
  `any` y mantener comprobaciones estrictas en proyectos TypeScript.
- Separar cálculos y decisiones de persistencia, navegación y llamadas externas
  cuando esa separación facilite entender y probar el comportamiento.

## 3. Componentes, contenido y presentación

- Revisar componentes existentes antes de crear markup; reutilizar patrones visuales
  y semánticos equivalentes sin generalizar prematuramente.
- Las páginas componen componentes y conectan contenido. Extraer bloques con
  responsabilidad, interacción o reutilización propias.
- Separar contenido editorial y datos de negocio de la presentación; usar el CMS,
  configuración o fixtures apropiados. Los textos internos de interfaz pueden
  residir en el mecanismo de traducciones del producto.
- No inventar información real. Identificar claramente mocks y placeholders.
- No afirmar que una operación guardó o envió datos si el efecto no ocurrió.
- Mantener estado local para interacción; derivar valores en lugar de duplicarlos
  innecesariamente en estado.

## 4. Diseño y accesibilidad

- Centralizar colores, tipografía, espaciados y breakpoints compartidos en tokens
  semánticos. Seguir la solución de estilos del proyecto, sin imponer SCSS o BEM.
- Diseñar mobile-first y verificar los tamaños relevantes de móvil, tablet y escritorio.
- Reservar espacio para imágenes y contenido asíncrono para evitar saltos de layout.
- Usar HTML semántico, labels, foco visible, teclado, contraste WCAG AA y áreas
  táctiles adecuadas. Respetar `prefers-reduced-motion`.
- No depender exclusivamente de hover, color o animación para funciones esenciales.
- Usar las convenciones de navegación y renderizado del framework elegido.

## 5. Errores, datos y seguridad

- Mostrar errores claros, seguros y accionables en el idioma de la interfaz.
- Conservar contexto técnico útil en observabilidad sin exponer secretos ni datos
  sensibles. No silenciar excepciones ni devolver éxito tras un fallo.
- Validar permisos y entradas en el servidor o servicio que actúe como frontera
  de confianza; la validación del navegador mejora la experiencia y no la reemplaza.
- No versionar credenciales. Usar configuración por entorno y ejemplos sin secretos.
- Exponer únicamente los datos necesarios para cada audiencia y permiso.
- Cuando haya persistencia propia, proteger invariantes con restricciones y usar
  migraciones versionadas y transacciones coherentes para cambios relacionados.
- Cuando haya APIs, mantener semántica HTTP, contratos de error y formatos
  consistentes; coordinar cambios incompatibles y actualizar clientes y documentación.

## 6. Dependencias y verificación

- Evaluar capacidades existentes antes de añadir dependencias.
- Mantener manifiestos y lockfiles coherentes; usar instalaciones reproducibles.
  No editar lockfiles a mano ni aplicar correcciones forzadas sin revisar su impacto.
- Ejecutar las verificaciones disponibles y pertinentes: tipos, lint, build y
  pruebas según el cambio. No inventar comandos ni declarar verificaciones no ejecutadas.
- Añadir pruebas de comportamiento cuando el riesgo y la lógica lo justifiquen;
  cubrir fallos relevantes y evitar pruebas que solo repitan la implementación.
- Mantener pruebas independientes y reproducibles, sin depender de datos reales
  o servicios externos salvo integración explícitamente preparada para ello.
- No desactivar checks, ocultar errores o reducir exigencias para conseguir un resultado verde.

## 7. Documentación y entrega

- Actualizar documentación afectada junto con el cambio. Al modificar guías,
  revisar README, documentación de áreas, `docs/`, plantillas y ejemplos existentes.
- Mantener una fuente de verdad por regla; resumir y enlazar en vez de duplicar.
- Distinguir funcionalidades implementadas, propuestas y pendientes. Documentar
  contratos, intención y efectos relevantes; evitar comentarios que solo repitan código.
- Informar qué cambió, por qué, qué se verificó y qué limitaciones o placeholders quedan.
- Indicar explícitamente qué documentación revisada no necesitó cambios.

## 8. Git e idioma

- Aplicar la política de commits convencionales definida al final de este documento.
- Escribir código e identificadores técnicos en inglés; documentación y explicaciones
  del proyecto en español, salvo la política explícita del proyecto destino.
- Adaptar los textos visibles a los idiomas del producto.
- Aplicar la estrategia de ramas y PR siguiente. Los checks y el despliegue
  concretos se definen en cada proyecto.

## Commits convencionales

- Todos los commits deben seguir [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).
- El encabezado obligatorio usa el formato `<type>[optional scope]: <description>`.
- Usar `feat` para una funcionalidad o componente nuevo y `fix` para corregir un defecto. Se permiten tipos como `refactor`, `docs`, `test`, `build`, `ci` y `chore` cuando describan mejor la intención.
- El scope debe ser un sustantivo breve, en minúsculas y con guiones cuando tenga varias palabras, por ejemplo `feat(contact-details): ...`.
- La descripción debe ser breve, específica, escrita en presente imperativo y sin punto final, por ejemplo: `feat(contact-details): add reusable contact channel component`.
- El mensaje debe explicar la intención del cambio, no limitarse al nombre del archivo. Usar un body separado por una línea en blanco cuando haga falta contexto adicional.
- Los breaking changes deben usar `!` antes de `:` o un footer `BREAKING CHANGE: ...` según la especificación.
- Antes de confirmar cambios, agrupar archivos por responsabilidad para que cada commit sea coherente y pueda revisarse o revertirse de forma independiente.

## Estrategia de ramas y Pull Requests

- `main`: versión estable y fuente oficial de producción. El proyecto debe indicar
  si un merge dispara un despliegue automático; no asumirlo.
- `develop`: integración del trabajo para la próxima versión.
- No realizar commits directos, force pushes ni eliminar `main` o `develop`.
  Integrar cambios mediante PR y las validaciones aplicables.
- `feature/*`: funcionalidades; sale de `develop` y vuelve a `develop`.
- `bug/*`: correcciones no urgentes; sale de `develop` y vuelve a `develop`.
  Usar este prefijo consistentemente, sin alternarlo con `bugs/*` o `fix/*`.
- `hotfix/*`: corrección urgente de producción; sale de `main`, vuelve a `main`
  y después se sincroniza hacia `develop` mediante PR.
- `release/*`: estabilización de una versión desde `develop`; solo correcciones,
  documentación y configuración necesarias para publicar. Se integra a `main`,
  se sincroniza hacia `develop` y se etiqueta cuando corresponda.
- No mantener ramas de release permanentes. Eliminar ramas temporales después
  del merge cuando sea seguro.
- Una funcionalidad independiente destinada a producción puede salir de `main`
  excepcionalmente cuando `develop` contenga trabajo incompleto. Documentar el
  motivo en el PR y sincronizar después `main` hacia `develop`.
- Un proyecto puede adoptar un flujo más simple mediante una excepción explícita
  en sus guías; no crear ramas o infraestructura sin necesidad operativa.
- Los PR usan título Conventional Commits y la plantilla del repositorio.
  Explicar problema, resultado, validación y riesgos pertinentes; omitir secciones
  que no apliquen. No marcar verificaciones que no se ejecutaron.
- Preferir squash merge en ramas de trabajo. Conservar historial cuando aporte
  valor, especialmente en sincronizaciones de ramas permanentes.
- Resolver conversaciones y ejecutar los checks pertinentes antes del merge.
  Configurar protección de ramas cuando esté disponible; no asumir que existe.
- Cuando el usuario confirme que un PR hacia `develop` fue aprobado y mergeado,
  cambiar automáticamente el repositorio local a `develop`, actualizarlo mediante
  fast-forward y eliminar la rama local de origen si es temporal (`feature/*`,
  `bug/*` o el legado `fix/*`). No pedir una confirmación adicional para esta
  limpieza. Preservar y comunicar cambios locales sin commit que impidan realizarla;
  no eliminar la rama remota salvo solicitud explícita.
- Revisar compatibilidad, secretos, migraciones y reversión antes de producción
  según el alcance. No mezclar trabajo incompleto en un PR destinado a `main`.

## Lectura por agentes y adopción

- Cada agente debe leer su archivo de entrada, las guías del proyecto y esta base
  completa antes de desarrollar. Las instrucciones se aplican según su prioridad.
- El proyecto debe fijar la revisión de esta base mediante un commit completo.
  Leer el archivo autenticándose en el repositorio privado o usar un checkout local
  en esa revisión; un enlace por sí solo no cuenta como lectura.
- Si la base no está disponible, informar la limitación y solicitar acceso o una
  copia verificada antes de implementar. No asumir que se recuerda su contenido.
- Las reglas específicas complementan la base. Registrar cualquier adaptación
  explícita, su motivo y ámbito, sin alterar silenciosamente la regla compartida.
- Actualizar la revisión de la base mediante un cambio revisable y comprobar su
  impacto sobre las guías particulares; no seguir automáticamente una rama mutable.
