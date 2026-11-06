# Developer Guidelines

Fuente de verdad de mis reglas de desarrollo y colaboración con agentes de IA,
independiente del stack tecnológico. Repositorio privado.

## Estructura

- [Base normativa](AI_GUIDELINESS_BASE.md).
- [Plantilla de guías por proyecto](templates/AI_GUIDELINESS.md).
- [Entrada para Codex](templates/AGENTS.md).
- [Entrada para Claude](templates/CLAUDE.md).
- [Plantilla de Pull Request](templates/pull_request_template.md).

## Adopción en un proyecto

1. Copiar `templates/AI_GUIDELINESS.md` a la raíz del proyecto.
2. Registrar en ella el repositorio de esta base, un SHA completo y la forma de
   acceso autenticado o la ruta del checkout local. Reemplazar los placeholders.
3. Completar stack, arquitectura, comandos reales y adaptaciones del proyecto.
4. Copiar la entrada de cada agente utilizado a la raíz del proyecto.
5. Copiar la plantilla de PR a `.github/pull_request_template.md` y ajustarla.
6. Comprobar que el agente puede leer la revisión fijada de la base antes de trabajar.

La cadena de lectura es: archivo del agente → guías del proyecto → base compartida.
Cada proyecto fija su revisión para que las actualizaciones sean explícitas.
No hace falta copiar las reglas generales dentro de cada guía particular.

## Mantenimiento

Cambiar reglas generales aquí y decisiones particulares en el proyecto correspondiente.
Usar PR hacia `develop`, estabilizar y publicar hacia `main` según la base.
La creación inicial del repositorio constituye la excepción de bootstrap; después
se aplica el flujo de PR. Este repositorio documental no despliega un producto.
