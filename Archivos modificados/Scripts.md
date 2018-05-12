# Scripts

## Script da venta
```
IF Automatico== 1 THEN
    IF botonentrada==1 THEN 

    {Porque a electrovalvula tres non me funcionaba ben tal e como a tiña no script}
    IF ev1b+ev2b+ev3b+ev3b==0  THEN
        bomba2=0;
    ELSE 
        bomba2=1;
    ENDIF;

    {Bombear desde o tanque de alimentación a un só tanque}
    IF ev1b==1 THEN
        ev2b=0;
        ev3b=0;
        ev4b=0;
    ENDIF;
    IF ev2b==1 THEN
        ev1b=0;
        ev3b=0;
        ev4b=0;
    ENDIF;
    IF ev3b==1  THEN
        ev2b=0;
        ev1b=0;    
        ev4b=0;
    ENDIF;
    IF ev4b==1 THEN
        ev2b=0;
        ev3b=0;
        ev1b=0;
    ENDIF;


    {Para que poidamos levar a cabo o traballo en automático}

    IF nivelgeneral <=10 THEN
        botonentrada=1;
    ENDIF;


    {Cumplir a condición 7}

    IF nivel1 <=0.15  AND nivel2 >= 2.85 THEN
        ev2b=1;
    ENDIF;

    IF nivel1 <= 0.15 AND nivel3 >= 2.85 THEN
        ev3b=1;
    ENDIF;

    IF nivel1  <= 0.15 AND nivel4 >= 2.85 THEN
        ev4b=1;
    ENDIF;
    IF nivel2  <= 0.15 AND nivel1  >= 2.85 THEN
        ev1b=1;
    ENDIF;

    IF nivel2  <= 0.15 AND nivel3  >= 2.85 THEN
        ev3b=1;
    ENDIF;

    IF nivel2  <= 0.15 AND nivel4  >= 2.85 THEN
        ev4b=1;
    ENDIF;

    IF nivel3  <= 0.15 AND nivel1  >= 2.85 THEN
        ev1b=1;
    ENDIF;

    IF nivel3  <= 0.15 AND nivel2  >= 2.85 THEN
        ev2b=1;
    ENDIF;

    IF nivel3  <= 0.15 AND nivel4  >= 2.85 THEN
        ev4b=1;
    ENDIF;

    IF nivel4  <= 0.15  AND nivel1  >= 2.85 THEN
        ev1b=1;
    ENDIF;

    IF nivel4  <= 0.15  AND nivel2  >= 2.85 THEN
        ev2b=1;
    ENDIF;

    IF nivel4 <= 0.15 AND nivel3  >= 2.85 THEN
        ev3b=1;
    ENDIF;

    {Cumplimento da condición 8}
    IF nivel1<=0.15 AND nivel2<=2.85 THEN
        ev1a=1;
        ev2a=1;
    ENDIF;

    IF nivel1 <=0.15 AND nivel3 <=2.85 THEN
        ev1a=1;
        ev3a=1;
    ENDIF;

    IF nivel1<=0.15 AND nivel4 <=2.85 THEN
        ev1a=1;
        ev4a=1;
    ENDIF;

    IF nivel2 <=0.15  AND nivel3 <=2.85 THEN
        ev2a=1;
        ev3a=1;
    ENDIF;

    IF nivel2 <=0.15 AND nivel4<=2.85 THEN
        ev2a=1;
        ev4a=1;
    ENDIF;

    IF nivel3 <=0.15 AND nivel4 <=2.85 THEN
        ev3a=1;
        ev4a=1;
    ENDIF;

    {Fin do traballo automático}

    {HTUpdateToCurrentTime''HistTrend'';}
    HistTrend.UpdateTrend=1;

    {Configuración gráfico histórico}
    ELSE 
        bomba1=0;
        ev1a=0;
        ev2a=0;
        ev3a=0;
        ev4a=0;
        ev1b=0;
        ev2b=0;
        ev3b=0;
        ev4b=0;
        bomba2=0;
    ENDIF;
ENDIF;

```

