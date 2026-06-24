## 4.0 Análisis de Riesgos y Gestión de Contingencias: "Closed Challenge"

En el reto cerrado (*Closed Challenge*), la pista libre de obstáculos nos permite exprimir al máximo el rendimiento del motor de tracción trasera y la velocidad de procesamiento de la cámara HuskyLens. Sin embargo, rodar a regímenes de velocidad elevados introduce riesgos dinámicos severos. 

Para asegurar el 100% de efectividad en las rondas oficiales, nuestro equipo ha mapeado la siguiente matriz de riesgos mecánicos, eléctricos y de software, aplicando soluciones de ingeniería probadas en boxes:

---

### 🚨 4.1 Matriz de Mitigación de Riesgos en Alta Velocidad

#### 1. Riesgo Dinámico: Derrape Transversal y Pérdida de Grip en Curvas (Efecto Inercia)
* **El Problema:** Al configurar el motor con un pulso PWM alto para maximizar el tiempo de vuelta, la inercia acumulada en la cola de Trivilyn 3.0 puede vencer la fricción estática de los neumáticos de caucho contra la lona de la pista. Esto provoca un sobreviraje (derrape) que saca al coche de su trayectoria ideal, haciendo que se salte las líneas de guía.
* **Nuestra Solución en boxes:** Implementamos un algoritmo de desaceleración predictiva acoplado a la dirección Ackermann. Cuando el microcontrolador detecta un ángulo de giro pronunciado a través del servo, reduce automáticamente el ciclo de trabajo del motor de PWM 190 a PWM 130 antes de entrar al ápice de la curva. Al salir de la curva, el código vuelve a inyectar potencia máxima en milisegundos, estabilizando el chasis sin perder el control.

#### 2. Riesgo Perceptivo: Saturación Lumínica y Descalibración de la HuskyLens
* **El Problema:** El cambio de iluminación ambiental en los recintos de competencia (luces LED externas, flashes de cámaras o reflejos directos en el suelo) altera radicalmente el histograma de color que lee la cámara de Inteligencia Artificial. Esto puede provocar falsos negativos al intentar reconocer las líneas de los carriles.
* **Nuestra Solución en boxes:** Diseñamos e imprimimos en PETG un capó o "parasol" físico de perfil bajo que cubre el lente de la cámara. Además, programamos un script de calibración rápida en el menú basal del robot que nos permite ajustar el umbral de ganancia y balance de blancos directamente en los fosos un minuto antes de la ronda, congelando la matriz de exposición según la luz exacta de la pista.

#### 3. Riesgo Eléctrico: Caídas de Voltaje Súbitas (*Brownouts*) en el Arduino Mega 2560
* **El Problema:** Al exigirle aceleraciones explosivas al motor de tracción, el driver L298 experimenta demandas masivas de corriente. Si la batería decae momentáneamente, este bajón de energía puede drenar la línea lógica del microcontrolador, causando un reinicio del sistema en plena marcha (*Crash del Kernel*).
* **Nuestra Solución en boxes:** Como se observa en nuestro plano eléctrico (image_dd07c1.jpg), aislamos por completo los sistemas mediante dos módulos STEP-UP independientes. El elevador de 10V absorbe los golpes de corriente del motor, mientras que el módulo de 6.5V mantiene una línea de voltaje constante, limpia y blindada para el procesador y los sensores de piso (HC-5904, HC-3904, HC-2904), garantizando que el software jamás sufra un apagón.

#### 4. Riesgo de Desgaste Mecánico: Holgura (*Backlash*) en la Caja Reductora Impresa
* **El Problema:** Tras varias rondas de pruebas continuas, la fricción cíclica en los engranajes de la caja reductora (78:1) impresa en 3D puede desgastar los dientes de PETG, generando un pequeño juego mecánico o desfase. Esto altera la respuesta del freno del motor y deforma la precisión del lazo cerrado PID.
* **Nuestra Solución en boxes:** Aplicamos lubricante de silicona de alta viscosidad para automodelismo en todo el tren de engranajes para reducir el desgaste térmico. Asimismo, el equipo viaja con tres módulos de transmisión idénticos listos para un reemplazo express de menos de dos minutos en caso de detectar pérdidas de tracción en la inspección visual de pre-carrera.

---

### 📋 4.2 Protocolo de Verificación Pre-Ronda (Checklist Obligatorio)

Antes de colocar a Trivilyn 3.0 en la línea de salida del *Closed Challenge*, ejecutamos este protocolo estricto en la mesa de trabajo:

1. **[  ] Test de Espejo de Voltaje:** Verificar que las celdas 18650 marquen un mínimo de 4.1V por celda para asegurar la curva de potencia máxima.
2. **[  ] Inspección de Pines en Cascada:** Comprobar la firmeza de las conexiones de los sensores HC y el bus serie de la cámara para mitigar fallos por vibración.
3. **[  ] Limpieza de Banda de Rodadura:** Limpiar los neumáticos de caucho con alcohol isopropílico para retirar el polvo de la pista y garantizar el agarre máximo en las curvas de alta velocidad.
4. **[  ] Calibración de Cero Angular:** Verificar que el servomotor alinee las ruedas delanteras exactamente a 90 grados respecto al eje del chasis, evitando desviaciones parásitas en las rectas limpias.

### Archivos CAD

Este repositorio contiene todos los materiales y pasos necesarios para crear a "Trivilyn3.0", el robot autónomo construido por el equipo "teamroboticacrv", con el objetivo de participar en la categoría Futuros Ingenieros en las diferentes etapas de la WRO Venezuela, en su edición de 2026.




[Archivos CAD](#Archivos-CAD)

