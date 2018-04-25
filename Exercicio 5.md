
# Exercicio 5 das practicas de scada

## Oxetivos do exercicio
+ Os tanques solo poden ser cheos ou vaciados de un en un
+ Un tanque considerase vacio cando ten menos do 5% da sua capacidade
  + A cantidade calculada e 600
+ Un tanque considerase cheo cando ten mais do 95% da sua capacidade
  + A cantidade calculada e 10800
+ O tanque xeral considerase vacio cando ten menos do 10% da sua capacidade
  + A cantidade calculada e 30000
+ O tanque xeral considerase cheo cando ten mais do 90% da sua capacidade
  + A cantidade calculada e 270000
+ Denominase tanqueActivo a aquel que esta alimentando a saida nun momento dado
  + Damoslle ese valor a un tanque en canto este comeza a descargar o seu contido
? Cando o tanqueActivo chega ao estado de vacio debese cambiar automaticamente a un tanque cheo
  - Non entendo se temos que cambiar a un completamente cheo ou pode darse o caso de cambiar a un parcialmente cheo
- Por motivos de aforro e preciso que haxa 2 tanques disponhibles para bombear para realizar a carga dos tanques
+ Non se poden activar as bombas sen ter abertas antes as correspondentes valvulas


## PROCESO DE CARGA 
Esto garantiza que os depositos se enchan de un en un dende o 1 ata o 4 sempre que o tanque non se estea descargando e que o
tanque xeral tenha a carga suficiente o tanque activo non podera ser cargado ao mesmo tempo que se esta a descargar
```
valvulaEntradaTanque1 = 0;
valvulaEntradaTanque2 = 0;
valvulaEntradaTanque3 = 0;
valvulaEntradaTanque4 = 0;
tanqueEnchendose = 0;
bombaEntrada = 0;

IF tanqueGeneralVacio()
  bombaEntrada = 0;
ELSE
  IF NOT tanqueLLeno(tanque1) AND valvulaSaidaTanque1 == 0
    bombaEntrada = 1;
    tanqueEnchendose = tanque1;
    valvulaEntradaTanque1 = 1;
    valvulaEntradaTanque1 = 0;
    
  ELSE IF NOT tanqueLLeno(tanque2) AND valvulaSaidaTanque2 == 0
    bombaEntrada = 1;
    tanqueEnchendose = tanque2;
    valvulaEntradaTanque2 = 1;
  ELSE IF NOT tanqueLLeno(tanque3) AND valvulaSaidaTanque3 == 0
    bombaEntrada = 1;
    tanqueEnchendose = tanque3;
    valvulaEntradaTanque3 = 1;
  ELSE IF NOT tanqueLLeno(tanque4) AND valvulaSaidaTanque4 == 0 
    bombaEntrada = 1;
    tanqueEnchendose = tanque4;
    valvulaEntradaTanque4 = 1;
  ELSE
    bombaEntrada = 0
    tanqueEnchendose = 0;
```
    
## PROCESO DESCARGA 
Esto garantiza que os tanques sempre se vacien de un en un empezando dende o 4 ata chegar ao 1 ademais marca como activo o tanque que se esta descargando

```
valvulaSaidaTanque1 = 0;
valvulaSaidaTanque2 = 0;
valvulaSaidaTanque3 = 0;
valvulaSaidaTanque4 = 0;
tanqueActivo = 0;
bombaSaida = 0;

IF NOT tanqueVacio(tanque4) AND valvulaEntradaTanque4 == 0
  valvulaSaidaTanque4 = 1;
  tanqueDescargandose = tanque4;
  bombaSaida = 1;
ELSE IF NOT tanqueVacio(tanque3) AND valvulaEntradaTanque3 == 0
  valvulaSaidaTanque3 = 1;
  tanqueDescargandose = tanque3;
  bombaSaida = 1;
ELSE IF NOT tanqueVacio(tanque2) AND valvulaEntradaTanque2 == 0
  valvulaSaidaTanque2 = 1;
  tanqueDescargandose = tanque2;
  bombaSaida = 1;
ELSE IF NOT tanqueVacio(tanque1) AND valvulaEntradaTanque1 == 0
  valvulaSaidaTanque1 = 1;
  tanqueDescargandose = tanque1;
  bombaSaida = 1;
ELSE 
  tanqueDescargandose = 0;
  bombaSaida = 0;
```

