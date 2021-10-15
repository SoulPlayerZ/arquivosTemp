# Vamos praticar!


Chegou o melhor momento. :blush:
Agora é a hora de por em prática todo esse aprendizado de hoje.
Antes de iniciarmos os exercícios, vamos preprar nossa aplicação que será testada.
Lembre-se sempre de provocar uma falha nos testes para garantir que não está passando um falso positivo.
<br>
<br>


<u><h2>EXERCÍCIO 1</h2></u>

- Primeiro rode o comando *npx create-react-app sorteia-numero*

- Depois de instalada a aplicação, substitua o conteúdo do arquivo *App.js*, localizado na pasta *src*, pelo código abaixo:

````Javascript
import React from 'react';
import './App.css'

class App extends React.Component{
  constructor() {
    super();
    this.state = {
      disable: true,
      randomNumber: 0,
    }
  }

  handleClick = () => {
    this.setState({
      randomNumber: Math.floor(((Math.random() * 101))),
      disable: false,
    })
  }

  render() {
  const { randomNumber, disable } = this.state;
  return (
    <div>
      <h2>Clique para sortear um número entre 0 e 100</h2>
      <button type="button" onClick={ this.handleClick }>Sortear</button>
      {!disable
        ? 
          <>
            <h1>Número sorteado: { randomNumber }</h1>
            <img
              className="sage"
              src="https://vgraphs.com/images/players/sprays/high-quality/valorant-spray-all-good.png"
              alt="Sage joinha"
            />
          </>  
       : ''
      }
     
    </div>
  );
}
}

export default App;
````
<br>

- Rode o comando *npm start* para ver a aplicação no seu navegador.

- Agora vamos testar nossa aplicação :wink:

- Abra o arquivo *App.test.js*, localizado na pasta *src*, e substitua seu conteúdo pelo código abaixo:

````Javascript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import App from './App';

describe('Testa o comportamento do componente App.js', () => {
  it('Testa se o texto "Clique para sortear um número entre 0 e 100" é renderizado', () => {
    
  });
});
````

- Tudo pronto! Vamos praticar. :wink:
<br>
<br>

### 1 - Teste se o texto "Clique para sortear um número entre 0 e 100" é renderizado.

### 2 - Escreva um teste para verificar se um botão com o texto "Sortear" é renderizado.

### 3 - Verifique se, após clicar no botão, um elemento que contenha o texto "Número sorteado:" e uma imagem são exibidos na tela.

### 4 - Teste se a imagem possui o atributo "src" com a url(`https://vgraphs.com/images/players/sprays/high-quality/valorant-spray-all-good.png`);

<br>

<hr>
<u><h2>EXERCÍCIO 2 (Bônus)</h2></u>

Vamos testar uma aplicação simples que exibe uma imagem feliz para melhorar nosso dia :blush:

- Rode o comando npx *create-react-app imagem-feliz*.

- Substitua o conteúdo do arquivo *App.js*, localizado na pasta *src*, pelo código abaixo:


````Javascript
import { Component } from 'react';
import './App.css';

class App extends Component {
  constructor() {
    super();
    this.state = {
      disable: true,
    }
  }

  handleClick = () => {
    this.setState({
      disable: false,
    })

  }

  render() {
    const { disable } = this.state;
    const dogImage = (
      <section>
        <img
          className='dog'
          src="https://www.tupacity.com/img/2018/07/26/fileg_386550.jpg"
          alt="Cãozinho feliz"
        />
        <h2>Ficou Feliz ?</h2>
      </section>);
    return (
      <main className='App'>
        <header>
          <h2>Clique no botão e veja uma imagem feliz</h2>
        </header>
        <button type="button" onClick={ this.handleClick }>Fique feliz</button>
        {!disable ? dogImage : ''}
      </main>
    );
  }
}

export default App;
````


- Rode o comando *npm start* para ver a aplicação no seu navegador.

- Substitua o conteúdo do arquivo *App.test.js*, localizado na pasta *src*, pelo código abaixo:

````Javascript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import App from './App';

describe('Testa o comportamento do componente App.js', () => {

  it('Verifica se o título é renderizado', () => {

  });  
})
````
<br>
<br>


### 1 - Teste se o título está na tela ao renderizar o componente App.

### 2 - Verifique se existe um botão renderizado na tela.

### 3 - Teste se o botão possui o texto "Fique feliz".

### 4 - Faça um teste que verifica se uma imagem é rendizada após clicar no botão.

### 5 - Verifique se a imagem possui o atributo "src" com a url(`https://www.tupacity.com/img/2018/07/26/fileg_386550.jpg`)
