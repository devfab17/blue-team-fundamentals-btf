# True Positive, False Positive, True Negative y False Negative

Esta parte sirve para entender qué tan bien funciona una regla de detección y cómo revisar las alertas del SOC.

| | Realmente malicioso | Realmente legítimo |
|---|---|---|
| **El sistema alerta** | True Positive (TP) | False Positive (FP) |
| **El sistema no alerta** | False Negative (FN) | True Negative (TN) |

- **TP:** detectó correctamente una amenaza.
- **FP:** generó una alerta por actividad legítima.
- **FN:** existía una amenaza, pero la detección la dejó pasar.
- **TN:** no alertó porque la actividad era legítima.

### Analogía del detector de metales

Si detecta correctamente un objeto prohibido, es TP. Si activa la alarma por algo permitido, es FP. Si ignora un objeto prohibido, FN. Si deja pasar sin alarmar a quien no llevaba nada prohibido, TN.

### Caso parecido al del video

Wazuh detecta una modificación de `/etc/passwd`. Si un atacante realizó el cambio, y la regla lo detectó, hay un TP. Si fue una tarea de administración autorizada que disparó incorrectamente una alerta de amenaza, hay un FP. **Sin investigación no podemos elegir entre ambos.**

Un falso negativo suele descubrirse mediante otras fuentes: por ejemplo, un análisis forense muestra malware que ninguna regla evaluada detectó.

## Métricas útiles (ampliación)

```text
Precisión = TP / (TP + FP)
Recall   = TP / (TP + FN)
```

La precisión indica cuántas alertas positivas fueron correctas; el recall indica qué proporción de amenazas reales detectamos. No siempre conocemos todos los FN, así que estas métricas requieren un conjunto evaluado con resultados conocidos.

## Preguntas

1. ¿Una alerta con severidad alta es necesariamente TP? **No.**
2. ¿Un evento sin alerta es necesariamente TN? **No; podría ser FN.**
3. ¿Qué problema crean demasiados FP? Consumen tiempo y pueden provocar fatiga de alertas.

**Fuente:** BTF, p. 15, más capturas del video. La matriz y las métricas están ordenadas para evitar confusiones en la explicación.
