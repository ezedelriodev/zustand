<h1>Apuntes Zustand</h1>
<p align="center">
  <a href="https://docs.pmnd.rs/zustand/getting-started/introduction" target="blank"><img src="https://repository-images.githubusercontent.com/180328715/fca49300-e7f1-11ea-9f51-cfd949b31560" width="250" alt="Zustand Logo" /></a>
</p>

## **Índice**

- [**Índice**](#índice)
- [**Documentación**](#documentación)
- [**Crear un estado global**](#crear-un-estado-global)



## **Documentación**
* [Documentación](https://zustand.docs.pmnd.rs/getting-started/introduction)

## **Crear un estado global**

```js
//Javascript

import { create } from 'zustand'

const useStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
  updateBears: (newBears) => set({ bears: newBears }),
}))
```

```js
//TypeScript

import { create } from 'zustand'

interface BearState {
  bears: number
  increase: (by: number) => void
}

const useBearStore = create<BearState>()((set) => ({
  bears: 0,
  increase: (by) => set((state) => ({ bears: state.bears + by })),
}))
```

Podemos crear el store globlal en el directorio ``stores/ bears/ bears.store.ts``

Èl estado puede constar de dos partes:
- Piezas del estado (properties)
- Acciones o métodos del estado.

Podemos encontralas juntas en la misma interface o separadas.

**Ejemplo de estado global**
___
```js
import { create } from 'zustand'

interface BearState {
blackBears: number;
polarBears: number;
pandaBears: number;

increaseBlackBears: (by: number) => void;

}

export const useBearStore = create<BearState>()((set) => ({
    blackBears:10,
    polarBears:5,
    pandaBears:1,
    increaseBlackBears: (by: number) => set((state) => ({ blackBears: state.blackBears + by })),
}))
```
1. **Definición de la interfaz del estado (BearState)**:

- Se define una interfaz llamada ``BearState`` que describe la **forma del estado que se manejará**. Contiene:
 - Tres propiedades numéricas: ``blackBears``, ``polarBears`` y ``pandaBears``, que representan cantidades de diferentes tipos de osos.  
 - Una función llamada ``increaseBlackBears`` que acepta un número (``by``) y no devuelve nada (``void``), pero modifica el estado al incrementar el número de ``blackBears``.  
 - 
2. **Creación del estado global (``useBearStore``)**:

- La función ``create`` de **Zustand** se utiliza para crear un hook llamado ``useBearStore``.
- Este hook maneja un estado inicial y las funciones para actualizarlo.  
  
3. **Estado inicial**:

- Dentro del ``create``, se proporciona el estado inicial:  
  - ``blackBears: 10``
  - ``polarBears: 5``
  - ``pandaBears: 1``
- Estas propiedades representan las cantidades iniciales de cada tipo de oso.  
  
4. **Función para actualizar el estado (``increaseBlackBears``)**:

- Se define la función ``increaseBlackBears`` que incrementa el valor de blackBears en la cantidad especificada por el parámetro ``by``.
- Usa la función ``set`` (proporcionada por Zustand) para actualizar el estado. ``set`` recibe una función que toma el estado actual (``state``) y devuelve un nuevo objeto con los cambios deseados. En este caso, solo actualiza ``blackBears``.

**[⬆ Volver a índice](#índice)**

---