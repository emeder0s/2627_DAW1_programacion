# PASO A PASO

## Creación de un repositorio
### De remoto a local
1. Creamos un repositorio remoto en GitHub:
    **IMPORTANTE!!** El nombre del repositorio no debe tener espacio en blanco. Por otro lado, debe estar estar **checkeada** la opción de añadir un fichero README.

2. Copiamos la url del repositorio. Esta url podemos copiarla al hacer clic en el botón Code que podemos encontrar en la página principal de nuestro repositorio.

3. Abrimos un terminal (cmd, git bash, el terminal de VSC...) en la ruta donde queremos clonar el repositorio local. 

4. Ejecutamos el siguiente comando: 
```
    git clone <url>
```
donde **url** es es la url del repositorio que hemos copiado. 

5. Una vez clonado el repositorio ya podemos empezar a crear ficheros en nuestro repositorio. 


### De local a remoto
1. Abrimos un terminal con la ruta de la carpeta que queremos que sea un repositorio. Esta carpeta puede estar vacía (ya que estamos iniciando un proyecto) o puede tener ficheros. 

2. Ejecutamos el comando para iniciar un repositorio:
```
    git init
```

2. Creamos un repositorio vacío en GitHub. En este caso, no hay que añadir el fichero README. 

3. Ejecutamos los siguientes para configurar el repositorio remoto
```
    git remote add <name> <url>
```
donde **name** es el nombre que le queramos dar al repositorio remoto, como por ejemplo *origin*, donde **url** es la url del repositorio.

4. Necesitamos renombrar la rama master que se ha creado con el comando de git init. Para ello ejecutamos el siguiente comando:
```
    git branch -M main
```
5. En ese punto, ya podremos empezar a crear ficheros y a trabajar en nuestro proyecto. Tendremos que añadir y confirmar los cambios antes de hacer el push. Por último para hacer el primer push necesitaremos configurar la rama remota:
```
    git push --set-upstream origin main
```

## Añadir y confirmar cambios
Cuando añadimos ficheros nuevos o modificamos alguno  ya existente en nuestro repositorio local antes de enviarlos al repositorio remoto debemos ejecutar los siguientes comandos:
```
    git add <fichero>

    git commit -m "mensaje descriptivo"

    git push
```

## Eliminar archivos
Cuando eliminamos un fichero en vez de usar el comando git add, debemos usar el comando:
```
    git rm <fichero>
```
OJO! Este comando elimina  eliminar archivos del área de trabajo y del índice (staging area) al mismo tiempo!!!

Los ficheros eliminados, son cambios en el proyecto, por tanto también deben ser confirmados, para ello haremos un commit despues del *git rm*. 
