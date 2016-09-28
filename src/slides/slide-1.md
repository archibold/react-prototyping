name: inverse
layout: true
class: center, middle, inverse
---
class: title
# Prototypowanie z React'em
---
class: title
# Dlaczego prototypowanie?
---
## Idea → Prototyp → Design → Development → Produkt
---
## Łatwiej wyłapać błędy podczas designu
---
## Ponieważ prototypownie jest tanie, szybkie i proste
---
class: title
# Dlaczego React?
---
Po pierwsze, czym jest [React](https://facebook.github.io/react/) ?
---
## Prototypowanie w przegladarce jest trudne ponieważ...
---
### 1. Ciężko ponownie używać tych samych elementów
---
### 2. Cieżko pracuje się z danymi
---
### 3. Ciężko wykonywać i obsługiwać różnego rodzaju akcje
---

## React jest wystarczający do budowania realnie wyglądajacych mocków aplikacji
---
### 1. ~~Ciężko ponownie używać tych samych elementów~~
Używanie reactowych komponentów
---
### 2. ~~Cieżko się pracuje z danymi~~
Używanie Reactowych `props`'ów.
---
### 3. ~~Ciężko wykonywać i obsługiwać różnego rodzaju akcje~~
Używanie Reactowych `state`'ów i eventów.
---
class: title
# Nauczmy się tych czterech rzeczy...
---
## Components, props, state, i event'y
---

## 1. Components (komponenty)
---
Komponenty sa jak widgety lub moduły: Możemy z nich zbudować małe bloki interfejsu użytkownika i w łatwy sposób ich używać ponownie.
---
React zachęca nas do tworzenia małych struktur które można dalej wykorzystywać.
---
Używanie składni JSX ułatwia tworzenie komponentów.
---
```js
class HelloWorld extends React.Component {
    render() {
      return (
        <div className="hello-world">
          <p>Hello world!</p>
        </div>
      );
    }
}
```
---
```js
class App extends React.Component {
    render() {
      return (
        <section>
          <HelloWorld/>
          <HelloWorld/>
          <HelloWorld/>
        </section>
      );
    }
}
```
---

## 2. Props (właściwości)
---
Props = properties (właściwości)
---
Używamy ich podobnie jak atrybuty HTMLowych elementów
---
```html
<div class="foo" data-bar="bat">Wut</div>
```
---
Propsów używamy do przekazywania informacji w dół komponentu...
---
...te informacje mogą być użyte do zmieniania kontentu, zachowania badź wywoływania akcji
---
przekazanie props'u do komponentu renderuje komponent
---
```js
class App extends React.Component {
    render() {
      return (
        <section>
          <HelloWorld name="Piotr"/>
        </section>
      );
    }
}
```
---
```js
class HelloWorld extends React.Component {
    render() {
      return (
        <div className="hello-world">
          <p>Hello {this.props.name}!</p>
        </div>
      );
    }
}
```
---

## 3. State (stan komponentu)
---
Każdy komponent posiada własny `state`
---
Jeżeli zaktualizujesz `state`, komponent zostanie wyrenderowany na nowo
---
`state` używamy do podstawowych akcji jak otwieranie zamykanie dropdownów, lub symulowanie bazy danych
---
W realnych aplikacjach używanie `state` nie jest zalecane. W prototypowaniu jest to twój najlepszy przyjaciel
---
```js
class Example extends React.Component {
    getInitialState() {
      return {
        definition: false
      };
    },

    render() {...}
}
```
---
```js
class Example extends React.Component {
  getInitialState() {...},

  render() {
    return (
      <dl className="hello-world">
        <dt>Hello World!</dt>
        {this.state.definition ?
          <dd>A computer program that outputs "Hello, World!" (or some variant thereof) on a display device. Because it is typically one of the simplest programs possible in most programming languages, it is by tradition often used to illustrate to beginners the most basic syntax of a programming language.</dd>
        : null}
      </dl>
    );
  }
}
```
---
```js
class Example extends React.Component {
  getInitialState() {
    return {
      definition: false
    };
  },

  render() {
    return (
      <dl className="hello-world">
        <dt>Hello World!</dt>
        {this.state.definition ?
          <dd>A computer program that outputs "Hello, World!" (or some variant thereof) on a display device. Because it is typically one of the simplest programs possible in most programming languages, it is by tradition often used to illustrate to beginners the most basic syntax of a programming language.</dd>
        : null}
      </dl>
    );
  }
}
```
---
ten przykład nie jest interesujacy bez...
---

## 4. Events (Zdarzenia)
---
Zdarzenia pozwalaja wykonać nam akcje
---
Możesz używać różne typy zdarzeń i przypisać je do każdego elementu
---

__Przykład:__ kliknięcie przycisku i zaktualizowanie komponentu
---
```js
class Example extends React.Component {
    getInitialState() {...},

    handleDefinitionToggle() {...},

    render() {
        return (
            <dl className="hello-world">
                <dt>Hello World!</dt>
                {this.state.definition ?
                    <dd>A computer program that outputs "Hello, World!" (or some variant thereof) on a display device. Because it is typically one of the simplest programs possible in most programming languages, it is by tradition often used to illustrate to beginners the most basic syntax of a programming language.</dd>
                : null}
                <button onClick={this.handleDefinitionToggle}>Toggle definition</button>
            </dl>
            );
        }
    }
    ```
---
```js
class Example extends React.Component {
  getInitialState() {...},

  handleDefinitionToggle() {
    this.setState({definition: !this.state.definition});
  },

  render() {...}
}
```
---
```js
class Example extends React.Component {
  getInitialState() {
    return {
      definition: false
    };
  },

  handleDefinitionToggle() {
    this.setState({definition: !this.state.definition});
  },

  render() {
    return (
      <dl className="hello-world">
        <dt>Hello World!</dt>
        {this.state.definition ?
          <dd>A computer program that outputs "Hello, World!" (or some variant thereof) on a display device. Because it is typically one of the simplest programs possible in most programming languages, it is by tradition often used to illustrate to beginners the most basic syntax of a programming language.</dd>
        : null}
        <button onClick={this.handleDefinitionToggle}>Toggle definition</button>
      </dl>
    );
  }
}
```
---
Zapomnij o CSS'ach i pozwól wirtualnemu DOMowi załatwić sprawę
---
```js
// Maybe you've done it this way in the past...
$('.dropdown-menu').addClass('is-hidden');

// Or...
$('.dropdown-menu').hide();

// But in React you can...
class Dropdown extends React.Component {
  render() {
    return (
      <div className="dropdown">
        <button onClick={this.handleDropdownToggle}>More options</button>
        {this.state.dropdown ?
          <div className="dropdown-menu">...</div>
        : null}
      </div>
    );
  }
};
```
---
class: title
# Źródła
---
Prezentacja oparta na prezentacji autora [Andrew Liebchen](http://andrewliebchen.github.io/prototype-with-reactjs)
---
[podstawowe tutoriale z React'a](https://facebook.github.io/react/docs/tutorial.html)
---
ciekawa [seria artykułów](https://medium.com/react-tutorials) na Medium
---
[Prosty reactowy starter](https://github.com/facebookincubator/create-react-app)
---
[React + Webpack Yeoman generator](https://github.com/marcopeg/generator-reapp)
---
Napisz maila: [piotr.borysowski@gmail.com](mailto:piotr.borysowski@gmail.com)
