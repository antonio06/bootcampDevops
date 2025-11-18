# Ejercicios

## 1. Crea mediante comandos de bash la siguiente jerarquía de ficheros y directorios

```bash
mkdir -p foo/{dummy,empty}

touch foo/dummy/file{1,2}.txt

echo "Me encanta la bash!!" 1> foo/dummy/file1.txt
```

## 2. Mediante comandos de bash, vuelca el contenido de file1.txt a file2.txt y mueve file2.txt a la carpeta empty

```bash
cat foo/dummy/file1.txt > foo/dummy/file2.txt

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

while [ $numberFile -lt 3 ]; do
        touch "foo/dummy/file${numberFile}.txt"
        ((numberFile++))
done

echo "$text" > "foo/dummy/file1.txt"

cat foo/dummy/file1.txt > foo/dummy/file2.txt

mv foo/dummy/file2.txt foo/empty
```

- Miro si tiene permisos de ejecución: `ls -l scriptEjercicio3.sh`

- Le doy permisos de ejecución al fichero `chmod +x scriptEjercicio3.sh`

- Por último ejecuto el comando `./scriptEjercicio3.sh "Este texto no es el de por defecto :D"`

## 4. Crea un script de bash que descargue el contenido de una página web a un fichero y busque en dicho fichero una palabra dada como parámetro al invocar el script

Pasos:

- Creo el fichero con el comando `touch scriptEjercicio4.sh`

- Con vim edito el fichero

```bash
#!/bin/bash

url="https://bonviveur.com/es/recetas/patatas-aplastadas-al-horno"

word=${1}

if [ -z "$word" ]; then
    echo "No se ha informado la palabra a buscar"
    exit 1
fi

curl -s "$url" | sed 's/<[^>]*>//g' > resultPage.txt

count=$(grep -o -i -E "${word}(s)?" resultPage.txt | wc -l)

if [ "$count" -gt 0 ]; then
    echo "La palabra '$word' aparece $count veces"
    echo "Número de la primera línea donde aparece: " grep -i -n -m 1 -E "${word}(s)?"  resultPage.txt | cut -d: -f1 " veces"
else
    echo "No se ha encontrado la palabra '$word'"
fi

rm resultPage.txt
```

- Miro si tiene permisos de ejecución: `ls -l scriptEjercicio4.sh`

- Le doy permisos de ejecución al fichero `chmod +x scriptEjercicio4.sh`

- Por último ejecuto el comando `./scriptEjercicio4.sh patata`

## 5. OPCIONAL - Modifica el ejercicio anterior de forma que la URL de la página web se pase por parámetro y también verifique que la llamada al script sea correcta

Pasos:

- Creo el fichero con el comando `touch scriptEjercicio5.sh`

- Con vim edito el fichero

```bash
#!/bin/bash

url=${1}
word=${2}

if [[ $# -ne 2 ]]; then
    echo "Se necesitan únicamente dos parámetros para ejecutar este script"
    exit 1
fi

curl -s "$url" | sed 's/<[^>]*>//g' > resultPage.txt

count=$(grep -o -i -E "${word}(s)?" resultPage.txt | wc -l)

if [ "$count" -gt 0 ]; then
    echo "La palabra '$word' aparece $count $( [ "$count" -eq 1 ] && echo "vez" || echo "veces" )"

    first_line=$(grep -i -n -m 1 -E "${word}(s)?" resultPage.txt | cut -d: -f1)
    echo "Número de la primera línea donde aparece: $first_line"
else
    echo "No se ha encontrado la palabra '$word'"
fi

rm resultPage.txt
```

- Miro si tiene permisos de ejecución: `ls -l scriptEjercicio5.sh`

- Le doy permisos de ejecución al fichero `chmod +x scriptEjercicio5.sh`

- Por último ejecuto el comando `./scriptEjercicio5.sh https://bonviveur.com/es/recetas/patatas-aplastadas-al-horno patata`
