---
sidebar_label: "Grouped Problem"
sidebar_position: 2
tags: [React, Javascript]
---
# Interview Problem [Basic]
Una de la pruebas que hacer usualmente es escojer elejir una estructura de datos, en el ejemplo siguiente escojeremos un objeto en javascript para agrupar fechas,

## Problem to solve

Teniendo un arreglo de dias `[{date:"10-10-2024,id:1, autor:"Juan Montes"},{date:"11-10-2024,id:101, autor:"Juan Montes"},{date:"10-10-2024,id:102, autor:"Juan Montes"}]` debes de agruparlo por dia para mostar cuantas veces al dia a trabajado. 

```js
//fetch the data
//group the data 

//solution A
const dataGrouped = data.reduce((item, acc)=>{

return acc
},0)

//solution B
const obj = {}
let counter = 0;
data.map((item)=>{
 if(obj[item.date]){
  obj[item.date] = ++counter
 }else{
  obj[item.date] = 1
 }
})

// merge con todos los dias del mes 
  // ya que si no estan en el data array debo mostralos 
// assign colors base range 1-3 3-6, 7 +

```