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
<br>

<b>a) </b>CERTA
<br>
*O melhor seletor a utilizar neste caso seria o "getByText". "getByTextIncludes" não existe. logo, nosso teste falhará.*
<br>
<br>

<s>b)</s> ERRADA
<br>
*Lembre-se sempre de consultar a [documentação](https://testing-library.com/docs/react-testing-library/cheatsheet/) em caso de dúvidas. "getByTextIncludes" não está correto.*
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

<s>a)</s> Se favoriteMusicElement tem o texto "Minha música preferida".
<br>
*Para realizarmos este teste poderíamos utilizar o matcher "toHaveTextContent" por exemplo.*
<br>
<br>

<s>b)</s> Se o elemento recuperado é um parágrafo.
<br>
*No código não podemos afirmar se o elemento recuperado é um `<p>`.*
<br>
<br>

<b>c) </b> Se um elemento que inclue o texto "Minha música preferida" está renderizado na tela.
<br>
*O seletor "getByText" recuperar um elemento pelo seu texto. E o matcher "toBeInTheDocument" verifica se este elemento é renderizado.*
<br>
<br>

<s>d)</s> Se existe uma imagem renderizada na tela.
<br>
*O detalhe aqui é que não recuperamos um elemento `<img>` por texto, mas poderíamos recuperar com o seletor "getByAltText".*
<br>
<br>


<s>e)</s> Se favoriteMusicElement é possui a propriedade "Minha música preferida".
<br>
*No código, estamos apenas testando se um determinado elemento é renderizado. Mas você pode tentar utilizar o matcher
"toHaveAttribute" para testar se um elemento possui um determinado atributo. Lembre-se de consultar sempre a [documentação](https://github.com/testing-library/jest-dom)*
<br>
<br>
<br>
<br>
<hr>

<u><h2>Questão 3</h2></u>

## O objetivo principal da React Testing Library(RTL) é:

<br>

<b>a)</b> Testar o comportamento da aplicação em diversas situações de acordo com os possíveis casos de uso.
<br>
*Quando utilizávamos Jest, o foco era cobrir nosso código e testar o retorno de nossas funções. 
Com a RTL nós testamos o comportamento da nossa aplicação.*
<br>
<br>

<s>b)</s> Substituir a biblioteca Enzyme para realizar testes em aplicações React.
<br>
*Além da preferência de quem está desenvolvendo os testes, existem cituações onde é melhor utilizar o Enzyme
e outras onde seria mais adequado utilizar o RTL. Nos recursos adicionais temos [este artigo](https://medium.com/wesionary-team/react-testing-library-vs-enzyme-afd29db380ac) que explica de forma mais detalhada algumas
diferenças entre as duas bibliotecas.*
<br>
<br>
<s>c)</s>  Garantir a cobertura de código das funções da nossa apllicação.
<br>
*O foco principal da biblioteca RTL é testar o comportamento da nossa aplicação.*
<br>
<br>
<s>d)</s>  Se tornar uma linguagem de programação.
<br>
*O objetivo da Rect Testing Library é, apenas testar nossas aplicações. rs*
<br>
<br>
<s>e)</s>  Tentar conquistar o mundo.
<br>
*Este é o objetivo princípal do Cérebro. Isso mesmo. Aquele do desenho. rs*
<br>
<br>
<br>
<br>
<hr>

<u><h2>Questão 4</h2></u>
<br>

## Qual a sintaxe correta para o caso de querermos testar se um botão inclue o texto "Enviar" ?
<br>

<s>a)</s> 
````JavaScript
render(<App />);
const button = screen.getByType('button');
expect(button).toHaveTextContent('Enviar');
````
*O seletor nesse caso seria o 'getByRole'. Sempre precisamos lembrar de consultar a [documentação](https://testing-library.com/docs/react-testing-library/cheatsheet/) quando temos alguma dúvida.*
<br>
<br>
<br>

<s>b)</s> 
````JavaScript
render(<App />);
expect(<button>).toBeInTheDocument();
````
*Precisamos usar um seletor para recuperar o botão antes de testá-lo. Semelhante a ideia de navegar pelo DOM com JavaScript:
EX: `document.getElementById('button-id')`.*
<br>
<br>
<br>

