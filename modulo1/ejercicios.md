# Ejercicios

## 1. Crea mediante comandos de bash la siguiente jerarquía de ficheros y directorios

```bash
mkdir -p foo/{dummy,empty}

touch foo/dummy/file{1,2}.txt

echo "Me encanta la bash!!" 1> foo/dummy/file1.txt
echo "Me encanta la bash!!" 1> foo/dummy/file2.txt
```

## 2. Mediante comandos de bash, vuelca el contenido de file1.txt a file2.txt y mueve file2.txt a la carpeta empty

```bash
cp foo/dummy/file1.txt foo/dummy/file2.txt

mv foo/dummy/file2.txt foo/empty
```

## 3. Crear un script de bash que agrupe los pasos de los ejercicios anteriores y además permita establecer el texto de file1.txt alimentándose como parámetro al invocarlo

### Pasos:

- Creo el fichero con el comando `touch scriptEjercicio3.sh`

- Con vim edito el fichero:

```bash
#!/bin/bash

mkdir -p foo/{dummy,empty}

numberFile=1
text="${1:-Que me gusta la bash!!!}"

while [ $numberFile -lt 2 ]; do
        touch "foo/dummy/file${numberFile}.txt"
        echo "$text" > "foo/dummy/file${numberFile}.txt"
        ((numberFile++))
done

cp foo/dummy/file1.txt foo/dummy/file2.txt

mv foo/dummy/file2.txt foo/empty
```

- Miro si tiene permisos de ejecución: `ls -l scriptEjercicio3.sh`

- Le doy permisos de ejecución al fichero `chmod +x scriptEjercicio3.sh`

- Por último ejecuto el comando `./scriptEjercicio3.sh "Este texto no es el de por defecto :D"`

## 4. Crea un script de bash que descargue el contenido de una página web a un fichero y busque en dicho fichero una palabra dada como parámetro al invocar el script

Pasos

- Creo el fichero con el comando `touch scriptEjercicio4.sh`

- Con vim edito el fichero

```bash
#!/bin/bash

url="https://www.bonviveur.es/recetas/patatas-aplastadas-al-horno"

curl -s "$url" > resultPage.txt

count=$(grep -o -i -E "patata(s)?" resultPage.txt | wc -l)

if [ "$count" -gt 0 ]; then
        echo "La palabra 'patata' aparece $count veces"
else
        echo "No se ha encontrado la palabra 'patata'"
fi
```

- Miro si tiene permisos de ejecución: `ls -l scriptEjercicio4.sh`

- Le doy permisos de ejecución al fichero `chmod +x scriptEjercicio4.sh`

- Por último ejecuto el comando `./scriptEjercicio4.sh
