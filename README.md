
# CC3039 — Laboratorio 6 · **Práctica Parte 2**  
**Estabilidad por Jacobiano y Autovalores (Modelo SIR con dinámica vital)**

> Integrantes: Gabriel Paz, Davis Roldán, Jorge Lopez  
> Fecha de entrega: 2025-10-22

---

## 📌 Objetivo
Demostrar matemáticamente la **estabilidad** de los puntos de equilibrio observados en la Parte 1 del laboratorio, utilizando el **Jacobiano** del sistema SIR con dinámica vital y el cálculo de **autovalores** en:
- **ELE (Equilibrio Libre de Enfermedad)**: \((S^*, I^*) = (N, 0)\)
- **Equilibrio Endémico**: \((S^*, I^*)\) con \(I^* > 0\)

---

## 🧮 Modelo
Con \(\beta\) normalizada por \(N\) (es decir, ya incluye el factor \(1/N\)):

\[
\begin{aligned}
\frac{{dS}}{{dt}} &= \mu N - \beta S I - \mu S, \\
\frac{{dI}}{{dt}} &= \beta S I - (\gamma + \mu) I.
\end{aligned}
\]

**Número reproductivo básico** (con \(\beta\) normalizada):  
\[ R_0 = \frac{\beta N}{\gamma + \mu} \]

---

## 🔢 Parámetros usados (mismos de la Parte 1)
| Parámetro | Valor |
|---|---:|
| Población total (\(N\)) | 1000 |
| Tasa de transmisión (\(\beta\)) | 0.000500 |
| Tasa de recuperación (\(\gamma\)) | 0.1 |
| Natalidad/Mortalidad (\(\mu\)) | 0.02 |
| **R₀** | **4.1667>** |

> Con estos valores, **R₀ > 1**, por lo que el **ELE** es **inestable** y el **endémico** **existe**.

---

## 📍 Equilibrios calculados
| Equilibrio | \(S^*\) | \(I^*\) | \(R^*\) (implícito) |
|---|---:|---:|---:|
| ELE | 1000 | 0 | 0 |
| Endémico | 240.000000 | 126.666667 | 633.333333 |

> Fórmulas: \(S^* = \frac{{\gamma + \mu}}{{\beta}}\), \(I^* = \frac{{\mu (N - S^*)}}{{\beta S^*}}\).

---

## 🧩 Jacobiano del sistema
\[
J(S, I) =
\begin{{bmatrix}}
-\beta I - \mu & -\beta S \\
\beta I & \beta S - (\gamma + \mu)
\end{{bmatrix}}
\]

- En el **ELE** \((N, 0)\): autovalores \(\lambda_1 = -\mu\), \(\lambda_2 = \beta N - (\gamma + \mu) = (\gamma + \mu)(R_0 - 1)\).  
  - Si **R₀ > 1**, entonces \(\lambda_2 > 0\) ⇒ **inestable**.
- En el **endémico**: se evalúa **numéricamente** el Jacobiano y sus **autovalores**.

---

## ✅ Resumen esperado
- **ELE**: autovalor \(\lambda_2 = (\gamma + \mu)(R_0 - 1)\) confirma inestabilidad si **R₀ > 1**.  
- **Endémico**: autovalores con **parte real negativa** ⇒ **estable** (atractor).

---

## 🧠 Uso de Gen AI
**Último prompt utilizado:**  
> *“Construye un notebook para la **Práctica Parte 2** del Lab 6 (SIR con dinámica vital) que: defina el Jacobiano simbólico con `sympy`; evalúe autovalores en el **ELE (S=N, I=0)**; calcule el equilibrio **endémico** con los parámetros de la Parte 1; evalúe el Jacobiano numérico en ese punto y compute autovalores con `numpy`; e imprima claramente todos los resultados. Incluye una breve sección de análisis que interprete los autovalores.”*



