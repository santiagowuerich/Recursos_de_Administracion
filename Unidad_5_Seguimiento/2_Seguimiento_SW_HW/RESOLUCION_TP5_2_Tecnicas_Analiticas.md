# TRABAJO PRÁCTICO N° 5.2: “SEGUIMIENTO DE SI/TI: Técnicas Analíticas”
**Universidad Tecnológica Nacional - Facultad Regional Resistencia**  
**Ingeniería en Sistemas de Información | Administración de Sistemas de Información (4° Nivel)**  
**Ciclo Lectivo: 2026**

---

## 👨‍💻 Datos del Alumno / Grupo
* **Asignatura:** Administración de Sistemas de Información
* **Unidad Temática:** Unidad V: Seguimiento de SI/TI (Evaluación del Rendimiento de Sistemas Informáticos)
* **Fecha de Entrega:** Miércoles 30/09/2026

---

# CONSIGNA 1: Marco Teórico & Homologación de Simbología

### 1.a) Variables Operacionales Básicas
Las variables operacionales básicas son magnitudes obtenidas mediante observación directa en un período de medición determinado.

| Magnitud / Concepto | Simbología Puigjaner et al. (1995) | Simbología Molero et al. (2004) | Simbología Cátedra AdmSI | Unidad de Medida | Definición Operacional |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Tiempo de Observación** | $T$ | $T$ | $T$ | Segundos (s) / Minutos | Duración total de la sesión de monitorización y captura de datos. |
| **Peticiones Llegadas** | $A$ | $A$ (o $C_{in}$) | $A$ | Peticiones / Transacciones | Número total de solicitudes que ingresan al sistema durante el período $T$. |
| **Peticiones Completadas** | $C$ | $C$ (o $C_{out}$) | $C$ | Peticiones / Transacciones | Número de solicitudes procesadas y despachadas exitosamente durante $T$. |
| **Tiempo Ocupado del Recurso** | $B$ | $B$ | $B$ | Segundos (s) / Minutos | Tiempo total durante el cual el componente estuvo efectivamente ocupado ($B \le T$). |
| **Peticiones en el Sistema** | $N$ | $N$ (o $\bar{N}$) | $N$ | Peticiones / Clientes | Número medio de peticiones presentes en el sistema (en servicio o en cola). |

---

### 1.b) Variables Operacionales Deducidas
Son magnitudes derivadas matemáticamente a partir de las variables básicas:

| Magnitud / Concepto | Simbología Puigjaner | Simbología Molero et al. | Fórmula de Cálculo | Unidad | Interpretación Operacional |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Tasa de Llegadas** | $\lambda$ | $\lambda$ | $\lambda = \frac{A}{T}$ | Peticiones / seg | Frecuencia media con la que arriban nuevos trabajos al sistema. |
| **Productividad (Throughput)** | $X$ | $X$ | $X = \frac{C}{T}$ | Peticiones / seg | Ritmo real de trabajo completado y despachado por unidad de tiempo. |
| **Utilización del Recurso** | $U$ | $U$ | $U = \frac{B}{T}$ | Adimensional ($0 \le U \le 1$) o $\%$ | Fracción de tiempo que el recurso está ocupado prestando servicio. |
| **Tiempo Medio de Servicio** | $S$ | $S$ | $S = \frac{B}{C}$ | Segundos / petición | Tiempo promedio de cómputo exclusivo requerido para procesar una petición. |
| **Tiempo Medio de Respuesta** | $R$ | $R$ | $R = \frac{W}{C}$ | Segundos / petición | Tiempo total transcurrido desde que una petición ingresa hasta que se completa ($R = W_q + S$). |

---

### 1.c) Leyes Operacionales Fundamentales

1. **Ley de Utilización:**
   $$U = X \cdot S$$
   *Demostración:* $U = \frac{B}{T} = \frac{C}{T} \cdot \frac{B}{C} = X \cdot S$.  
   *Significado:* La utilización de un recurso es directamente proporcional al producto entre su productividad y el tiempo que requiere atender cada solicitud.

2. **Ley de Little:**
   $$N = X \cdot R$$
   *Significado:* El número medio de peticiones presentes en un sistema en equilibrio ($N$) es igual a la productividad del sistema ($X$) multiplicada por el tiempo medio de permanencia/respuesta ($R$).

