# Conteúdo

## Primeiros passos em RTL
<br>

Quando você estudou *Assert* e *Jest*, o objetivo principal era testar código(funções). Testar o retorno das funções implementadas na aplicação. O objetivo da RTL é testar o comportamento da nossa aplicação em determinado momento de acordo com os *casos de uso*.

- **Caso de uso**: Em resumo, são possibilidades que fazem com que nossa aplicação se comporte de determinada maneira.

EX:

  Como está nossa aplicação no momento em que ela é inicilizada, o que é renderizado na tela em determinado momento ou como ela se comporta de acordo com determinada interação do usuário, como por exemplo, clicar em um botão.

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

- Lembrando que *react-tests* é o nome que estamos dando a pasta que será criada. :blush:

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
Exatamente :wink: . A biblioteca RTL já vem instalada quando iniciamos um projeto React do zero.

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
Um ponto importante aqui, é que o render simula a renderização em uma espécie de browser virtual. Isso é importante para testarmos por exemplo, requisições a API's'. Você verá isso em um futuro próximo.
<br>
<br>
<br>


## Seletores
<br>

````javascript
const linkElement = screen.getByText(/learn react/i);
````

Após a renderização do nosso componente App.js, nós "recuperamos" o componente cujo conteúdo contenha o texto "learn react".

- Relembrando: /learn react/i quer dizer que o texto do componente deve incluir o texto "learn react" e o "i" está ignorando o case sensitive, podendo ser maiúsculo ou minúsculo.

Você deve ter percebido que é semelhante a navegar pelo DOM em JavaScript com o famoso *document.getElementById('element-id')* por exemplo.

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

Estes você já conhece bem. Assim como em *Jest*, usamos matchers para realizar nossos testes. No exemplo acima estamos verificando se o elemento recuperado está presente na tela após a renderização do nosso componente `<App />`.