<s>c)</s> 
````JavaScript
render(<App />);
const button = screen.getByRole('button');
expect(button).toHaveTextContentIncludes('Enviar');
````
*O matcher que utilizamos para saber se algum elemento inclui algo em seu texto é toHaveTextContent. Consulte a 
[documentação](https://github.com/testing-library/jest-dom).*
<br>
<br>
<br>

<b>d)</b>
````JavaScript
render(<App />); 
const button = screen.getByRole('button');
expect(button).toHaveTextContent('Enviar');
````
*Após recuperar o botão ,testamos com o matcher toHaveTextContent, se palavra "Enviar" está incluso em seu texto.
O que passamos para o matcher 'toHaveTextContent' é o que queremos testar se está incluso no texto. O botão poderia ter o texto "Enviar Formulário".
O teste iria passar, já que "Enviar Formulário" contém a plavra "Enviar".*
<br>
<br>
<br>
 
<s>e)</s> 
````JavaScript
render(<App />);
const button = screen.getByRole('button');
expect(button).toHaveTextContent.includes('Enviar');
````
*O matcher correto para este teste seria somente "toHaveTextContent". "toHaveTextContent.includes" está incorreto.*
<br>
<br>
<br>
<br>

<hr>
<u><h2>Questão 5</h2></u>
<br>

## Qual das alternativas abaixo testa corretamente se uma imagem possui o atributo "src":
<br>


<s>a)</s>
````JavaScript
render(<App />)
const hatImage = screen.getByText(/hat/i);
expect(hatImage).toHaveAttribute('src'); 
````
*Não conseguimos recuperar imagem pelo seletor 'getByText'. Este seletor é utilizado 
quando queremos capturar um elemento pelo seu conteúdo texto. Com imagem podemos utilizar o 'getByAltText' por exemplo.*
<br>
<br>
<br>
 

<s>b)</s>
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute.SRC(); 
````
*Não existe uma função 'SRC' no matcher 'toHaveAttribute'.*
<br>
<br>
<br>
 

<b>c)</b>
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute('src'); 
````
*Estamos, após a renderização do componente `<App />` recuperando o componente imagem
através do texto da propriedade 'alt' da imagem. Em seguida testamos se a imagem possui o atibuto 'src' 
com o matcher 'toHaveAttribute' e indicando em string o atributo que queremos verificar.*
<br>
<br>
<br>
 


<s>d)</s>
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage).toHaveAttribute(src); 
````
*Aqui é um detalhe. Quando passamos para o matcher o atributo que estamos querendo testar, este deve ser passado
em formato string. Para este caso funcionar precisaríamos declarar uma const chamada src e passar o valor em string 'src' para ela.*
<br>
<br>
<br>
 

