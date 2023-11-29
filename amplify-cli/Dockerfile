# Usa una imagen base de Node
FROM node:14

# Etiqueta para identificar al creador/mantenedor de la imagen
LABEL maintainer="Eduardo Ortiz <eortiz@tracsa.com.mx>"

# Instala las herramientas de desarrollo requeridas (puedes agregar más si lo necesitas)
RUN apt-get update \
    && apt-get install -y git xdg-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Establece el directorio de trabajo
WORKDIR /app

# Copia el contenido del directorio actual al directorio /app dentro del contenedor
COPY ./src /app

# Instala Amplify CLI
RUN npm install -g @aws-amplify/cli

RUN amplify -v
# Exponer el puerto si es necesario
# EXPOSE 3000

# Comando por defecto para iniciar el contenedor
CMD ["bash"]