3. **Ley del Tiempo de Respuesta Interactivo (Ley de Pensamiento):**
   $$R = \frac{N}{X} - Z$$
   Donde:
   * $N$: Número de usuarios o terminales interactivas concurrentes.
   * $X$: Productividad global del sistema interactivo (peticiones/seg).
   * $Z$: Tiempo medio de pensamiento del usuario (*think time*), tiempo que transcurre antes de emitir la siguiente consulta.
   * $R$: Tiempo medio de respuesta del servidor percibido por el usuario.

4. **Ley de Flujo Forzado:**
   $$X_k = V_k \cdot X_0$$
   Donde $X_k$ es la productividad del componente $k$, $V_k$ es el número medio de visitas al recurso $k$, y $X_0$ es la productividad global del sistema.

5. **Demanda de Servicio:**
   $$D_k = V_k \cdot S_k = \frac{U_k}{X_0}$$
   Representa el tiempo total acumulado de servicio que una transacción individual demanda al recurso $k$.

---

### 1.d) Ley de Amdahl
* **Formulación Matemática:**
  $$S_{\text{global}} = \frac{1}{(1 - f) + \frac{f}{k}}$$
  Donde:
  * $f$: Fracción del tiempo de ejecución que se ve beneficiada por la optimización ($0 \le f \le 1$).
  * $k$: Factor de aceleración local aplicado a dicha fracción ($k > 1$).
  * $S_{\text{global}}$: Ganancia o aceleración general (*Speedup*) del sistema completo.

* **Límite Asintótico:**
  $$\lim_{k \to \infty} S_{\text{global}} = \frac{1}{1 - f}$$
* **Análisis de Impacto:** La Ley de Amdahl demuestra que el factor limitante de la optimización es la parte no mejorada $(1 - f)$. Por ejemplo, si una tarea pasa el 80% de su tiempo en base de datos ($f = 0,8$) y el 20% en CPU ($1 - f = 0,2$), por más que compremos un procesador infinitamente rápido ($k \to \infty$), la aceleración máxima posible del sistema nunca superará $1 / 0,2 = 5\times$.

---
---

# CONSIGNA 2: Resolución de Ejercicios Prácticos

---

### 2.a) Servidor Web de la Plataforma "Mi Correo"
**Datos del Enunciado:**
* Período de medición ($T$): 30 minutos $= 30 \times 60 = 1.800\text{ segundos}$.
* Peticiones llegadas ($A$): $450\text{ peticiones}$.
* Peticiones completadas ($C$): $400\text{ peticiones}$.
* Tiempo ocupado ($B$): 28 minutos $= 28 \times 60 = 1.680\text{ segundos}$.

**Cálculos:**
1. **Tasa de llegadas ($\lambda$):**
   $$\lambda = \frac{A}{T} = \frac{450\text{ pet}}{1.800\text{ s}} = \mathbf{0,25\text{ pet/seg}} \quad (15\text{ pet/min})$$
2. **Productividad ($X$):**
   $$X = \frac{C}{T} = \frac{400\text{ pet}}{1.800\text{ s}} = \frac{2}{9} \approx \mathbf{0,2222\text{ pet/seg}} \quad (13,33\text{ pet/min})$$
3. **Utilización ($U$):**
   $$U = \frac{B}{T} = \frac{1.680\text{ s}}{1.800\text{ s}} = \frac{14}{15} \approx \mathbf{0,9333} \quad (\mathbf{93,33\%})$$
4. **Tiempo medio de servicio ($S$):**
   $$S = \frac{B}{C} = \frac{1.680\text{ s}}{400\text{ pet}} = \mathbf{4,2\text{ segundos/petición}}$$

*Verificación mediante Ley de Utilización:* $U = X \cdot S = 0,2222 \times 4,2 = 0,9333$ ✅.

**Explicación del Resultado e Impacto:**
* **Impacto Operativo:** El servidor web opera al **93,33% de utilización**, superando ampliamente el umbral recomendado de seguridad operacional ($75\% - 80\%$).
* **Acumulación de Cola:** Dado que la tasa de llegadas ($\lambda = 0,25$) es mayor que la productividad de despacho ($X = 0,2222$), durante la media hora quedaron $A - C = 50\text{ peticiones sin procesar}$ acumuladas en cola, lo que genera demoras crecientes en la plataforma Mi Correo.

---

### 2.b) Asistente Virtual "Bruni" (Correo Argentino) - Escenario Normal
**Datos del Enunciado:**
* Usuarios concurrentes ($N$): $50\text{ usuarios}$.
* Tiempo de pensamiento / lectura ($Z$): $8\text{ segundos}$.
* Productividad del backend ($X$): $5\text{ peticiones/segundo}$.