## Valvula de entrada do tanque 1
### Requisitos
- A valvula de saida debe estar cerrada
- Debe haber polo menos 2 tanques vacios para comezar a encher
- O tanque 1 non pode estar cheo para comezar a encher
- Cando o tanque xeral estea vacio a valvula debese cerrar
- Cando a valvula de saida se abra a de entrada debese cerrar
- Cando o tanque 1 chege a sua carga maxima a valvula de entrada debe cerrarse
```
IF valvulaSaidaTanque1 == 0 THEN
  IF vaciados >= 2 THEN
    IF tanque1 <= Lleno THEN
      IF tanqueGeneral > vacio THEN
        valvulaEntradaTanque1 = 1;
      ELSE
        valvulaEntradaTanque1 = 0;
      ENDIF;
    ELSE
      valvulaEntradaTanque1 = 0;
    ENDIF;
  ENDIF;
ELSE
  valvulaEntradaTanque1 = 0
ENDIF;
```

## Valvula de entrada do tanque 2
### Requisitos
- A valvula de saida debe estar cerrada
- Debe haber polo menos 2 tanques vacios para comezar a encher
- O tanque 2 non pode estar cheo para comezar a encher
- Cando o tanque xeral estea vacio a valvula debese cerrar
- Cando a valvula de saida se abra a de entrada debese cerrar
- Cando o tanque 2 chege a sua carga maxima a valvula de entrada debe cerrarse
```
IF valvulaSaidaTanque2 == 0 THEN
  IF vaciados >= 2 THEN
    IF tanque2 < Lleno THEN
      IF tanqueGeneral < Lleno AND tanqueGeneral > vacio THEN
        valvulaEntradaTanque2 = 1;
      ELSE
        valvulaEntradaTanque2 = 0;
      ENDIF;
    ELSE
      valvulaEntradaTanque2 = 0;
    ENDIF;
  ENDIF;
ELSE
  valvulaEntradaTanque2 = 0;
ENDIF;
```



## Valvula de entrada do tanque 3
### Requisitos
- A valvula de saida debe estar cerrada
- Debe haber polo menos 2 tanques vacios para comezar a encher
- O tanque 3 non pode estar cheo para comezar a encher
- Cando o tanque xeral estea vacio a valvula debese cerrar
- Cando a valvula de saida se abra a de entrada debese cerrar
- Cando o tanque 3 chege a sua carga maxima a valvula de entrada debe cerrarse
```
IF valvulaSaidaTanque3 == 0 THEN
  IF vaciados >= 3 THEN
    IF tanque3 < Lleno THEN
      IF tanqueGeneral < Lleno AND tanqueGeneral > vacio THEN
        valvulaEntradaTanque3 = 1;
      ELSE
        valvulaEntradaTanque3 = 0;
      ENDIF;
    ELSE
      valvulaEntradaTanque3 = 0;
    ENDIF;
  ENDIF;
ELSE
  valvulaEntradaTanque3 = 0;
ENDIF;
```


## Valvula de entrada do tanque 4
### Requisitos
- A valvula de saida debe estar cerrada
- Debe haber polo menos 2 tanques vacios para comezar a encher
- O tanque 3 non pode estar cheo para comezar a encher
- Cando o tanque xeral estea vacio a valvula debese cerrar
- Cando a valvula de saida se abra a de entrada debese cerrar
- Cando o tanque 3 chege a sua carga maxima a valvula de entrada debe cerrarse
```
IF valvulaSaidaTanque4 == 0 THEN
  IF vaciados >= 4 THEN
    IF tanque4 < Lleno THEN
      IF tanqueGeneral < Lleno AND tanqueGeneral > vacio THEN
        valvulaEntradaTanque4 = 1;
      ELSE
        valvulaEntradaTanque4 = 0;
      ENDIF;
    ELSE
      valvulaEntradaTanque4 = 0;
    ENDIF;
  ENDIF;
ELSE
  valvulaEntradaTanque4 = 0;
ENDIF;
```
