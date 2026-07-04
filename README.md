# ✈ VuelosCol — Vuelos baratos desde Barranquilla, Cartagena y Bogotá

Página web estática (GitHub Pages) que muestra las ofertas de vuelos **nacionales e internacionales** con los precios más bajos desde **Barranquilla (BAQ)**, **Cartagena (CTG)** y **Bogotá (BOG)**, con actualización automática diaria vía GitHub Actions y alertas visuales de **súper descuentos** (≥30% bajo el precio típico).

**Sitio en vivo:** https://melissagarridos.github.io/vuelos-baq/

## Características

- Tres orígenes con pestañas: Barranquilla, Cartagena y Bogotá.
- Ofertas separadas en **nacionales** (10 ciudades) e **internacionales** (17 destinos).
- Filtros por tipo de ruta y ordenamiento por descuento o precio.
- Panel de estadísticas: vuelo más barato y súper descuentos por ciudad.
- Buscador con enlaces directos a Google Flights, Skyscanner y Kayak con la ruta prellenada.
- Banner de alerta cuando hay súper descuentos en la ciudad activa.
- Bot (GitHub Actions) que consulta la API gratuita de Travelpayouts cada día a las 6:00 a.m. (Colombia) y actualiza `data/deals.json`.

## Estructura

```
vuelos-baq/
├── index.html                          # La página web
├── data/deals.json                     # Ofertas (se actualiza automáticamente)
├── scripts/update_deals.py             # Script que consulta la API (3 orígenes)
└── .github/workflows/update-deals.yml  # Automatización diaria
```

## Activar la actualización automática de precios

1. Regístrate gratis en [Travelpayouts](https://www.travelpayouts.com/) y copia tu **API token** (Perfil → API token).
2. En el repositorio: **Settings → Secrets and variables → Actions → New repository secret**
   - Name: `TRAVELPAYOUTS_TOKEN`
   - Secret: tu token
3. En la pestaña **Actions**, habilita los workflows y ejecuta "Actualizar ofertas de vuelos" manualmente (Run workflow) para probar.

Mientras no configures el token, la página muestra los datos de ejemplo de `data/deals.json`.

## Personalización

- **Orígenes**: edita `ORIGINS` en `scripts/update_deals.py` y las pestañas en `index.html`.
- **Destinos**: edita `NATIONAL` / `INTERNATIONAL` en el script y en `index.html`.
- **Umbral de súper descuento**: cambia `SUPER_DISCOUNT` en `index.html` (por defecto 30%).
- **Precios típicos** (base del % de descuento): ajusta `TYPICAL_NATIONAL` / `TYPICAL_INTERNATIONAL` en el script.
- **Horario**: cambia el `cron` en `.github/workflows/update-deals.yml`.

## Nota

Los precios son referenciales (datos en caché de Aviasales) y pueden variar al reservar.
