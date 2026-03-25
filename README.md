# 🐧 Unidad 2: Técnicas Avanzadas de Animación 2D 🎬
## 🧊 Proyecto Integrador: Walk Cycle  | Personaje Estilizado | Blender 5.0

---

### 🛠️ Tecnologías y Entorno de Desarrollo
![Blender](https://img.shields.io/badge/Blender_5.0-E87D0D?style=for-the-badge&logo=blender&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Animation](https://img.shields.io/badge/Motion_Design-4A90E2?style=for-the-badge&logo=adobe-after-effects&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)

* **Software Base:** Blender 5.0 LTS 🎨
* **Pipeline:** Modelado Poligonal, Rigging Cinético y Animación No Lineal.
* **Técnica de Referencia:** Análisis de secuencias de movimiento cuadro a cuadro.
* **Control de Versiones:** Git & GitHub para documentación técnica.

---

> [!IMPORTANT]
> **RESUMEN DEL PROYECTO:** Este repositorio documenta el desarrollo de un ciclo de caminata (*Walk Cycle*) para un modelo de bajo impacto poligonal. Se prioriza la mecánica del cuerpo, el equilibrio de masas y la correcta interpolación de curvas en el *Graph Editor* de Blender 5.0.

![](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

<div align="center">
  <h3> 🖼️ 1. Planificación de Poses (Storyboard Técnico) </h3>
</div>

El proceso comenzó con la creación de una guía de poses secuencial. Esta referencia visual permitió establecer los límites de extensión de las extremidades y el centro de gravedad del personaje antes de entrar a la fase de animación.

<div align="center">
  <img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/ba494c97-089f-404a-a990-76e9aa990a59" />

</div>

---

<div align="center">
  <h1> 🛠️ 2. Guía Paso a Paso ("How To") </h1>
</div>

Para replicar este proyecto o realizar un mantenimiento del archivo `.blend`, se deben seguir estos pasos técnicos:

### A. Preparación del Viewport
1. **Importación de Referencia:** Uso de `Empty > Image` alineada al eje X para tener una guía visual constante en la vista lateral.
2. **Escalado Real:** Ajuste del personaje a la escala métrica de Blender para asegurar que las dinámicas de gravedad funcionen correctamente.

### B. Setup de Rigging (Armature)
1. **Estructura Ósea:** Creación de una armadura con jerarquía de padres (Torso > Muslo > Pierna > Pie).
2. **Inverse Kinematics (IK):** Configuración de restricciones IK en los pies para permitir que el cuerpo baje sin que los pies atraviesen el suelo.
3. **Weight Painting:** Asignación manual de pesos para evitar deformaciones en la zona de la panza del pingüino durante la caminata.

### C. Bloqueo de Animación (Blocking)
1. **Pose de Contacto (Frame 1):** Definición de la zancada máxima.
2. **Pose de Paso (Frame 12):** Elevación de la rodilla y equilibrio sobre una sola pierna.
3. **Ciclado:** Uso del modificador *Cycles* en el editor de curvas para repetir el movimiento infinitamente sin saltos visuales.

---

<div align="center">
  <h1>  3. Especificaciones de Diseño y Materiales </h1>
</div>

Se implementó un sistema de materiales tipo "Toon Shade" para mantener una estética limpia y legible.

| Módulo | Parámetro | Valor Hex | Propiedad Física |
| :--- | :--- | :--- | :--- |
| **Capa Exterior** | Base Color | `#1A1A1B` | Specular 0.2 / Roughness 0.8 |
| **Pechera** | Subsurface | `#F9F9F9` | Difuso puro |
| **Extremidades** | Base Color | `#FF9F1C` | IOR 1.45 (Naranja Plástico) |

---

<div align="center">
  <h3> 🧬 Arquitectura de Keyframes (Timeline) </h3>
</div>

```bash
# Distribución de fotogramas clave en un ciclo de 24 FPS
01 [Contact]  -> Extensión máxima de zancada.
06 [Down]     -> Compresión del volumen (Squash).
12 [Passing]  -> Pierna de apoyo vertical.
18 [Up]       -> Extensión del cuerpo (Stretch).
24 [Contact]  -> Inversión de pies para ciclo continuo.
```
<div align="center">
  <h1> 🛠️ Guía de Ejecución Técnica ("How To") </h1>
  <p>Basado en el flujo de trabajo de animación profesional para ciclos de caminata.</p>
</div>

### 1. Configuración de Referencia y Escala
Antes de animar, es vital tener una base sólida. Se configuró el Viewport en modo ortográfico lateral.
* **Paso:** Importar la secuencia de poses y alinear el suelo con el eje global de Blender.
* **Ajuste:** Configurar la opacidad de la referencia al 50% para visibilidad del modelo.

<img width="1919" height="884" alt="image" src="https://github.com/user-attachments/assets/55306027-f937-4f09-adcc-9708c030b0e9" />

---

### 2. Creación de Poses Clave (Blocking)
Siguiendo el método de "Key Poses", se definieron los 4 estados fundamentales del ciclo:

1.  **Contact (Contacto):** El punto donde ambos pies tocan el suelo. Define el largo del paso.
2.  **Down (Bajada):** El punto de máxima compresión donde el cuerpo absorbe el impacto.
3.  **Passing (Paso):** El equilibrio sobre una sola pierna mientras la otra avanza.
4.  **Up (Subida):** El impulso máximo antes de caer al siguiente contacto.

<img width="841" height="238" alt="image" src="https://github.com/user-attachments/assets/51df5b41-f04a-47db-9e3c-70f89490ea79" />

---

### 3. Uso de Interpolación Constante (Step Mode)
Para evitar que Blender intente adivinar el movimiento antes de tiempo, se utilizó el modo de interpolación **Constant**.
* **Técnica:** Seleccionar todos los Keyframes en el *Graph Editor* y presionar `T > Constant`.
* **Resultado:** Esto permite ver la animación como "recortes", asegurando que cada pose sea fuerte y clara antes de suavizarla.

<img width="874" height="631" alt="image" src="https://github.com/user-attachments/assets/3cac417b-04f3-4554-8a45-6f2b9df15203" />

---

### 4. El Ciclo Infinito (Cycles F-Curve Modifier)
Para no tener que copiar y pegar poses infinitamente, se aplicó un modificador de curva:
* **Paso:** En el Graph Editor, se seleccionaron los canales de transformación y se añadió el modificador **Cycles**.
* **Beneficio:** El pingüino caminará automáticamente durante toda la duración de la línea de tiempo.

<img width="1063" height="932" alt="image" src="https://github.com/user-attachments/assets/c6db302e-2bf3-4f0c-b9fa-7c9e0624892f" />

---



<div align="center">
  <h1> 🚀 Resultado Final </h1>
  <img width="1362" height="408" alt="image" src="https://github.com/user-attachments/assets/1b09b189-fed6-4d12-9d86-3c3883ba086a" />

</div>

---

<div>
  <h2> 📚 Referencias Bibliográficas </h2>
  <ul>
    <li>Blender Foundation (2026). Blender 5.0 Reference Manual.</li>
    <li>DillonGoo (2020). <i>How to Animate in Blender</i> [Video Tutorial].</li>
    <li>Williams, R. (2001). The Animator's Survival Kit.</li>
  </ul>
</div>

<div align="center">
  <sub>Ingeniería en Sistemas Computacionales | Unidad 2 | Tecnológico de Cuautla</sub>
</div>

