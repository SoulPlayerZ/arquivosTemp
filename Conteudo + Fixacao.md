# Conteúdo

## Primeiros passos em RTL
<br>

Quando você estudoe *Assert* e *Jest*, o objetivo principal era testar código(funções).Testar o retorno das funções implementadas na aplicação. O objetivo da RTL é testar o comportamento da nossa aplicação em determinado momento de acordo com os *casos de uso*.

- **Caso de uso**: Em resumo, é um momento específico da nossa aplicação.

EX: Como está nossa aplicação no momento em que ela é inicilizada. Ou como ela se comporta de acordo com determinada interação do 
usuário, como por exemplo, clicar em um botão.

Em RTL nós simulamos a utilização da nossa aplicação. Diferentemente dos testes que vimos antes, que focava nos retornos de funções.

Você deve estar se perguntando: Como fazemos esses testes de comportamento ? 
Vamos isso na prática a seguir.


Vamos tomar como exemplo a aplicação inicial do React quando você começa um projeto *"do zero"*.

Lembra como fazemos isso ?
<br>
<br>

Digite no seu terminal o comando abaixo:

````shell
npx create-react-app react-tests
````
<br>

- Lembrando que *react-tests* é o nome que estamos dando a pasta que será criada. :wink:

<br>
   
Agora abra seu editor(VSCode) e procure pelo arquivo **package.json**.


Verifique a chave **dependencies**. Ela vai possuir chaves **@testing-library...**

````javascript
  "dependencies": {
    "@testing-library/jest-dom": "^5.14.1",
    "@testing-library/react": "^11.2.7",
    "@testing-library/user-event": "^12.8.3",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-scripts": "4.0.3",
    "web-vitals": "^1.1.2"
  },
````  
<br>
Exatamente. :blush: A biblioteca RTL já vem instalada quando iniciamos um projeto React do zero.

Agora abra o arquivo App.test.js que está dentro de src e vamos analisar o código.

````javascript
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
````
<br>
O primeiro detalhe que você vai perceber é que a estrutura é bem parecida com a que você fazia em Jest. :blush:

Agora vamos verificar o teste em si.
<br>
<br>
<br>

## A função render
<br>

````javascript
render(<App />);
````

Em resumo, a função render, como o nome diz, renderiza o componente que queremos testar. Lembrando que vamos testar comportamento, logo, precisamos renderizar o componente a ser testado. 
Um ponto importante aqui é que o render simula a renderização em uma espécie de browser virtual. Isso é importante para testarmos por exemplo, requisições a API's'. Você verá isso em um futuro próximo.
<br>
<br>
<br>


## Seletores
<br>

````javascript
const linkElement = screen.getByText(/learn react/i);
````

Após a renderização do nosso componente App.js, nós "recuperamos" o componente cujo conteúdo contenha o texto "learn react".

- Relembrando: /learn react/i quer dizer que o texto do componente deve incluir o texto "learn react" e o "i" está ignorando o case sensitive, podendo ser maiúsculo ou minísculo.

Você deve ter percebido que é semelhante a navegar pelo DOM com o JavaScript com o famoso *document.getElementById('element-id')* por exemplo.

Você pode ver os diversos tipos de seletores no [RTL Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/).
É sempre bom termos por perto qualquer tipo de documentação para nos auxiliar a escrever nossos testes.
<br>
<br>
<br>


## Matchers
<br>

````javascript
expect(linkElement).toBeInTheDocument();
````

Estes você já conhece bem. Assim como em *Jest*, usamos matchers para realizar nossos testes. No exemplo acima estamos verificando se o elemento recuperado está presente na tela após a renderização do nosso componente <App />

Podemos testar inúmeras situações do nosso componente. Se um elemento tem um texto específico ou se algum elemento possui determinada propriedade, por exemplo.
É bom sempre ter em mãos uma [lista dos matchers](https://github.com/testing-library/jest-dom) para nos auxiliar em nossa lógica de testes.


Lembre-se de provocar uma falha no seu teste para evitar famoso *falso positivo*. Experimente trocar o texto "learn react" do elemento por "Alguma coisa", o teste deve falhar.
<br>
<br>
<br>

## Testando Eventos
<br>
---------Escrever essa parte ainda -----
<br>
<br>

Agora que tal um quizz para ajudar a fixar o conteúdo antes de exercitar ?

<br>
<br>

# Fixação

<u><h2>Questão 1</h2></u>

## Marque CERTO ou ERRADO.

### Considere o código abaixo:
````JavaScript
render(<App />);
const fightingGame = screen.getByTextIncludes(/Street Fighter 5/i);
expect(fightingGame).toBeInTheDocument();
````


<h3>---Ao rodar o comando 'npm test' teste falhará.---</h3>
<br>

### A afirmação acima está:

a) CERTA

b) ERRADA
<br>
<br>
<br>
<hr>
<u><h2>Questão 2</h2></u>
<br>

### Considere o código abaixo:
````JavaScript
render(<App />);
const favoriteMusicElement = screen.getByText(/Minha música preferida/i);
expect(favoriteMusicElement).toBeInTheDocument();
````
<br>

## Neste caso, está sendo testado:
<br>

a) Se favoriteMusicElement tem o texto "Minha música preferida".

b) Se o elemento recuperado é um parágrafo.

c) Se um elemento que inclue o texto "Minha música preferida" está renderizado na tela.

d) Se existe uma imagem renderizada na tela.

e) Se favoriteMusicElement é possui a propriedade "Minha música preferida".
<br>
<br>
<br>
<hr>

<u><h2>Questão 3</h2></u>

## O objetivo principal da React Testing Library(RTL) é:

<br>

a) Testar o comportamento da aplicação em diversas situações de acordo com os possíveis casos de uso.

b) Substituir a biblioteca Enzyme para realizar testes em aplicações React.

c) Garantir a cobertura de código das funções da nossa apllicação.

d) Se tornar uma linguagem de programação.

e) Tentar conquistar o mundo.
<br>
<br>
<br>
<hr>

<u><h2>Questão 4</h2></u>

## Qual a sintaxe correta para o caso de querermos testar se um botão inclue o texto "Enviar" ?

a)
````JavaScript
render(<App />);
const button = screen.getByType('button');
expect(button).toHaveTextContent('Enviar');
````

b) 
````JavaScript
render(<App />);
expect(<button>).toBeInTheDocument();
````

c) 
````JavaScript
render(<App />);
const button = screen.getByRole('button');
expect(button).toHaveTextContentIncludes('Enviar');
````

d)
````JavaScript
render(<App />); 
const button = screen.getByRole('button');
expect(button).toHaveTextContent('Enviar');
````
 
e) 
````JavaScript
render(<App />);
const button = screen.getByRole('button');
expect(button).toHaveTextContent.includes('Enviar');
````
<br>
<br>
<br>
<hr>
<u><h2>Questão 5</h2></u>
<br>

## Qual das alternativas abaixo testa corretamente se uma imagem possui o atributo "src":


a)
````JavaScript
render(<App />)
const hatImage = screen.getByText(/hat/i);
expect(hatImage).toHaveAttribute('src'); 
````

b)
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute.SRC(); 
````

c)
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute('src'); 
````


d)
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute(src); 
````

e)
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage.attribute).toBe(src); 
````