## Script bomba1
```
{Para que a bomba funcione ten que haber ao menos un elemento acceso}
IF Automatico == 1 THEN
    IF bomba1==0 THEN 
        ev1a=0;
        ev2a=0;
        ev3a=0;
        ev4a=0;
    ENDIF;
ENDIF;

```

## Script bomba 2
```
{Para que a bomba funcione ten que haber ao menos un elemento acceso}

IF Automatico == 1 THEN
    IF bomba2==0 THEN 
        ev1b=0;
        ev2b=0;
        ev3b=0;
        ev4b=0;
    ENDIF;
    IF ev1b+ev2b+ev3b+ev4b==0 THEN 
        bomba2=0;
    ELSE 
        bomba2=1;
    ENDIF;
ENDIF;
```
## Script Valvula de entrada 1
```
IF Automatico == 1 THEN

    {Se o nivel do tanque está cheo entón a ev de entrada non pode estar operativa}
    IF nivel1==3 THEN 
        ev1a=0;
    ENDIF;

    {Comprobación de que está a electroválvula operativa para poder funcionar}
    IF ev1a==1 THEN 
        bomba1=1;
    ENDIF;

    {Ten que haber ao menos unha ev operativa para poder funcionar}
    IF ev1a+ev2a+ev3a+ev4a <1 THEN 
        bomba1=0;
    ENDIF;

    {Condición referente a operatividade das ev é o nivel do tanque de abastecemento}
    IF ev1a+ev2a+ev3a+ev4a >1  AND nivelgeneral>=1 THEN 
        bomba1=1;
    ENDIF;
ENDIF;
```

## Script valvula de entrada 2
```
IF Automatico == 1 THEN
    IF nivel2==3 THEN 
        ev2a=0;
    ENDIF;

    IF ev2a==1 THEN 
        bomba1=1;
    ENDIF;

    IF ev1a+ev2a+ev3a+ev4a <1 THEN 
        bomba1=0;
    ENDIF;
ENDIF;
```

## Script valvula de entrada 3
```
IF Automatico == 1 THEN
    IF nivel3==3 THEN 
        ev3a=0;
    ENDIF;

    IF ev3a==1 THEN 
        bomba1=1;
    ENDIF;

    IF ev1a+ev2a+ev3a+ev4a <1 THEN 
        bomba1=0;
    ENDIF;
ENDIF;
```

## Script valvula de entrada 4
```
IF Automatico==1 THEN
    IF nivel4==3 THEN 
        ev4a=0;
    ENDIF;

    IF ev4a==1 THEN 
        bomba1=1;
    ENDIF;

    IF ev1a+ev2a+ev3a+ev4a <1 THEN 
        bomba1=0;
    ENDIF;
ENDIF;
```

## Script valvula de saida 1
```
IF Automatico == 1  THEN
    IF ev1b==1  AND tanque1lleno==1 THEN 
        tanqueactivo=1;
    ENDIF;

    IF ev1b==0  THEN
        tanqueactivo=0;
    ENDIF;

    IF ev1b==1  THEN
        ev2b=0;
        ev3b=0;
        ev4b=0;
        bomba2=1;
    ENDIF;
ENDIF;
```

## Script valvula de saida 2
```
IF Automatico == 1 THEN
    IF ev2b==1  AND tanque2lleno==1 THEN 
        tanqueactivo=1;
    ENDIF;

    IF ev2b==0  THEN
        tanqueactivo=0;
    ENDIF;

    IF ev2b==1  THEN
        ev1b=0;
        ev3b=0;
        ev4b=0;
        bomba2=1;
    ENDIF;
ENDIF;
```

