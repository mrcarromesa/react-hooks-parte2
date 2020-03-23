<h1>Hooks</h1>

<h2>useState</h2>

- importando o `useState`:

```js
import React, { useState } from 'react';
```

- inicializando o `useState`:

```js
const [techs, setTech] = useState(['ReactJS', 'React Native']);
const [newTech, setNewTech] = useState('');
```

- Alterando o valor do estado:

```js
setTech([...techs, newTech]);
setNewTech('');
```
---

<h2>useEffect</h2>

- importando o `useEffect`:

```js
import React, { useState, useEffect } from 'react';
```

- Executar function quando iniciar o componente:

```js
useEffect(() => {
  //...
}, []);
```

- Inserir `[]`, vazio. e acima de outros useEffect.

- Para executar uma function após atualziar um  `useEffect`:

```js
const [techs, setTech] = useState([]);
  const [newTech, setNewTech] = useState('');

  function handleAdd() {
    setTech([...techs, newTech]);
    setNewTech('');
  }

  useEffect(() => {
    localStorage.setItem('tech', JSON.stringify(techs));
  }, [techs]);
```

- Executar uma function quando um componente deixar de existir, em geral é pouco utilizado:

```js
useEffect(() => {
  //...

  return () => {};
}, []);
```

- Basicamente é utilizado `return () => {};`

---

<h2>useMemo</h2>

- Importando o `useMemo`:

```js
import React, { useState, useEffect, useMemo } from 'react';
```

- Chamamos quando precisamos realizar calculos mais complexos, pois se pegarmos uma váriavel do useState, então toda vez que ela alterar o calculo será chamado novamente, então para melhorar o desempenho é recomendado utilizar o useMemo.

- Imaginando que por exemplo tenhamos que realizar a seguinte ação

```js
<strong>Você tem {techs.length} tecnologias</strong>
```

- Então toda vez que o techs sofrer alguma alteração ela será chamada, ou seja esse recurso sempre será chamado, nesse caso com se trata de pegar o tamanho do array até que tudo bem, mas quando é um calculo mais complexo e demorado é recomendado utilizar o useMemo, nesse caso isso ficaria assim:

```js
const techsSize = useMemo(() => techs.length, [tech]);
```

- Nessa função estamos pedindo para recalcular o valor de techs.length, toda vez que `tech` sofrer alteração e definindo o valor para const techsSize.

- Então agora podemos substituir o código anterior para:

```js
<strong>Você tem {techsSize} tecnologias</strong>
```

---

<h2>useCallback</h2>

- Importando:

```js
import React, { useState, useEffect, useMemo, useCallback } from 'react';
```

É semelhante ao `useMemo` porém ao invés de retornar um único valor ele retorna uma function


- As functions criadas dentro do componente são recriadas toda vez que o componente ou estado é alterado, utilizando muito processamento, para resolver isso pode ser utilizado o `useCallback`, por exemplo a function:

```js
function handleAdd() {
  setTech([...techs, newTech]);
  setNewTech('');
}
```

- Essa fuction é criada toda vez quando as variaveis ali dentro muda, para melhorar isso utilizamos o `useCallback`:

```js
const handleAdd = useCallback(() => {
  setTech([...techs, newTech]);
  setNewTech('');
}, [techs, newTech]);
```

- Dessa forma a function só será recriada apenas quando o techs e ou o newTech mudar
