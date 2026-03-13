# Anotações de melhoria – Portfólio

Este documento explica as melhorias feitas no código HTML e CSS do portfólio.
O objetivo das mudanças foi melhorar principalmente:

* Organização do HTML
* Semântica
* Responsividade
* Legibilidade do código
* Boas práticas de CSS
* Segurança básica em links externos

---

# 1. Estrutura do menu de navegação

## Antes

O menu era feito apenas com links diretamente dentro da tag `nav`.

```html
<nav>
    <a href="#">Linkedin</a>
    <a href="#">GitHub</a>
    <a href="#">Instagram</a>
</nav>
```

## Depois

Agora o menu utiliza **lista não ordenada (`ul`) e itens de lista (`li`)**.

```html
<nav>
    <ul>
        <li><a href="#">Linkedin</a></li>
        <li><a href="#">GitHub</a></li>
        <li><a href="#">Instagram</a></li>
    </ul>
</nav>
```

## Por que isso é melhor?

Menus de navegação **são semanticamente listas de links**.

Usar `ul` e `li` traz benefícios como:

* Melhor semântica HTML
* Melhor acessibilidade (leitores de tela entendem melhor)
* Estrutura mais fácil de estilizar no CSS
* Segue boas práticas da web

---

# 2. Uso de Flexbox no menu

Foi adicionado `display: flex` para organizar os itens do menu.

```css
header nav ul {
    display: flex;
    justify-content: center;
}
```

## O que é Flexbox?

Flexbox é um **sistema de layout do CSS** que facilita alinhar e distribuir elementos.

Neste caso ele foi usado para:

* alinhar os links horizontalmente
* centralizar o menu na página

Sem Flexbox seria necessário usar `inline-block`, `float` ou outros métodos mais limitados.

Também foi usado:

```CSS
gap: 0.625rem;
```

O ```gap``` cria espaço entre os elementos sem precisar usar ```margin```.

---

# 3. Reset CSS e Box Sizing

Foi adicionado no início do CSS:

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

## Por que isso foi adicionado?

### Reset de margin e padding

Cada navegador aplica estilos padrão diferentes.

Remover `margin` e `padding` evita comportamentos inesperados.

### box-sizing: border-box

Por padrão o CSS calcula largura assim:

```
width + padding + border
```

Com `border-box` o cálculo fica:

```
width = conteúdo + padding + border
```

Isso torna o layout **muito mais previsível**, principalmente em layouts responsivos.

---

# 4. Fontes e importação do Google Fonts

Foi adicionado `@import` do Google Fonts e definidas duas fontes no projeto:

* `Roboto` como fonte padrão
* `Revalia` como fonte de destaque

```css
@import url('https://fonts.googleapis.com/css2?family=Revalia&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap');
```

```css
:root {
    --fonte-padrao: "Roboto", arial, verdana, helvetica, sans-serif;
    --fonte-destaque: 'revalia', sans-serif;
}
```

E aplicada:

```css
body {
    font-family: var(--fonte-padrao);
}
```

## Por que isso melhora o código?

* Centraliza a definição das fontes
* Facilita manutenção
* Permite trocar o visual alterando apenas variáveis

---

# 5. Uso de variáveis CSS

O projeto já utilizava variáveis CSS:

```css
:root {
    --cor0: #6C6C6C;
    --cor1: #121212;
    --cor2: #95999A;
    --cor3: #5256AB;
    --cor4: #887CFF;
}
```

Isso é uma boa prática porque:

* evita repetir cores várias vezes
* facilita mudanças futuras
* melhora a organização do código

---

# 6. Fonte de destaque nos títulos

Os títulos principais passaram a usar a fonte de destaque.

```css
header h1,
.secao-sobre h2,
.secao-experiencia h2,
.secao-formacao h2,
.secao-diferenciais h2 {
    font-family: var(--fonte-destaque);
    color: var(--cor4);
    margin-bottom: 1rem;
}
```

Isso dá identidade visual sem perder legibilidade.

# 7. Hierarquia correta dos títulos

A estrutura de títulos ficou organizada assim:

```
h1 → título principal da página
h2 → seções principais
h3 → subtítulos
```

