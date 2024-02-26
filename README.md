# Modelo de visión artificial para verificar la edad en la venta de alcohol en Good Seed

## Contacto
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andres946/)
[![Correo Electrónico](https://img.shields.io/badge/Correo%20Electrónico-andresgvelasquez8@gmail.com-red?style=for-the-badge&logo=mail.ru)](mailto:andresgvelasquez8@gmail.com)  

# Descripción 
A la cadena de supermercados Good Seed le gustaría explorar si la ciencia de los datos puede ayudarle a cumplir con las leyes sobre el alcohol, al asegurarse de no vender alcohol a personas menores de edad. Te piden que hagas esa evaluación, así que, cuando te pongas a trabajar, ten en cuenta lo siguiente:
- Las tiendas están equipadas con cámaras en el área de pago, las cuales se activan cuando una persona está comprando alcohol.
- Los métodos de visión artificial se pueden usar para determinar la edad de una persona a partir de una foto.
- La tarea, entonces, es construir y evaluar un modelo para verificar la edad de las personas.  

Para empezar a trabajar en la tarea, tienes un conjunto de fotografías de personas que indican su edad.

## Instalación de dependencias

Para instalar las dependencias necesarias para este proyecto, puedes ejecutar el siguiente comando:

```bash
pip install -r requirements.txt
```
**Nota** Esta versión de Boruta puede arrojar un error al utilizar np.float, np.int y np.bool. Basta con reemplazarlos por
float, int, bool respectivamente en el archivo donde este el error. 

# Descripción de los datos
El conjunto de datos se almacena en la carpeta `/datasets/faces/` 
- La carpeta `final_files` con 7600 fotos 
- El archivo `labels.csv` con etiquetas, con dos columnas: `file_name` y `real_age` 
Dado que el número de archivos de imágenes es bastante elevado, se evitara leerlos todos a la vez, ya que esto consumiría muchos recursos computacionales. Se creo un generador con ImageDataGenerator. 

# Objetivo
Usando una red neuronal preentrenada y los conocimiento adquiridos en el sprint 15: visión artificial se desarrollara un modelo de redes neuronales que prediga la edad de acuerdo a la imagen. 

# Plan de trabajo
- Se realizara un EDA para ver el estado de las imagenes,¿estan  color? ¿en blanco y negro? ¿estan rotada? ¿Qué formato tienen?
- Se vera la distribución de las edades. 
- Para el modelado se crearan las siguientes funciones:
  - load_train: contiene la carga de las imagenes de entrenamiento. Reescala la imagen a un formato de 0-1 para cada pixel. Tambien la rota horizontal y verticalmente, ademas de agregar una rotación de 90 grados. Finalmente genera un lote de 32 imagenes de 224 x 224 como el conjunto de entrenamiento.
  - load_test: De igual forma reescala la imagen de 0 a 1 y genera un lote de 32 imagenes de 224 x 224 como el conjunto de prueba.
  - create_model: Utiliza un RESNE50 preentrenada de tensorflow. Se añaden las salidas como una unica neurona (que predice la edad del cliente). Como función de perdida se elije Mean Absolute Error. 
  - train_model: Entrena por 20 epocas utilizando los conjuntos de entrenamiento y prueba generados anteriormente, ademas del modelo. 
  
- Estas funciones se subieron a una plataforma GPU para un entrenamiento mas rápido.
- Como resultado se obtuvo `MAE: 7.55` menor al 8 propuesto. 
  
# Conclusiones
- Se obtuvo un EAM de 7.5288, menos al propuesto (8), algunas epocas dieron hasta 7.10. Probablemente entrenarlo durante mayor tiempo hubiese dado un mejor resultado.
- Cumple la función de predecir la edad adecuadamente. 
- Rotar y voltear las imagenes funciona para mejorar el modelo.
- Podría usarse para identificar productos en la tienda. Por ejemplo frutas y verduras evitando que la persona encargada tenga que memorizar los ID's. 
- Quiza en un futuro se pueda implementar un sistema de recomendación. Si puede reconocer los clientes en vez de la edad, se ajustaría no solamente la recomendación por edad sino por gustos. 
