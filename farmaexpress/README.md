# FarmaExpress — Unidad 3: Diseño arquitectural del sistema

**Curso:** Componentes de Lógica de Negocios · **Equipo 10** · FIME-UANL
**Integrantes:** Arleth García Martínez (2145524) · Ángel Mauricio Castruita Márquez (2146281) · Carlos Patricio Lozano Treviño (2147049)
**Empresa y caso:** FarmaExpress (continuación de la Unidad 2). **Proceso principal:** venta en mostrador con validación de receta, existencia, lote y caducidad, y disparo de resurtido.

## Dónde está cada entregable
| Entregable | Ubicación |
|---|---|
| Casos de uso (Etapa 1) | `docs/00-casos-de-uso.md` |
| Selección de patrón (Etapa 2) | `docs/01-seleccion-de-patron.md` |
| Mapa de dominio / DDD (Etapa 3) | `docs/02-mapa-de-dominio.md` · `diagrams/01-mapa-de-dominio.{dot,svg,png}` |
| Service Layer, Repository, Unit of Work, CQRS (Etapas 4–6) | `docs/03-service-layer-persistencia-cqrs.md` |
| Revisión SOLID (Etapa 7) | `docs/04-revision-solid.md` |
| **Diagrama de clases** | `diagrams/02-diagrama-de-clases.{dot,svg,png}` |
| **Diagramas de secuencia** | `diagrams/03-secuencia-cobro-controlado.{mmd,png}` · `diagrams/04-secuencia-receta-vencida-y-autorizacion.{mmd,png}` |
| **ADR** | `docs/adr/ADR-001…ADR-005` |
| Matriz de trazabilidad | `docs/05-trazabilidad.md` |
| Hallazgos sobre la U2 | `docs/06-hallazgos-u2.md` |
| Bitácora de IA | `docs/07-bitacora-ia.md` |
| Código base | `src/farmaexpress/{dominio,aplicacion,infraestructura}` |
| Pruebas | `tests/` |

## Cómo revisar
```bash
pip install pytest
python -m pytest -q          # 21 pruebas: casos de uso + reglas de arquitectura
```
Regenerar diagramas (opcional): `dot -Tpng -Gdpi=150 diagrams/01-mapa-de-dominio.dot -o diagrams/01-mapa-de-dominio.png` (Graphviz) y `mmdc -i diagrams/03-secuencia-cobro-controlado.mmd -o diagrams/03-secuencia-cobro-controlado.png` (Mermaid CLI).

## Estructura
```
docs/        informe por etapas, ADR, trazabilidad, hallazgos, bitácora de IA
diagrams/    fuentes (.dot, .mmd) y exportaciones (.png, .svg)
src/         dominio (reglas) · aplicacion (casos de uso, puertos) · infraestructura (implementaciones en memoria)
tests/       un escenario por caso de uso + pruebas de dependencias entre capas
```
La regla de dependencia es `infraestructura → aplicacion → dominio`, verificada automáticamente en `tests/test_arquitectura.py`.

## Supuestos pendientes de validar
FEFO como política de lote, vigencia de receta de 30 días, "sucursales cercanas" = todas las demás, `Receta` como Value Object. Ver `docs/06-hallazgos-u2.md`.