Isso melhora a **hierarquia semântica dos títulos**.

Isso ajuda:

* SEO
* leitores de tela
* organização do conteúdo

---

# 8. Classes por seção

Foram adicionadas classes nas `section` para facilitar a estilização:

```html
<section class="secao-sobre">
<section class="secao-experiencia">
<section class="secao-formacao">
<section class="secao-diferenciais">
```

Com isso o CSS ficou mais direto e organizado, por exemplo:

```css
.secao-sobre h2 { ... }
.secao-experiencia article { ... }
```

---

# 9. Melhor organização do layout com Flexbox

O `main` agora usa flexbox.

```css
main {
    display: flex;
    flex-direction: column;
    gap: 1.875rem;
}
```

## O que isso faz?

* organiza os elementos em **coluna**
* centraliza o conteúdo
* cria espaçamento automático entre seções (`gap`)

Isso deixa o layout **mais limpo e fácil de controlar**.

---

# 10. Controle de largura do conteúdo

Foi definido um limite para o conteúdo principal.

```CSS
max-width: 56.25rem;
margin: auto;
```

Isso impede que o conteúdo fique muito largo em telas grandes.

Além disso os parágrafos usam:

```CSS
max-width: 100ch;
```

```ch``` representa aproximadamente a largura de um caractere.

Isso limita o tamanho das linhas de texto, melhorando a leitura.
Linhas muito longas são cansativas para o usuário.

---

# 11. Melhor tratamento da imagem

A imagem foi ajustada para ser responsiva.

```CSS
main picture img {
    width: 100%;
    max-width: 37.5rem;
    height: auto;
}
```

Isso garante que:

* a imagem nunca ultrapasse o container
* a proporção original seja mantida
* a imagem funcione bem em telas pequenas

---

# 12. Uso de unidades relativas (rem)

Algumas medidas foram convertidas para rem.

Exemplo:

```CSS 
4.375rem
1.25rem
0.9375rem
```

## O que é ```rem```?

```rem``` é uma unidade baseada no tamanho da fonte raiz do navegador.

Normalmente:

```
1rem = 16px
```

Benefícios:

* melhor acessibilidade
* layouts mais flexíveis
* adaptação melhor quando o usuário aumenta o tamanho da fonte

--- 

# 13. Segurança em links externos

Nos links que abrem em nova aba foi adicionado:

```HTML
rel="noopener noreferrer"
```
Exemplo:

```HTML
<a href="..." target="_blank" rel="noopener noreferrer">
```
Isso é uma **boa prática de segurança**.

Evita que a página aberta tenha acesso à página original através de ```window.opener```.
Além disso melhora a segurança e a performance.

--- 

# 14. Organização das experiências

Cada experiência ficou em um bloco separado dentro da seção:

```HTML
<section class="secao-experiencia">
    <article>
        <div>...</div>
        <div>...</div>
    </article>
</section>
```

E no CSS:

```css
.secao-experiencia article {
    display: flex;
    flex-direction: column;
}
```

Isso deixa a leitura mais clara e facilita ajustes de layout.

---

# 15. Responsividade com Media Query

Foi adicionada:

```css
@media (max-width: 620px) {
    main {
        padding: 1rem;
    }

    header nav ul {
        flex-direction: column;
        align-items: center;
        gap: 1.5625rem;
    }
}
```

## O que é uma Media Query?

Media Queries permitem aplicar CSS **dependendo do tamanho da tela**.

Neste caso:

Se a tela for **menor que 620px**, o padding diminui.

Isso melhora a visualização em:

* celulares
* telas pequenas

# 16. Pequenas melhorias de gerais

Também foram feitas pequenas melhorias como:

* padronização de espaçamentos
* uso consistente de unidades relativas
* simplificação de seletores CSS
* melhor organização do HTML
* melhoria na legibilidade do código
* gradiente no `header` e sombra no `main` para dar profundidade
* marcador de lista com check na seção de cursos

---

# Conclusão

As melhorias realizadas tornaram o projeto:

* mais semântico
* mais organizado
* mais responsivo
* mais acessível
* mais fácil de manter

Agora o código segue práticas mais próximas do que é utilizado em projetos profissionais de front-end.
