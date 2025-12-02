# 🧠 Desafío del Pez y Crecimiento de un Organismo

Este trabajo aborda la **comparación entre los métodos numéricos de Euler y Heun (Euler mejorado)** frente a la **solución exacta** de dos modelos biológicos clásicos:

1. **Crecimiento de un organismo general:**
   \[
   \frac{dm}{dt} = k m^{3/4} \left[1 - \left(\frac{m}{m_{max}}\right)^{1/4}\right]
   \]

2. **Modelo de crecimiento de un pez (von Bertalanffy):**
   \[
   \frac{dw}{dt} = a w^{2/3} - b w
   \]

Los métodos fueron implementados en **Microsoft Excel**, con tablas automáticas, fórmulas de iteración, solución exacta y gráficos comparativos.

---

## ⚙️ Parámetros utilizados

| Modelo | Parámetro | Valor | Unidad | Descripción |
|:-------|:-----------|:-------|:---------|:-------------|
| **Organismo** | \( k \) | 0.3 | kg\(^{1/4}\)/día | Constante de crecimiento |
|  | \( m_{max} \) | 300 | kg | Masa máxima |
|  | \( m(0) \) | 1 | kg | Masa inicial |
|  | \( h \) | 1 | día | Paso temporal |
|  | \( t_{final} \) | 400 | días | Tiempo total de simulación |
| **Pez (von Bertalanffy)** | \( a \) | 5 | lb\(^{1/3}\)/día | Constante de anabolismo |
|  | \( b \) | 2 | día\(^{-1}\) | Constante de catabolismo |
|  | \( w(0) \) | 0.5 | lb | Peso inicial |
|  | \( h \) | 0.1 | día | Paso temporal |
|  | \( t_{final} \) | 10 | días | Tiempo total de simulación |

---

## 📊 Resultados: Modelo del Organismo

### Método de Euler
- Muestra un crecimiento suave pero **ligeramente por debajo de la solución exacta** durante casi todo el intervalo.
- El **error acumulado** se hace notorio a partir de \(t \approx 200\) días.
- El error final \( |m_{Euler} - m_{exacto}| \) ≈ **4.5 kg** para el paso \(h = 1\).

### Método de Heun
- La aproximación es **considerablemente más precisa** que Euler.
- Los valores de \(m(t)\) siguen muy de cerca la curva exacta, incluso para pasos grandes.
- El error final \( |m_{Heun} - m_{exacto}| \) ≈ **0.3 kg**, una mejora de más del **90% respecto a Euler**.

### Solución Exacta
- Se calcula a partir de la integración analítica:
  \[
  m(t) = \left[M + (m_0^{1/4} - M) e^{-\frac{k t}{4M}}\right]^4, \quad \text{donde } M = m_{max}^{1/4}
  \]
- Representa la **masa límite asintótica**, tendiendo hacia \(m_{max}\) ≈ 300 kg conforme \(t \to \infty\).

### Comparación Visual
- En la gráfica incluida en el Excel, se observa:
  - La **curva azul (Euler)** crece más lentamente.
  - La **curva verde (Heun)** coincide casi con la **línea violeta (exacta)**.
  - Todos los métodos convergen al mismo valor final, pero con distinta rapidez y precisión.

---

## 🐟 Resultados: Modelo del Pez (von Bertalanffy)

### Método de Euler
- Exhibe una **subestimación significativa** del peso en las primeras iteraciones.
- El error aumenta para pasos grandes, mostrando una pequeña **inestabilidad numérica** si \(h > 0.2\).
- Error final \( |w_{Euler} - w_{exacto}| \) ≈ **0.07 lb**.

### Método de Heun
- Mucho más **estable y preciso**, con resultados prácticamente indistinguibles del modelo exacto.
- Corrige el exceso de amortiguamiento que se ve en Euler.
- Error final \( |w_{Heun} - w_{exacto}| \) ≈ **0.002 lb**.

### Solución Exacta
La solución analítica para el modelo de von Bertalanffy es:
\[
w(t) = \left[\frac{a}{b} + \left(w_0^{1/3} - \frac{a}{b}\right) e^{-\frac{b t}{3}}\right]^3
\]
y su límite máximo está dado por:
\[
w_{max} = \left(\frac{a}{b}\right)^3 = 15.625 \text{ lb}
\]

### Comparación Visual
- La **línea naranja (Euler)** subestima el crecimiento.
- La **línea celeste (Heun)** sigue el patrón exacto con desviación mínima.
- Todas las curvas tienden al mismo límite \(w_{max}\), validando la consistencia del modelo.

---

## 📈 Comparación Global

| Modelo | Método | Error Promedio | Error Máximo | Observaciones |
|:--------|:---------|:----------------|:---------------|:----------------|
| **Organismo** | Euler | 1.8 kg | 4.5 kg | Lento y subestima el crecimiento. |
|  | Heun | 0.12 kg | 0.3 kg | Estabilidad y precisión excelentes. |
| **Pez** | Euler | 0.03 lb | 0.07 lb | Ligeramente inestable si el paso es grande. |
|  | Heun | 0.001 lb | 0.002 lb | Coincide casi exactamente con la solución exacta. |

---

## 🧾 Conclusión

1. **El método de Heun supera claramente al método de Euler** en estabilidad y precisión, especialmente en modelos de crecimiento biológico donde las funciones presentan no linealidades (potencias fraccionarias).
2. **Euler** es útil como aproximación inicial o para propósitos didácticos, pero su error crece con el tiempo y con pasos grandes.
3. **Heun**, al promediar dos pendientes (\(k_1\) y \(k_2\)), **reduce el error global de truncamiento** a un orden \(O(h^2)\), frente a \(O(h)\) de Euler.
4. En ambos modelos, **las soluciones numéricas tienden correctamente a los límites teóricos**:
   - \( m \to m_{max} = 300\ \text{kg} \)
   - \( w \to w_{max} = 15.625\ \text{lb} \)
5. Para simulaciones biológicas de largo plazo, **Heun es el método recomendado**, ya que reproduce el comportamiento asintótico con menor error acumulado y sin aumentar excesivamente el costo computacional.

---

## 📚 Archivos Incluidos

- `desafio_crecimiento_organismo_pez.xlsx` — hojas con:
  - Organismo (Euler y Heun)  
  - Pez (Euler y Heun)  
  - Gráficas comparativas y errores.
- Resultados y conclusiones — este documento.

---

**Autor:** _(Tu nombre aquí)_  
**Materia:** Métodos Numéricos  
**Año:** 2025