## Script valvula de saida 3
```
IF Automatico==1 THEN 
    IF ev3b==1  AND tanque3lleno==1 THEN 
        tanqueactivo=1;
    ENDIF;

    IF ev3b==0  THEN
        tanqueactivo=0;
    ENDIF;


    IF ev3b==1  THEN
        ev1b=0;
        ev2b=0;
        ev3b=0;
    ENDIF;

    IF ev1b+ev2b+ev4b == 0 THEN
        IF nivel3 >= 0.15 THEN
            ev3b=1;
        ENDIF;
    ENDIF;

    IF nivel1==0.15  AND nivel3>=2.85  THEN
        ev3b=1;
    ELSE 
        IF nivel2 ==0.15 AND nivel3 >= 2.85 THEN
            ev3b=1;
        ENDIF;
        IF nivel4==0.15  AND nivel3>=2.85  THEN
            ev3b=1;
        ENDIF;
    ENDIF;
ENDIF;

```

## Script valvula de saida 4
```
IF Automatico == 1 THEN
    IF ev4b==1  AND tanque4lleno==1 THEN 
        tanqueactivo=1;
    ENDIF;

    IF ev4b==0  THEN
        tanqueactivo=0;
    ENDIF;

    IF ev4b==1  THEN
        ev1b=0;
        ev2b=0;
        ev3b=0;
        bomba2=1;
    ENDIF;

    IF nivel1==2.85  AND nivel2==2.85  AND nivel3==2.85  AND nivel4==2.85  THEN
        IF ev2b+ev3b+ev4b==0  THEN
            ev1b=1;
        ENDIF;
    ENDIF;
ENDIF;
```

## Script nivel 1
```
IF Automatico == 1 THEN
    IF nivel1>=0.15 THEN 
        tanque1vacio=0;
    ENDIF;

    IF nivel1>=2.85 THEN 
        tanque1lleno=1;
    ENDIF;

    IF nivel1<=0.15 THEN 
        tanque1vacio=1;
        tanque1lleno=0;
        ev1b=0;
    ENDIF;

    IF tanque1vacio+tanque2vacio+tanque3vacio+tanque4vacio >=3 THEN
        Alarmavacio=1;
    ELSE
        Alarmavacio=0;
    ENDIF;

    IF nivel1==3 THEN 
        ev1a=0;
    ENDIF;
ENDIF;   
```
## Script nivel 2
```
IF Automatico == 1 THEN
    IF nivel2>=0.15 THEN 
        tanque2vacio=0;
    ENDIF;

    IF nivel2>=2.85 THEN 
        tanque2lleno=1;
    ENDIF;

    IF nivel2<=0.15 THEN 
        tanque2vacio=1;
        tanque2lleno=0;
        ev2b=0;
    ENDIF;

    IF tanque1vacio+tanque2vacio+tanque3vacio+tanque4vacio >=3 THEN
        Alarmavacio=1;
    ELSE
        Alarmavacio=0;
    ENDIF;

    IF nivel2==3 THEN 
        ev2a=0;
    ENDIF;
ENDIF; 
```

## Script nivel 3

```
IF Automatico == 1 THEN
    IF nivel3>=0.15 THEN 
        tanque3vacio=0;
    ENDIF;

    IF nivel3>=2.85 THEN 
        tanque3lleno=1;
    ENDIF;

    IF nivel3<=0.15 THEN 
        tanque3vacio=1;
        tanque3lleno=0;
        ev3b=0;
   
    ENDIF;

    IF tanque1vacio+tanque2vacio+tanque3vacio+tanque4vacio >=3 THEN
        Alarmavacio=1;
    ELSE
        Alarmavacio=0;
    ENDIF;

    IF nivel1==3 THEN 
        ev3a=0;
    ENDIF;
ENDIF;
```

## Script nivel 4

```
IF Automatico == 1 THEN
    IF nivel4>=0.15 THEN 
        tanque4vacio=0;
    ENDIF;

    IF nivel4>=2.85 THEN 
        tanque4lleno=1;
    ENDIF;

    IF nivel4<=0.15 THEN 
        tanque4vacio=1;
        tanque4lleno=0;
        ev4b=0;

    ENDIF;

    IF tanque1vacio+tanque2vacio+tanque3vacio+tanque4vacio >=3 THEN
        Alarmavacio=1;
    ELSE
        Alarmavacio=0;
    ENDIF;

    IF nivel4==3 THEN 
        ev4a=0;
    ENDIF;
ENDIF; 
```
