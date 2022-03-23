# Actividad dirigida 2

Para la actividad dirigida 2, lo primero que realizamos es importar la librería requests para bajarnos la página web de donde queremos extraer los datos y luego importamos la librería BeautifulSoup para interpretar el código HTML.
Estos son los otros pasos:
* Se deben establecer las variables como la URL que en este caso es del [El Pais](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/), que dirige a un medallero de los Juegos de Tokio 2020 y que será la página a la que realizaremos en scraping.
* *Realizamos la petición a la web* se define que si el estatus code no es 200 no se puede leer la página. En caso de que si sea 200, se imprime en la página **"vamos a por ello"**
* Después, pasamos el contenido HTML de la web a un objeto 'BeautifulSoup()'', que representa al árbol de objetos Python resultante de parsear el documento HTML de entrada.
* Definimos las variables países, oros, plata, bronce, total, etc y las identificamos con la función `find_all()`, para obtener todas las etiquetas que cumplan con las condiciones del objeto HTML.
* Se realiza la pregunt: ¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n'. En caso de que la persona presione `s`, se imprimirá la frase **"De acuerdo"**
* Bucle para obtener los datos: finalmente para obtener los datos realizaremos un bucle for, es decir, repetiremos el bloque de instrucciones en un rango de 20 veces. ya que estas han sido determinadas previamente a través del código `for i in range (20)`.
Una vez y se excesa el número de intentos, la página imprimirá **Qué lástima, y...**

```
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')
´´´
