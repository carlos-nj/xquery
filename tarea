PRODUCTOS
Obtén por cada zona el número de productos que tiene.
for $i in distinct-values(//produc/cod_zona)
return count(//produc[cod_zona = $i])

Obtén la denominación de los productos entre las etiquetas <zona10></zona10> si son del código de zona 10, <zona20></zona20> si son del código de zona 20, <zona30></zona30> si son del código de zona 30 y <zona40></zona40> si son del código de zona 40
    for $zona in distinct-values(//produc/cod_zona)
return 
    if ($zona='10') then <zona10>{//produc[cod_zona = $zona]//denominacion
}</zona10>
else if ($zona='20') then <zona20>{//produc[cod_zona = $zona]//denominacion
}</zona20>
else if ($zona='30') then <zona30>{//produc[cod_zona = $zona]//denominacion
}</zona30>
else<zona40>{//produc[cod_zona = $zona]//denominacion
}</zona40>
 
Obtén por cada zona la denominación del producto o de los productos más caros
for $zona in distinct-values(//produc/cod_zona)
let $precio_max := max(//produc[cod_zona = $zona]//precio)
let $denominacion:= //produc[precio = $precio_max]//denominacion
return concat($denominacion, ": ", $precio_max, " EUROS &#10;")
 
 
 
 
Obtén la denominación de los productos contenida entre las etiquetas <placa></placa> para los productos en cuya denominación aparece la palabra  placa base, <memoria></memoria> para los que contienen la palabra Memoria <micro></micro>, para los que contienen la palabra Micro y <otros></otros> para el resto de productos
for $denominacion in distinct-values(//produc/denominacion)
return
    if(contains ($denominacion, "Placa Base")) then <placa>{//produc[denominacion = $denominacion]        //denominacion}</placa>
    else if(contains ($denominacion, "Memoria")) then <memoria>{//produc[denominacion = $denominacion]        //denominacion}</memoria>
    else if(contains ($denominacion, "Micro")) then <micro>{//produc[denominacion = $denominacion]        //denominacion}</micro>
    else <otros>{//produc[denominacion = $denominacion]//denominacion}</otros>
 
SUCURSALES
Devuelve el código de sucursal y el número de cuentas que tiene de tipo AHORRO y de tipo PENSIONES
for $c in //sucursal/@codigo
let $tipo_ahorros:=count(//sucursal[@codigo=$c]//cuenta[@tipo="AHORRO"])
let $tipo_pensiones:= count(//sucursal[@codigo=$c]//cuenta[@tipo="PENSIONES"])
return concat("Codigo de sucursal: ", $c, " - Numero de cuentas de ahorro y pensiones: ", $tipo_ahorros, " y ", $tipo_pensiones)
 
 
 
 
Devuelve por cada sucursal el código de sucursal, el director, la población, las sumas del total debe y la suma del total haber de sus cuentas
for $sucursal in //sucursal
return 
   <sucursal>
       {$sucursal/@codigo,
        $sucursal/director,
       $sucursal/poblacion}
    <totalDebe>
       {sum($sucursal//saldodebe)}
    </totalDebe>
    <totalHaber>
        {sum($sucursal//saldohaber)}
    </totalHaber>
   </sucursal>
Devuelve el nombre de los directores, el código de sucursal y la población de las sucursales con más de 3 cuentas
for $sucursal in //sucursal
where count($sucursal/cuenta)  > 3
return
  <sucursal>
       {$sucursal/@codigo,
       $sucursal/director,
       $sucursal/poblacion}
       <numCuentas>
       {count($sucursal/cuenta)}
       </numCuentas>
    
   </sucursal>
 
Devuelve por cada sucursal, el código de sucursal y los datos de las cuentas con más saldo debe
for $sucursal in //sucursal
return 
   <sucursal>
       {$sucursal/@codigo}
    <cuenta>
       {max($sucursal//saldodebe)}
    </cuenta>
   </sucursal>
   
Devuelve la cuenta del tipo PENSIONES que ha hecho más aportación
for $cuenta in //sucursal/cuenta
where $cuenta/@tipo = "PENSIONES"
return 
          $cuenta[aportacion = max(//aportacion)]
