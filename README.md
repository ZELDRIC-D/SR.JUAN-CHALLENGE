# SR.JUAN-CHALLENGE
# 📜 README - Análisis AluraStoreLatam

## 🧑💻 Explicación del Código

### 1. Configuración Inicial
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
- **Pandas**: Para manejar los datos como tablas (DataFrames)
- **Matplotlib/Seaborn**: Para crear gráficos profesionales

### 2. Carga de Datos
```python
urls = [
    "https://raw.githubusercontent.com/.../tienda_1.csv",
    # ... otras 3 URLs
]
tienda = pd.read_csv(urls[0])
```
- Carga los datos directamente desde GitHub
- `pd.read_csv()` convierte el CSV en un DataFrame manipulable

### 3. Función de Análisis
```python
def calcular_suma_precios(df, num_tienda):
    try:
        suma = df['Precio'].sum()
        print(f"Tienda {num_tienda}: ${suma:,.2f}")
        return suma
    except Exception as e:
        print(f"Error en Tienda {num_tienda}: {str(e)}")
        return None
```
- **Qué hace**: Suma todos los precios de una tienda
- **Manejo de errores**: Captura posibles problemas con los datos
- **Formato**: Muestra los resultados con separadores de miles y 2 decimales

### 4. Visualización Básica
```python
plt.figure(figsize=(10, 6))
bars = plt.bar(sumas.keys(), sumas.values())
for bar in bars:
    height = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2., height,
             f'${height:,.0f}', ha='center', va='bottom')
```
- **figsize**: Tamaño del gráfico (10x6 pulgadas)
- **bar**: Crea barras para cada tienda
- **text**: Añade el valor exacto sobre cada barra

### 5. Dashboard de KPIs
```python
fig, axes = plt.subplots(2, 2, figsize=(12, 8))
for ax, (tienda, valor) in zip(axes.flat, sumas.items()):
    ax.text(0.5, 0.7, tienda, ha='center')
    ax.text(0.5, 0.5, f'${valor:,.0f}', 
            ha='center', fontsize=18, fontweight='bold')
    ax.axis('off')
```
- **subplots**: Crea una cuadrícula 2x2
- **axis('off')**: Oculta ejes para mejor presentación
- **text**: Centra los valores numéricos en cada celda

### 6. Análisis por Categoría
```python
categorias = tienda.groupby('Categoría del Producto')['Precio'].mean()
ax = sns.boxplot(x='Categoría del Producto', y='Precio', data=tienda)
ax.set_title('Distribución de Precios por Categoría')
```
- **groupby**: Agrupa por categoría y calcula promedios
- **boxplot**: Muestra distribución estadística (medianas, quartiles)

### 7. Instrucciones de Uso
```python
# Para ejecutar el análisis completo:
# 1. Ejecutar todas las celdas de importación
# 2. Ejecutar la función de cálculo de sumas
# 3. Generar visualizaciones
# 4. Exportar resultados con:
plt.savefig('resultados.png', dpi=300, bbox_inches='tight')
```

## 🛠️ Requisitos Técnicos
```python
# requirements.txt
pandas>=1.3.0
matplotlib>=3.4.0
seaborn>=0.11.0
jupyter>=1.0.0
```

## 💡 Consejos para Modificar
1. Para cambiar estilos de gráficos:
```python
plt.style.use('ggplot')  # Otros estilos: 'seaborn', 'fivethirtyeight'
```

2. Para analizar otra tienda:
```python
tienda2 = pd.read_csv(urls[1])  # Cambiar el índice para otra tienda
```

3. Para exportar resultados:
```python
tienda.to_excel('resultados.xlsx', sheet_name='Análisis')
```

## 📝 Notas Importantes
1. El código está organizado en secciones lógicas
2. Cada visualización incluye títulos y etiquetas claras
3. Los errores están controlados con try-except

## 🚀 Ejecución Rápida
```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar Jupyter
jupyter notebook AluraStoreLatam.ipynb
```
