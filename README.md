<h1>Hooks verification eslint</h2>

- Verifica se há algum erro no hook:

```bash
yarn add eslint-plugin-react-hooks -D
```

- No arquivo `eslintrc.js` na parte de plugins deveremos ter o seguinte:

```js
plugins: [
    'react',
    'prettier',
    'react-hooks'
  ],
```

- Ainda nesse arquivo na parte de `rules`:

```js
rules: {
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': [
      'warn',
      { extensions: ['.jsx', '.js']}
    ],
    'import/prefer-default-export': 'off',

    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
  },
```

- a regra `'react-hooks/rules-of-hooks': 'error',` irá avisar qualquer erro que estivermos infringindo nas regras do hooks

- a regra `'react-hooks/exhaustive-deps': 'warn',` na parte de useEffects, irá avisar quando estivermos faltando com algumas dependencias.