**Cálculo del Tiempo Medio de Respuesta ($R$):**
Aplicando la Ley del Tiempo de Respuesta Interactivo:
$$R = \frac{N}{X} - Z = \frac{50}{5} - 8 = 10 - 8 = \mathbf{2\text{ segundos}}$$

**Explicación del Resultado e Impacto:**
* El bot responde en **2 segundos**, ofreciendo una experiencia altamente interactiva y satisfactoria para los clientes de autogestión de envíos.

---

### 2.c) Asistente Virtual "Bruni" - Pico Masivo CyberMonday
**Datos del Enunciado:**
* Usuarios concurrentes en pico ($N$): $200\text{ usuarios}$.
* Tiempo de pensamiento reducido ($Z$): $6\text{ segundos}$.
* Productividad fija del backend ($X$): $5\text{ peticiones/segundo}$.

**Cálculo del Nuevo Tiempo Medio de Respuesta ($R$):**
$$R = \frac{N}{X} - Z = \frac{200}{5} - 6 = 40 - 6 = \mathbf{34\text{ segundos}}$$

**Análisis de Aceptabilidad y Medidas de Mejora:**
* **¿Es aceptable?:** **NO, es completamente inaceptable**. Un tiempo de espera de 34 segundos por cada mensaje en un chatbot interactivo quiebra la usabilidad, genera abandono de sesión y provoca que los usuarios reintenten enviar mensajes, agravando la sobrecarga (*retry storm*).
* **Medidas para mejorarlo:**
  1. *Autoscaling Horizontal:* Desplegar réplicas automáticas del microservicio del chatbot en contenedores (Kubernetes/ECS) ante picos de concurrencia.
  2. *Caché Distribuido (Redis):* Cachear estados de tracking y respuestas frecuentes para evitar consultas reiteradas a la base de datos central.
  3. *Optimización de Consultas:* Implementar réplicas de lectura de base de datos exclusivas para consultas de seguimiento de envíos.

---

### 2.d) Fluidez en CyberMonday (Objetivo: $R = 2\text{ s}$ con $N = 200$, $Z = 6\text{ s}$)
**Datos del Enunciado:**
* $N = 200\text{ usuarios}$, $Z = 6\text{ segundos}$, tiempo de respuesta objetivo $R = 2\text{ segundos}$.

**Cálculo de la Productividad Requerida ($X$):**
Despejando $X$ de la Ley del Tiempo de Respuesta Interactivo:
$$R + Z = \frac{N}{X} \implies X = \frac{N}{R + Z} = \frac{200}{2 + 6} = \frac{200}{8} = \mathbf{25\text{ peticiones/segundo}}$$

**Explicación y Sugerencias Técnicas:**
* Para mantener la fluidez de 2 segundos ante 200 usuarios, el backend debe **quintuplicar su capacidad de procesamiento**, pasando de $5\text{ pet/s}$ a **$25\text{ pet/s}$**.
* **Sugerencia de Arquitectura:** Desplegar un clúster balanceado con un mínimo de **5 nodos/instancias réplica** detrás de un balanceador de carga Nginx/HAProxy (dado que 1 nodo procesa 5 pet/s: $5 \times 5 = 25\text{ pet/s}$).

---

### 2.e) Utilización de Segmento de Red Local
**Datos del Enunciado:**
* Productividad ($X$): $7.500\text{ paquetes/segundo}$.
* Tiempo medio de transmisión ($S$): $0,01\text{ ms} = 0,00001\text{ segundos/paquete}$.

**Cálculo de la Utilización ($U$):**
$$U = X \cdot S = 7.500\text{ paq/s} \times 0,00001\text{ s/paq} = \mathbf{0,075} \quad (\mathbf{7,5\%})$$

**Explicación del Resultado e Impacto:**
* El canal de red tiene una utilización de solo el **7,5%**. Opera de forma sumamente holgada, libre de colisiones o encolamientos, con amplia capacidad disponible para absorber tráfico adicional.

---

### 2.f) Demanda de Servicio en Red 10 Gigabit Ethernet (10GbE)
**Datos del Enunciado:**
* Ancho de banda de la red ($BW$): $10\text{ Gbps} = 10 \times 10^9\text{ bits/segundo}$.
* Petición cliente $\to$ servidor: $5\text{ paquetes} \times 1.600\text{ bytes} = 8.000\text{ bytes}$.
* Respuesta servidor $\to$ cliente: $15\text{ paquetes} \times 1.600\text{ bytes} = 24.000\text{ bytes}$.