<s>e)</s>
````JavaScript
render(<App />)
const hatImage = screen.getByAltText(/hat/i);
expect(hatImage.attribute).toBe(src); 
````
*"attribute" não é um atributo da tag <img>, mas, a nível de curiosidade, você pode testar imagem.src e usar o matcher toBe para
testar se o valor do atributo src é um determinado valor, em string, passado ao matcher toBe. 
Lembre-se sempre de consultar a [documentação](https://github.com/testing-library/jest-dom) quando necessário.*
<br>
<br>
<br>


# Exercícios 


<br>


<u><h2>EXERCÍCIO 1</h2></u>

## 1 - Teste se o texto "Clique para sortear um número entre 0 e 100" é renderizado.
<br>

<u><h2>Solução</h2></u>
````JS
 it('Testa se o texto "Clique para sortear um número entre 0 e 100" é renderizado', () => {
    render(<App />);
    const headerText = screen.getByText(/número entre 0 e 100/i);
    expect(headerText).toBeInTheDocument();
  });
````
<br>
<br>

## 2 - Escreva um teste para verificar se um botão com o texto "Sortear" é renderizado.
<br>

<u><h2>Solução</h2></u>
````JS
 it('Testa se existe um botão com o texto "Sortear" renderizado na tela', () => {
    render(<App />);
    const button = screen.getByRole('button');
    expect(button).toBeInTheDocument();
    expect(button).toHaveTextContent('Sortear');
  });
````
<br>
<br>

## 3 - Verifique se, após clicar no botão, é exibido na tela um elemento que contenha o texto "Número sorteado:" e uma imagem.
<br>

<u><h2>Solução</h2></u>
````JS
  it('Verifica se, após clicar no botão, um elemento contendo o texto "Número sorteado:" e uma imagem são renderizados', () => {
      render(<App />);
      const button = screen.getByRole('button');
      userEvent.click(button);
      const textResult = screen.getByText(/sorteado/i);
      const image = screen.getByAltText("Sage joinha");
      expect(textResult).toBeInTheDocument();
      expect(image).toBeInTheDocument();
  });
````
<br>
<br>

## 4 - Teste se a imagem possui o atributo "src" com a url(`https://vgraphs.com/images/players/sprays/high-quality/valorant-spray-all-good.png`);
<br>

<u><h2>Solução</h2></u>
````JS
  it('Verifica se a imagem possui o atributo src e o valor deste atributo', () => {
      render(<App />);
      const button = screen.getByRole('button');
      userEvent.click(button);
      const image = screen.getByAltText("Sage joinha");
      expect(image).toHaveAttribute('src', `https://vgraphs.com/images/players/sprays/high-quality/valorant-spray-all-good.png`)
  });
````

<br>
<br>
<br>
<br>

<u><h2>EXERCÍCIO 2 (Bônus)</h2></u>


## 1 - Teste se o título está na tela ao renderizar o componente App.
<br>

<u><h2>Solução</h2></u>
````JavaScript
  it('Verifica se o título é renderizado', () => {
      render(<App />);
      const headerTitle = screen.getByText(/Clique no botão/i);
      expect(headerTitle).toBeInTheDocument();
    });
````
<br>
<br>

## 2 - Verifique se existe um botão renderizado na tela.
<br>

<u><h2>Solução</h2></u>
````JavaScript
  it('Verifica se um botão é renderizado na tela', () => {
    render(<App />);
    const btn = screen.getByRole('button');
    expect(btn).toBeInTheDocument();
  });
  ````
  <br>
  <br>

## 3 - Verifique se o botão possui o texto "Fique feliz".
<br>

<u><h2>Solução</h2></u>
````JavaScript
  it('Verifique se o botão possui o texto "Fique feliz"', () => {
    render(<App />);
    const btn = screen.getByRole('button');
    expect(btn).toHaveTextContent("Fique feliz");
  });
  ````
  <br>
  <br>

## 4 - Verifique se uma imagem é rendizada após clicar no botão.
<br>

<u><h2>Solução</h2></u>
````JS
 it('Verifica se uma imagem é renderizada ao clicar no botão', () => {
    render(<App />);
    const btn = screen.getByRole('button');
    userEvent.click(btn);
    const dogImage = screen.getByAltText(/Cãozinho feliz/i);
    expect(dogImage).toBeInTheDocument();
  });
````
<br>
<br>

## 5 - Verifique se a imagem possui o atributo "src" com a url(`https://www.tupacity.com/img/2018/07/26/fileg_386550.jpg`)
<br>

<u><h2>Solução</h2></u>
````JavaScript
 it('Verifique se a imagem possui o atributo "src" com a url(`https://www.tupacity.com/img/2018/07/26/fileg_386550.jpg`)', () => {
    render(<App />);
    const btn = screen.getByRole('button');
    userEvent.click(btn);
    const dogImage = screen.getByAltText(/Cãozinho feliz/i);
    expect(dogImage).toHaveAttribute('src', `https://www.tupacity.com/img/2018/07/26/fileg_386550.jpg`); 
  });
  ````

