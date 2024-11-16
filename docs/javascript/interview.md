---
sidebar_label: "Intervie Questions React"
sidebar_position: 1
tags: [React]
---
# Interview Questions
## Explain React's component lifecycle.
En el virtual dom, y react hay 3 tipos de funciones o estados, 
cuando se monta, se desmonta y se actualiza
usando hooks,
### Mounting - se monta 
```javascript 
useEffect(()=>{},[])
```
### Updating - se actualiza 
```javascript 
useEffect(()=>{},[param])
```
### Unmouting - se desmonta 
```javascript 
useEffect(
  ()=>{
    return ()=>{
}
},[])
```

## Example of ContextAPI

El uso de context api es para manejar el estado de la apicacion para evitar el drop dilling, que es evitar pasar el estado entre componentes

### Ejemplo Simple

```jsx
// 1. Creacion del contexto
const UserContext = createContext();

// 2. Crear provider
const UserProvider = ({children})=>{
  const [user, setUser] = useState("");
  return <UserContext.Provider value={user, setUpdate}>{children}</UserContext.Provider>;
};

// 3. Implementar
<UserContextProvider>
</UserContextProvider>

// 4. Acceso al estado
const [user, setUser] = useContext(UserContext);
```

### Ejemplo con hook y reducers
```jsx

// Crear state 
const initialTaskState = {
  tasks:[]
};
const TaskReducer = (state, action)=>{
  switch(action.type){
    case "Add":
      const _tasks = [...state.tasks,action.payload]
      return {...state, tasks:_tasks}
      break;
  }
}
// crear context
const TaskContext = createContext();
// crear provider 
const [state, dispatch] = useReducer(Taskreducer, initialTaskState)
const TaskContextProvider = ()=>{
  <TaskContext.Provider value={state, dispatch}></TaskContext.Provider>
}


// Implementacion List

const [state, dispatch:taskDispatch] = useContext(TaskContext)
taskDispatch({type:"Add", {id:4,}})

```
### Ventajas
- Manejo global
- no es necesario intalar librerias, ya esta disponible, es nativo de React
- es sencillo
- combinacion con otro hooks para agragar complegidad como useReduce
### Desventajas

8:00 - 8:30 LLegamos Tepoz
8:30- 5:30 