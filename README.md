## Proyecto 1 - Notación O en el tiempo de ejecución de un algoritmo (Sucesión de Fibonacci)

Universidad del Valle de Guatemala   
Facultad de Ingeniería      
Análisis y diseños de algoritmos - Sección 30     

### Grupo 4 - Integrantes:      
- Adrian Fulladolsa Palma - 21592
- Karen Jimena Hernández Ortega - 21199
- Emilio José Solano Orozco - 21212
- Diego Alexander Hernández Silvestre - 21270
- Linda Ines Jimenez Vides - 21169
- Kristopher Javier Alvarado Lopez - 21188

### Descripción de las convenciones elegidas.
<div style="text-align: justify">
    1. Para la representación y manipulación de entradas en forma de máquinas de Turing se utilizó el proyecto 3, realizado en el curso de Teoría de Computación. Este proyecto consistió en la creación de un constructor que solicita y permite utilizar las propiedades fundamentales de una maquina tales como los estados, el alfabeto, el alfabeto de la cinta, el estado inicial, los estados de aceptación y las transiciones. De esta manera, solo se necesitó definir la estructura de la máquina de Fibonacci para poder simularla.
</div>
<br>
2. Se utilizó la siguiente máquina de Fibonacci la cual cuenta con:

    - Estados: q101, q102, q103, q104, q105, q106, q107, q108, q109, q201, q202,q203, q204, q301, q302, q303, q304, q305, q306, q307, q308, q309, q310, q311, q401, q402,q403, q404, q501, q502, q503, q601, q602, q603, q604, q701, q702, q703, q704, q801, q802,q803, q804, q805, q806, q807, q808, q809
    - 99 Transiciones
    - Los símbolos: "1","x", "*", en donde * fue reemplazado por "S"
    - Un estado inicial q0
    - Un estado final "qf" en donde "qf" fue reemplazado por qAccept
    - Un simbolo blank "b"
 [Referencia de la máquina de Fibonacci](https://www.researchgate.net/publication/1958918_Computing_Fibonacci_numbers_on_a_Turing_Machine)
### Diagrama de la máquina de Turing que calcula la sucesión de Fibonacci.
![image](https://github.com/Kojimena/P1-AA/assets/85262580/ceda9720-288a-43ec-8f21-1423fb548c49)

El siguiente diagrama fue realizado en la página [turingmachine.io](https://turingmachine.io/), la cual lee archivos ``.yaml`` y así poder crear diagramas de máquinas de Turing. Se debe recalcar que su sintaxis no acepta movimientos N o "No Move" por lo que se realizan acciones que utlizan los estados de formato 'q000N', los cuales son estados de transición donde '000' se reemplaza por el número de estado al que se quiere llegar. En cada uno de estos estados, se tiene la misma premisa: cuando se necesite pasar por uno de ellos, habrá un movimiento previo a la derecha. Los estados aceptarán cualquier elemento que esté en la cinta y lo mantendrá para después moverse a la izquierda y cambiar al estado que se quiera llegar luego del "No Move" simulado. Por ejemplo:

    q108:
        S: {write: S, R: q109N}
        1: {write: 1, L}
    q109N:
        S: {write: S, L: q109}
        1: {write: 1, L: q109}
        b: {write: b, L: q109}
        x: {write: x, L: q109}

En este caso particular, el estado q108 no debería moverse cuando tenga a 'S' en la cinta y deba cambiar al estado q109. Debido a la ausencia del elemento lógico N dentro de la sintaxis de turingmachine.io, lo que se hace es mover a q108 a la derecha y cambiar al estado q109N, donde se acepta cualquier elemento que esté a la derecha en la cinta. Este mismo elemento se sobreescribe y luego el estado mueve a la izquierda cambiando, ahora sí, al estado q109.

[Ver diagrama a detalle, junto con la simulación de la cadena '11'](https://turingmachine.io/?import-gist=b2cda674dea326f5c0252ef38b5c741c)

### Archivo con los componentes de la máquina de Turing del punto 2.
- El archivo se encuentra en "turing.json"
[Ir al archivo](https://github.com/Kojimena/P1-AA/blob/main/backend/turing.json)
### Programa en Python
 - Los componentes de la Máquina de Turing se deben configurar a través de un archivo
 [Ir al archivo](https://github.com/Kojimena/P1-AA/blob/main/backend/turing.json)
 - Debe permitir ingresar la cadena de entrada (según convención del punto 2).
    - La cadena de entrada debe ser una sucesión de ``1s`` por ejemplo, al referirnos al número ``5`` la cadena sería ``11111``
    - Las cadenas pueden probarse en el siguiente enlace [Turing machine](https://resonant-gelato-08c783.netlify.app/)

### Simulación en línea
 - Mostrar el listado de las configuraciones de la simulación, donde se indique el estado, la posición de la cabeza y los elementos de la cinta.
    - Al ingresar la cadena en [Turing machine](https://resonant-gelato-08c783.netlify.app/) y hacer click en "Run" se podrá observar la simulación de la misma en donde se indicará el estado posición de la cabeza y elementos de la cinta. Esta también puede ser probada en el archivo ``turing.py``. 
### Análisis empírico.
<div style="text-align: justify">
    La sucesión de Fibonacci consiste en una serie infinita compuesta de números enteros construida sobre la premisa de iniciar con los números 0 y 1, y sucesivamente, se van sumando los dos últimos números para generar el siguiente (Trejos, 2015). A manera de representación, la sucesión se vería de la siguiente manera:
</div>
<br>
<center>
0 - 1 - 1 - 2 - 3 - 5 - 8 - 13 - 21 - 34 - 55 - ...
</center>
<br>
<br>
<div style="text-align: justify">
    Al determinar los tiempos de ejecución que genera este algoritmo de sucesión numérica, se generó un diagrama de dispersión y la regresión polinomial, con el que se identificó que el comportamiento de la sucesión es exponencial. Esto debido a que en la implementación realizada no se cuenta con memorización, ya que los resultados calculados no se almacenan en memoria para ser utilizados posteriormente. 
    
    Con respecto al árbol de recursión tendríamos:
       
        F(n)
       /    \
    F(n-1) F(n-2)

    A manera de ejemplificación el F(3) se representa de la siguiente manera:
       
        F(3)
       /    \
      F(2)  F(1)
     /   \
    F(1)  F(1)

</div>

Con el árbol, a través de inducción:
- Base: n = 1 
- Suponemos T(n-1) = O(2^(n-1)), por lo tanto
- T(n) = T(n-1) + T(n-2) + O(1) que es igual a
- T(n) = O(2^(n-1)) + O(2^(n-2)) + O(1) = O(2^n)

Por lo que la sucesión fibonacci es exponencial debido a que al calcularla de manera recursiva sin memoización esta crece exponencialmente con n.

 - Listado de entradas de prueba usadas para medir tiempos de ejecución de la máquina.
    - La lista puede ser consultada acá: [Lista de entradas](https://docs.google.com/spreadsheets/d/1INOLNnAtr3Q88ed102KgeiYqSA2B5-xYOxnM2roUPis/edit?usp=sharing)
    - Se realizaron un total de 11 pruebas con cadenas representando los numero de 1 a 14 para la función fibonacci. Se decidió parar en 14 ya que surgieron errores de memoria por parte del programa al ingresar cadenas de 15 o más. Además consideramos que n <= 14 representa de manera precisa y correcta la complejidad de nuestro programa.
 - Diagrama de dispersión que muestre los tiempos de ejecución de la máquina en función de su tamaño de entrada con una regresión exponencial.
![Diagrama de dispersión](https://docs.google.com/spreadsheets/d/e/2PACX-1vQH2Ti4y0I9EzXA_9ywUTNbpgQFwgAmBmJPkRxSFdUW_Yoz56MiiSJPJWkL9tkHtn5IodFjzrKJHF5A/pubchart?oid=240596747&format=image)
 - Grafico de la función de 2^n
![Grafico de 2^n](https://docs.google.com/spreadsheets/d/e/2PACX-1vQH2Ti4y0I9EzXA_9ywUTNbpgQFwgAmBmJPkRxSFdUW_Yoz56MiiSJPJWkL9tkHtn5IodFjzrKJHF5A/pubchart?oid=934101615&format=image)

Mediante el análisis de las regresiones exponenciales obtenidas para cada prueba y la comparación con el modelo de 2^n, podemos concluir que nuestro programa se aproxima con alta exactitud al comportamiento obtenido mediante inducción.

### Referencias

- Trejos, O. (2015). Algoritmo Recursivo diferente para hallar elementos
de la serie de Fibonacci usando Programación Funcional. AVANCES Investigación en Ingeniería Vol. 11. Recuperado de: https://acortar.link/jn0BbX