**Cálculo del Total de Bits por Transacción:**
$$\text{Total Bytes} = 8.000\text{ B} + 24.000\text{ B} = 32.000\text{ bytes}$$
$$\text{Total Bits} = 32.000\text{ bytes} \times 8\text{ bits/byte} = 256.000\text{ bits}$$

**Cálculo de la Demanda de Servicio ($D_{\text{red}}$):**
$$D_{\text{red}} = \frac{\text{Total Bits}}{BW} = \frac{256.000\text{ bits}}{10 \times 10^9\text{ bits/s}} = \mathbf{0,0000256\text{ segundos}} = \mathbf{0,0256\text{ ms}} = \mathbf{25,6\ \mu\text{s}}$$

**Explicación del Resultado e Impacto:**
* Cada transacción cliente-servidor consume únicamente **$25,6\text{ microsegundos}$** de tiempo de transmisión en la red 10GbE. Esto evidencia que la red no representará un cuello de botella para la aplicación.

---
---

# CONSIGNA 3: Caso Aplicado de Monitorización & Benchmarking

### 1. Descripción Detallada del Entorno y la Problemática
* **Entorno:** Plataforma web transaccional de pagos y facturación electrónica para una empresa de servicios logísticos y de eCommerce. Arquitectura basada en microservicios contenerizados (Docker/Kubernetes), con API Gateway, backend en Node.js/Go y base de datos relacional PostgreSQL en servidor dedicado.
* **Problema:** Durante los días de liquidación mensual y promociones comerciales, los usuarios reportan un incremento drástico en los tiempos de respuesta al generar comprobantes y realizar pagos (de 300 ms a más de 12 segundos), acompañado de errores HTTP 504 Gateway Timeout y degradación del sistema.

### 2. Herramientas Seleccionadas
1. **Monitorización Continua del Sistema:** `sar` (System Activity Reporter) de Sysstat y `node_exporter` + **Prometheus & Grafana** para telemetría en tiempo real.
2. **Monitorización de Base de Datos:** `pg_stat_statements` y `pg_top` para métricas de queries.
3. **Herramienta de Benchmarking:** `sysbench` (módulos CPU, Memory y OLTP PostgreSQL) y `k6` para generación de carga HTTP concurrente controlada.

### 3. ¿Qué se observará o medirá con cada herramienta?
* Con `sar -u` y `sar -r`: Porcentaje de utilización de CPU (%usr, %sys, %iowait) y memoria RAM ocupada/swap libre.
* Con `sar -d` y `sar -n DEV`: Operaciones de I/O de disco (tps, await, %util) y throughput de red.
* Con `pg_stat_statements`: Consultas lentas (*slow queries*), tiempo medio de ejecución de queries y bloqueos de tablas (*locks*).
* Con `sysbench`: Capacidad máxima de transacciones por segundo (TPS), latencia percentil 95/99 y comportamiento de transferencia de memoria con distintos tamaños de bloque.

### 4. Decisiones a Tomar en Base a los Resultados
* **Si el cuello de botella es I/O de Disco en Base de Datos (%iowait > 30%, await alto):**
  * Migrar el almacenamiento a unidades NVMe de alto rendimiento.
  * Añadir índices faltantes en tablas de transacciones y particionar tablas históricas.
  * Implementar Redis para caching de consultas de lectura frecuentes.
* **Si el cuello de botella es saturación de conexiones de PostgreSQL:**
  * Implementar un Connection Pooler robusto (`PgBouncer`) para reutilizar conexiones y reducir el overhead de creación de procesos.
* **Si el cuello de botella es CPU en los microservicios de aplicación:**
  * Configurar políticas de escalamiento horizontal (Horizontal Pod Autoscaler en Kubernetes) para balancear la carga automáticamente ante aumentos de TPS.

### 5. Justificación Técnica
La combinación de **monitorización pasiva** (`sar`/`Prometheus`) permite diagnosticar el comportamiento real del sistema en producción con mínima interferencia, mientras que el **benchmarking sintético** (`sysbench`/`k6`) permite aislar componentes, determinar los límites asintóticos de saturación antes de eventos críticos y validar que las optimizaciones resuelvan efectivamente el cuello de botella.
