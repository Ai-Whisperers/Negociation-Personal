# Manual Operativo Predictivo (v1.1)

**Objetivo:** cerrar acuerdos rápidos sin perder margen ni control de producto.  
**Reglas base:** pedir **primer precio**; **hard‑pass interno ≥ 15**; horizonte **2 meses**; **v1** listo + **cambios** y **mantenimiento** como add‑ons; límites por **archivos/tokens/hosting**.

---

## 1) Flujo de negociación (condicionales)
- **Si el cliente da primer precio (X):**  
  → Comparar con rango 25–15. **Si X ≥ 25:** aceptar con valor agregado (onboarding+2 tickets). **Si 15 ≤ X < 25:** contraoferta **X+Δ** (Δ=3–5). **Si X < 15:** agradecer y **no** avanzar; ofrecer *Lite*.
- **Si NO da primer precio:**  
  → Proponer **tiers** S/M/L + opción *flat* bajo límites; solicitar rango de presupuesto (mín–máx) antes de cifras finales.
- **Si pide “descuento por volumen”:**  
  → Aplicar -5% solo si firma **mantenimiento 3–6 meses** o volumen de archivos > umbral (p.ej., 9 000 KB/mes).
- **Si pide “flat ilimitado”:**  
  → Aceptar solo con **límites explícitos** (tamaño de archivo, tokens/mes, tickets) + **exceso** por unidad.
- **Si exige “urgente/para mañana”:**  
  → Tarifa **express +30%** y alcance **congelado** hasta entrega.
- **Si solicita “propiedad/código” o acceso ampliado:**  
  → Ofrecer **licencia de uso** y **deploy black‑box**; publicar código **no** (salvo fee Enterprise + NDA + soporte).
- **Si pide cambios UI simples (colores/textos):**  
  → Paquete “**Ajustes Rápidos**” (≤2 h).  
  **Si pide nueva funcionalidad:** estimación por horas → propuesta formal.
- **Si solicita demo/POC:**  
  → Demo guiada + dataset ejemplo; **POC** pagada con descuento canjeable si compra.
- **Si cuestiona precio:**  
  → Mostrar hoja de costo (horas + tokens + hosting) + **valor** (tiempo ahorrado, insights listos).
- **Si intenta ampliar alcance sin costo (scope‑creep):**  
  → Registrar cambio en **Matriz de Cambios** → cotización extra.

## 2) Pricing rápido (motor mínimo)
- **Tier S:** 1 dataset/mes, tamaño mediano, 1 export, 2 tickets.  
- **Tier M:** 3 datasets/mes, tokens +50%, 3 exports, 5 tickets.  
- **Tier L:** 5 datasets/mes, tokens +120%, 6 exports, 10 tickets, priorizado.
- **Flat condicionado:** topes por **tamaño/datasets/tokens/tickets**; **exceso** a tarifa por unidad.  
- **Cálculo base:** `Precio = (Horas · Tarifa) + Tokens + Hosting + Almacenamiento + Margen`.  
  - Tarifa de referencia: **120–150k PYG/h**.  
  - Tokens/hosting según consumo; publicar métrica simple (p.ej., tokens/mes incluidos).

## 3) Entrega y aceptación
- **Si entrega dataset a tiempo:** ejecutar pipeline → **Dashboard + Export (CSV/XLSX)** → check de aceptación.  
- **Si NO entrega dataset:** reprogramar hito; alquiler de horas no utilizadas **no reembolsable**.  
- **Criterio de aceptación:** dashboard visible + 1 export sin errores + checklist firmado.

## 4) Postventa & soporte
- **SLA opcional:** respuesta 24–48 h (S/M), 8–24 h (L/Enterprise).  
- **Si piden soporte extra:** bolsa de horas pre‑pagadas.  
- **Si retrasan pago:** suspender exportaciones y soporte; backup de cortesía 7 días.  
- **Reembolsos:** solo por falla reproducible no corregida en 7 días.

## 5) Riesgos & mitigación
- **CEM/NOC inquisitivo (riesgo de “robo de producto”):** **black‑box deploy**, logs firmados, **claves rotadas**, acceso mínimo.  
- **Conectividad/ruido:** rutas offline para cargas y reintentos.  
- **Compliance:** límites de subida, anonimización opcional, retención definida.  
- **Dirty‑playings:** todo cambio vía **Matriz de Cambios**; nada “de palabra”.

## 6) Scripts ultra‑breves (para reunión)
- “¿Podrían darnos su **primer número**? Ajustamos con límites y valor.”  
- “UI simple entra en **Ajustes Rápidos**; **features** nuevas van con estimación.”  
- “*Flat* sí, pero con **topes** claros; exceso se cobra por unidad.”  
- “Para urgencias aplicamos **express +30%** y congelamos alcance.”

## 7) Checklist relámpago
- [ ] Tiers + límites listos.  
- [ ] Hoja de costo (horas/tokens/hosting).  
- [ ] Matriz de Cambios activa.  
- [ ] Criterio de aceptación escrito.  
- [ ] Guion técnico y no‑técnico.

---

**KPI semáforo:** margen ≥ 35%, tickets dentro de tope, Δ‑alcance = 0, tiempo de ciclo ≤ 14 días.  
**Kill‑switch:** 2 violaciones de alcance o pago > 15 días → **pausa operativa** hasta regularización.
