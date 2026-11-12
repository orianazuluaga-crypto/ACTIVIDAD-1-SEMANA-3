# Semana 3 — Actividad 1: Encapsulamiento, Herencia y Polimorfismo

Refactor de la clase `Transaccion` de la Semana 2 para hacerla **robusta y extensible**,
aplicando los tres pilares de la POO y los principios SOLID (SRP y OCP).

## Archivos

| Archivo | Para qué sirve |
|---------|----------------|
| [`diseno_pilares_poo.py`](./diseno_pilares_poo.py) | Clase base `TransaccionBase` + clases hijas `TransaccionCredito`, `TransaccionDebito`, `TransaccionEfectivo`. |
| [`transacciones.txt`](./transacciones.txt) | Registros de ejemplo (`ID,TIPO,MONTO`). Incluye uno inválido (monto negativo) para probar el manejo de errores. |

## Qué se aplicó

- **Encapsulamiento:** el atributo `monto` es privado (`self._monto`) y se accede mediante un
  *getter* (`@property`) y un *setter* (`@monto.setter`) que **valida** que nunca sea negativo
  (`raise ValueError`).
- **Herencia:** `TransaccionBase` (padre) reúne el `__init__`, el getter, el setter y la lógica
  común. `TransaccionCredito`, `TransaccionDebito` y `TransaccionEfectivo` (hijas) la heredan sin
  repetir código.
- **Polimorfismo:** `calcular_impacto()` se define como *placeholder* en la base y se
  sobreescribe distinto en cada hija (interés, comisión fija, interés reducido). La misma
  llamada (`t.calcular_impacto()`) produce resultados distintos según el tipo de objeto.
- **OCP (Abierto/Cerrado):** agregar `TransaccionEfectivo` no modificó `TransaccionBase` ni el
  bucle principal; solo se agregó la clase hija y una línea en `crear_transaccion()`.
- **Robustez (try/except):** `leer_transacciones()` atrapa el `ValueError` del setter para que un
  dato inválido (la transacción `T005`) no detenga el programa.

## Cómo ejecutar

```bash
python diseno_pilares_poo.py
```