Podemos testar inúmeras situações do nosso componente. Se um elemento tem um texto específico ou se algum elemento possui determinada propriedade, por exemplo.
É bom sempre ter em mãos uma [lista de matchers](https://github.com/testing-library/jest-dom) para nos auxiliar em nossa lógica de testes.


Lembre-se de provocar uma falha no seu teste para evitar famoso *falso positivo*. Experimente trocar o texto "learn react" do elemento por "Alguma coisa", o teste deve falhar.
<br>
<br>
<br>

## Testando Eventos
<br>
Até o momento, nós testamos, basicamente, se elementos estão aprecendo na tela quando nosso componente é renderizado, se possuem alguma propriedade ou algum texto específico. Mas com a RTL nós podemos testar o comportamento da nossa aplicação de acordo com <s>interações</s> simulações de interação da pessoa que utiliza nossa aplicação.

A RTL possui uma ferramenta interessante para testar eventos que é o *fireEvent*. Vamos entender um pouco sobre ele com um exemplo:


````JS
fireEvent.click(button);
````
O código do exemplo acima está disparando um evento de click em um determinado botão. Com isso, você consegue realizar testes de eventos de click. Porém, o *fireEvent* não está simulado exatamente o comportamento de uma pessoa utilizando nossa aplicação. Um evento de click realizado por um usário possui vários outros passos até chegar ao click de fato. Um *mouseOver* por exemplo.
No caso de testar um click, o *fireEvent* pode atender tranquilamente se quisermos testar simplesmente o que acontece quando ocorre o click. Mas imagine um evento *onChange* ou até mesmo algumas situações de click isso pode não chegar de fato ao nível que queremos testar. Em resumo, o *fireEvent* nos ajuda a testar eventos em si, mas existe uma forma de nos aproximarmos ainda mais do comportamento real de uma pessoa utilizando nossa págna, a [user-event](https://testing-library.com/docs/ecosystem-user-event/).

**use-event** - É uma biblioteca que complementa a RTL. Esta biblioteca nos possibilita testar, mais próximo da realidade, o comportamento de uma pessoa que utilizará nossa aplicação. Por isso é recomendado que utilizemos *userEvent* quando vamos testar de acordo com a simulação de uma pessoa interagindo com a página.

Antes de mostrar um exemplo de utilização do *userEvent*, vale dar uma conferida na [documentação](https://github.com/testing-library/user-event) e na [lista de eventos](https://github.com/testing-library/dom-testing-library/blob/main/src/event-map.js) que o *fireEvent* suporta.

Um ponto importante a lembrar também, é que a biblioteca *user-event* já vem instalada quando iniciamos uma aplicação React com o comando *npx create-react-app*. Mas, caso seja necessário, podemos realizar a instalção com o comando abaixo:

````JS
npm install --save-dev @testing-library/user-event
````

Agora vamos ao exemplo:

Inicie uma aplicação React com o comando *npx create-react-app*.

Depois, substitua o conteúdo do arquivo App.js pelo código abaixo.

````JS
import React from 'react';
import './App.css';

class App extends React.Component {
  constructor(){
    super();
    this.state = {
      value: '',
      disable: true,
    }

  }

  handleChange = ({ target }) => {
    this.setState({
      value: target.value,
    })
  }

  handleClick = () => {
    this.setState({
      disable: false,
    })
  }

  render() {
    const { value, disable } = this.state;
    return (
      <div className="App">
        <label htmlFor="name">
          Digite um nome e mande um salve:
          <input type="text" id="name" value={ value } onChange={ this.handleChange } />
          <button type="button" onClick={ this.handleClick }>Mande um Salve</button>
          {!disable ? <h2>{ `Salve ${ value } !`}</h2> : '' }
          </label>
      </div>
    );
  }
}

export default App;
````
Rode o comando *npm start* para ver o funcionamento da aplicação.

Agora substitua o conteúdo do arquivo App.test.js pelo cópdigo abaixo.
````JS
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import App from './App';

describe('Testando o comportamento da aplicação', () => {
  it('Verifica se exibe um texto contendo "Salve" após clicar no botão', () => {
    render(<App />);
    const button = screen.getByRole('button');
    userEvent.click(button);
    const textAfterClick = screen.getByRole('heading', { level: 2 });
    expect(textAfterClick).toBeInTheDocument();
    expect(textAfterClick).toHaveTextContent("Salve");
  });
});
````

Vamos entender:

Após a renderização do componente `<App />`, nós recuperamos o botão utilizando o seletor *getByRole*. 
Em seguida, nós simulamos a interação de uma pessoa com nossa página no momento em que ela clicaria no botão.
````JS
render(<App />);
const button = screen.getByRole('button');
userEvent.click(button);
````

Após o *userEvent.click(button)*, nosso ambiente simulado entende que o botão foi clicado. Então podemos realizar nossos testes de acordo com o que acontece na página após o click.

````JS
const textAfterClick = screen.getByRole('heading', { level: 2 });
expect(textAfterClick).toBeInTheDocument();
expect(textAfterClick).toHaveTextContent("Salve");
````
Agora estamos recuperando um elemento `<h2>` utilizando também o seletor *getByRole* e testando se este elemento é renderizado após o click e se o mesmo elemento contém em seu texto a palavra "Salve".

 No momento dos exercícios poderemos por em prática e absover ainda mais os conceitos vistos até aqui. Mas antes, que tal um pequeno quizz para ajudar a fixar o conteúdo ?

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


<h3>---Ao rodar o comando 'npm test' o teste falhará.---</h3>
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

c) Se um elemento que inclui o texto "Minha música preferida" está renderizado na tela.

d) Se existe uma imagem renderizada na tela.

e) Se favoriteMusicElement possui a propriedade "Minha música preferida".
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

## Qual a sintaxe correta para o caso de querermos testar se um botão inclui o texto "Enviar" ?

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

