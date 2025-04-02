---
layout: "../../layouts/BlogPost.astro"
title: "Building a React and Stripe Shopping Cart Application: A Comprehensive Guide"
pubDate: "2025-03-01 14:13:42.983119"
youtubeVideoID: "_8M-YVY76O8"
index:
---

# Building a React and Stripe Shopping Cart Application: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/_8M-YVY76O8" frameborder="0" allowfullscreen></iframe>


This chapter will guide you through the process of building a fully functional e-commerce shopping cart application using React for the front-end and Stripe for payment processing. We will explore how to create a dynamic user interface, manage cart state, and integrate with the Stripe API to handle secure online transactions. This project is designed to be a valuable learning experience, covering essential concepts in modern web development.

## Introduction

This project aims to create an e-commerce platform where users can browse products, add them to a cart, view their cart summary, and securely checkout using Stripe.  This chapter will walk you through each step, from setting up the React front-end to integrating a basic Express.js back-end for handling Stripe API interactions.

## Project Overview: E-commerce Store Functionality

The application we will build will feature the following functionalities:

*   **Product Catalog:** Display a list of available products with names, prices, and "Add to Cart" buttons.
*   **Shopping Cart:**
    *   A cart icon in the navigation bar that visually indicates the number of items in the cart.
    *   A modal (pop-up window) that displays the items currently in the cart, including quantities and individual item prices.
    *   Functionality to increase, decrease, and remove items from the cart.
    *   A dynamic cart total that updates as items are added or removed.
*   **Stripe Integration:**
    *   Upon clicking a "Purchase Items" button, users will be redirected to Stripe's secure checkout page.
    *   The Stripe checkout will reflect the items and quantities in the user's cart.
    *   Successful payments will be processed through Stripe, and a confirmation message will be displayed.
    *   A Stripe dashboard will demonstrate successful payment processing and transaction details.
*   **Routing:** Utilizing React Router to handle navigation between different "pages" such as the store, success, and cancel pages.
*   **Styling:** Implementing React Bootstrap and Bootstrap CSS for visually appealing and responsive components.

## Setting Up the React Front-End

### Creating a New React Application

To begin, we will create a new React application. This provides the foundation for our user interface and component structure.

1.  **Open your terminal.**
2.  **Navigate to your desired project directory.**
3.  **Use `create-react-app` to generate a new React project:**

    ```bash
    npx create-react-app store
    ```

    > `npx create-react-app`: This command utilizes `npx`, the Node Package eXecutor, to run the `create-react-app` package, a tool for quickly setting up a new React project with a pre-configured build process and development environment.

4.  **Navigate into the newly created project directory:**

    ```bash
    cd store
    ```

### Installing Dependencies

Our React application will require several packages to implement the desired features and styling.

1.  **Install necessary npm packages:**

    ```bash
    npm install bootstrap react-bootstrap react-router-dom
    ```

    *   `bootstrap`: A popular CSS framework for responsive and mobile-first front-end development.
    *   `react-bootstrap`: A library of React components built using Bootstrap, providing pre-styled and functional UI elements.
    *   `react-router-dom`: A library for declarative routing in React applications, enabling navigation between different views or pages.

2.  **Start the React development server to verify setup:**

    ```bash
    npm start
    ```

    This command will compile your React application and open it in your default web browser, typically at `http://localhost:3000`. You should see the default React boilerplate application running.

### Structuring Components

To organize our React application effectively, we will create dedicated folders for components and pages within the `src` directory.

1.  **Create a `components` folder inside the `src` folder.** This folder will house reusable UI components such as the Navbar and Product Cards.
2.  **Create a `pages` folder inside the `src` folder.** This folder will contain components representing different routes or views of our application, like the Store page, Success page, and Cancel page.

## Building Front-End Components

### Navbar Component

The navigation bar, or Navbar, is a crucial element for user navigation and displaying essential information like the shopping cart.

1.  **Create `Navbar.js` inside the `components` folder.**
2.  **Initialize a functional component named `NavbarComponent`:**

    ```javascript
    import React from 'react';
    import { Button, Container, Navbar, Modal } from 'react-bootstrap';

    function NavbarComponent() {
      return (
        // Navbar content will be added here
        <div>Navbar</div>
      );
    }

    export default NavbarComponent;
    ```

3.  **Import necessary components from `react-bootstrap`:** `Button`, `Container`, `Navbar`, and `Modal`. The `Modal` component will be used for the shopping cart display.
4.  **Implement the Navbar structure using React Bootstrap components:**

    ```javascript
    import React, { useState } from 'react'; // Import useState hook
    import { Button, Container, Navbar, Modal } from 'react-bootstrap';

    function NavbarComponent() {
      const [showCart, setShowCart] = useState(false); // State to control modal visibility
      const handleCloseCart = () => setShowCart(false);
      const handleShowCart = () => setShowCart(true);

      return (
        <> {/* React Fragment to group elements without extra DOM node */}
          <Navbar expand="sm" className="bg-body-tertiary">
            <Container>
              <Navbar.Brand href="/">E-commerce Store</Navbar.Brand>
              <Navbar.Toggle aria-controls="basic-navbar-nav" />
              <Navbar.Collapse id="basic-navbar-nav" className="justify-content-end">
                <Button onClick={handleShowCart}>Cart (0 Items)</Button> {/* Cart Button to trigger modal */}
              </Navbar.Collapse>
            </Container>
          </Navbar>
          <Modal show={showCart} onHide={handleCloseCart}> {/* Modal component for cart */}
            <Modal.Header closeButton>
              <Modal.Title>Shopping Cart</Modal.Title>
            </Modal.Header>
            <Modal.Body>
              <h1>This is the modal body</h1> {/* Placeholder for cart content */}
            </Modal.Body>
          </Modal>
        </>
      );
    }

    export default NavbarComponent;
    ```

    *   `useState`: A React Hook used to manage state within functional components. In this case, it controls the visibility of the cart modal (`showCart`).
    *   `Navbar`: The main navigation bar component.
    *   `Navbar.Brand`:  The title or logo of the website, often a link to the homepage.
    *   `Navbar.Toggle`:  A button that appears on smaller screens to collapse and expand the navigation menu.
    *   `Navbar.Collapse`:  The collapsible section of the navbar, containing navigation links or buttons.
    *   `Button`: A standard button component, used here for the "Cart" button.
    *   `Modal`:  A component to create a pop-up window that overlays the main content, used for displaying the shopping cart.
    *   `Modal.Header`, `Modal.Title`, `Modal.Body`:  Sub-components of `Modal` to structure its content.
    *   `expand="sm"`:  Navbar property to determine when the navbar collapses (on small screens and below).
    *   `className="justify-content-end"`: Bootstrap class to align content to the right within the Navbar Collapse.
    *   `onClick={handleShowCart}` and `onClick={handleCloseCart}`: Event handlers to control the modal visibility state.
    *   `show={showCart}` and `onHide={handleCloseCart}`: Modal properties to bind the modal's visibility to the `showCart` state and handle closing events.

5.  **Import and use `NavbarComponent` in `App.js`:**

    ```javascript
    import React from 'react';
    import NavbarComponent from './components/Navbar';
    import 'bootstrap/dist/css/bootstrap.min.css'; // Import Bootstrap CSS

    function App() {
      return (
        <Container> {/* Container for centering content */}
          <NavbarComponent />
          {/* Application content will be added below Navbar */}
          <div>
            {/* ... */}
          </div>
        </Container>
      );
    }

    export default App;
    ```

    *   `import 'bootstrap/dist/css/bootstrap.min.css';`:  Crucially import Bootstrap CSS in `App.js` to apply Bootstrap styling to React Bootstrap components.
    *   `Container`: A React Bootstrap component used to center and constrain content within a page.

### Implementing React Router for Navigation

To handle different pages within our application, we will utilize React Router.

1.  **Import necessary components from `react-router-dom` in `App.js`:** `BrowserRouter`, `Routes`, and `Route`.
2.  **Structure the `App.js` component with routing:**

    ```javascript
    import React from 'react';
    import NavbarComponent from './components/Navbar';
    import Store from './pages/Store'; // Import Store page component
    import Success from './pages/Success'; // Import Success page component
    import Cancel from './pages/Cancel';   // Import Cancel page component
    import { Container } from 'react-bootstrap';
    import 'bootstrap/dist/css/bootstrap.min.css';
    import { BrowserRouter, Routes, Route } from 'react-router-dom';

    function App() {
      return (
        <Container>
          <BrowserRouter> {/* BrowserRouter to enable routing */}
            <NavbarComponent />
            <Routes> {/* Routes component to define different paths */}
              <Route index element={<Store />} /> {/* Route for the home page (index path) */}
              <Route path="success" element={<Success />} /> {/* Route for /success path */}
              <Route path="cancel" element={<Cancel />} />   {/* Route for /cancel path */}
            </Routes>
          </BrowserRouter>
        </Container>
      );
    }

    export default App;
    ```

    *   `BrowserRouter`:  Provides the routing context to the application, enabling navigation using URLs.
    *   `Routes`:  A container for defining individual `Route` components.
    *   `Route`:  Defines a mapping between a URL path and a component to render.
    *   `index`:  A property of `Route` that specifies this route should match the base path (`/`).
    *   `path`:  A property of `Route` that defines the URL path to match.
    *   `element`:  A property of `Route` that specifies the React component to render when the path is matched.

3.  **Create basic page components in the `pages` folder:** `Store.js`, `Success.js`, and `Cancel.js`.

    *   **`Store.js`:**

        ```javascript
        import React from 'react';

        function Store() {
          return (
            <h1>Welcome to the store</h1>
          );
        }

        export default Store;
        ```

    *   **`Cancel.js`:**

        ```javascript
        import React from 'react';

        function Cancel() {
          return (
            <h1>Sorry to see you canceled your Stripe payment!</h1>
          );
        }

        export default Cancel;
        ```

    *   **`Success.js`:**

        ```javascript
        import React from 'react';

        function Success() {
          return (
            <h1>Thank you for your purchase!</h1>
          );
        }

        export default Success;
        ```

    These basic page components are placeholders and will be expanded upon later.

### Displaying Products in the Store

To dynamically display products, we will create product data and use it to render product cards in the `Store` page.

1.  **Create `productsStore.js` in the `src` folder.** This file will store product data and helper functions.

2.  **Define product data as an array of objects:**

    ```javascript
    const productsArray = [
      { id: "1", title: "Coffee", price: 4.99 },
      { id: "2", title: "Sunglasses", price: 9.99 },
      { id: "3", title: "Camera", price: 39.99 },
    ];

    function getProductData(id) {
      let productData = productsArray.find(product => product.id === id);
      if (productData === undefined) {
        console.log("Product data does not exist for ID: " + id);
        return undefined;
      }
      return productData;
    }

    export { productsArray, getProductData };
    ```

    *   `productsArray`: An array holding objects, each representing a product with `id`, `title`, and `price` properties.
    *   `getProductData(id)`: A function that searches `productsArray` for a product with a matching `id` and returns the product object. If no product is found, it logs an error and returns `undefined`.
    *   `export { productsArray, getProductData }`: Exports the `productsArray` and `getProductData` function to be used in other components.

3.  **Import `productsArray` and `Row`, `Col` from `react-bootstrap` in `Store.js`.**
4.  **Render product columns using `productsArray.map`:**

    ```javascript
    import React from 'react';
    import { Row, Col } from 'react-bootstrap';
    import { productsArray } from '../productsStore';

    function Store() {
      return (
        <> {/* React Fragment */}
          <h1>Welcome to the store</h1>
          <Row xs={1} md={3} className="g-4"> {/* Row to arrange columns */}
            {productsArray.map((product, index) => (
              <Col align="center" key={index}> {/* Column for each product */}
                <h1>{product.title}</h1> {/* Display product title */}
              </Col>
            ))}
          </Row>
        </>
      );
    }

    export default Store;
    ```

    *   `Row xs={1} md={3} className="g-4"`: React Bootstrap `Row` component to structure products in a grid layout.
        *   `xs={1}`:  Specifies one column on extra-small screens.
        *   `md={3}`:  Specifies three columns on medium screens and larger.
        *   `className="g-4"`: Bootstrap class to add gutters (spacing) between columns.
    *   `productsArray.map((product, index) => ...)`:  Iterates over each product in `productsArray` using the `map` function to render a `Col` component for each product.
    *   `key={index}`:  A unique key prop is important when rendering lists in React, using the index is acceptable in this case as the product array order is not changing dynamically.

### Creating Product Card Components

To enhance the visual representation of products, we will create a dedicated `ProductCard` component.

1.  **Create `ProductCard.js` in the `components` folder.**
2.  **Initialize a functional component named `ProductCard` that accepts `props`:**

    ```javascript
    import React from 'react';
    import { Card, Button, Form, Row, Col } from 'react-bootstrap';

    function ProductCard(props) {
      const product = props.product; // Access product data from props

      return (
        <Card>
          <Card.Body>
            <Card.Title>{product.title}</Card.Title> {/* Display product title */}
            <Card.Text>${product.price}</Card.Text> {/* Display product price */}
            <Button variant="primary">Add to cart</Button> {/* Add to cart button */}
          </Card.Body>
        </Card>
      );
    }

    export default ProductCard;
    ```

    *   `props`:  Short for "properties," props are input values passed to React components, allowing them to be configured and rendered dynamically.
    *   `props.product`: Accesses the `product` prop passed to the `ProductCard` component.
    *   `Card`, `Card.Body`, `Card.Title`, `Card.Text`, `Button`: React Bootstrap components used to create a styled product card.
    *   `variant="primary"`:  Bootstrap button variant to set the button color to primary (typically blue).

3.  **Import and use `ProductCard` in `Store.js`:**

    ```javascript
    import React from 'react';
    import { Row, Col } from 'react-bootstrap';
    import { productsArray } from '../productsStore';
    import ProductCard from '../components/ProductCard'; // Import ProductCard component

    function Store() {
      return (
        <>
          <h1>Welcome to the store</h1>
          <Row xs={1} md={3} className="g-4">
            {productsArray.map((product, index) => (
              <Col align="center" key={index}>
                <ProductCard product={product} /> {/* Render ProductCard component */}
              </Col>
            ))}
          </Row>
        </>
      );
    }

    export default Store;
    ```

    *   `<ProductCard product={product} />`:  Renders the `ProductCard` component, passing the current `product` object from the `map` iteration as a prop. This makes product-specific data available within the `ProductCard` component.

## Implementing Cart Functionality with Context

To manage the shopping cart state across the application, we will use React Context.

### Creating Cart Context

React Context provides a way to share values like cart data and cart management functions between components without explicitly passing props through every level of the component tree.

1.  **Create `CartContext.js` in the `src` folder.**

2.  **Import `createContext` and `useState` from React.**

3.  **Create a cart context using `createContext`:**

    ```javascript
    import React, { createContext, useState } from 'react';
    import { productsArray, getProductData } from './productsStore'; // Import product data

    export const CartContext = createContext({
      items: [],
      getProductQuantity: () => {},
      addOneToCart: () => {},
      removeOneFromCart: () => {},
      deleteFromCart: () => {},
      getTotalCost: () => {}
    });

    export function CartProvider({ children }) {
      // Cart Provider implementation will be added here
    }

    export default CartProvider;
    ```

    *   `createContext`: A React function to create a context object.
    *   `CartContext`: The created context object. It is initialized with a default value object containing:
        *   `items`: An array to store cart items.
        *   Cart management functions: `getProductQuantity`, `addOneToCart`, `removeOneFromCart`, `deleteFromCart`, and `getTotalCost`. These are initially empty functions as placeholders.
    *   `CartProvider`: A functional component that will provide the cart context to its children components.
    *   `{ children }`:  Destructuring props to access the `children` prop, which represents the components wrapped by `CartProvider`.

4.  **Implement `CartProvider` to manage cart state and functions:**

    ```javascript
    import React, { createContext, useState } from 'react';
    import { productsArray, getProductData } from './productsStore';

    export const CartContext = createContext({ /* ... (context definition from above) ... */ });

    export function CartProvider({ children }) {
      const [cartProducts, setCartProducts] = useState([]); // State to hold cart items

      function getProductQuantity(id) {
        const quantity = cartProducts.find(product => product.id === id)?.quantity;
        if (quantity === undefined) {
          return 0;
        }
        return quantity;
      }

      function addOneToCart(id) {
        const quantity = getProductQuantity(id);

        if (quantity === 0) { // Item not in cart
          setCartProducts(
            [
              ...cartProducts, // Spread operator to include existing cart items
              {
                id: id,
                quantity: 1
              }
            ]
          )
        } else { // Item in cart
          setCartProducts(
            cartProducts.map(
              product => product.id === id // If condition to find the item
              ? { ...product, quantity: product.quantity + 1 } // Update quantity if item found
              : product // Otherwise return the original product
            )
          )
        }
      }

      function removeOneFromCart(id) {
        const quantity = getProductQuantity(id);

        if(quantity === 1) {
          deleteFromCart(id);
        } else {
          setCartProducts(
            cartProducts.map(
              product => product.id === id
              ? { ...product, quantity: product.quantity - 1 }
              : product
            )
          )
        }
      }

      function deleteFromCart(id) {
        setCartProducts(
          cartProducts =>
          cartProducts.filter(currentProduct => {
            return currentProduct.id !== id;
          })
        )
      }

      function getTotalCost() {
        let totalCost = 0;
        cartProducts.map((cartItem) => {
          const productData = getProductData(cartItem.id);
          totalCost += productData.price * cartItem.quantity;
          return null; // Added return null as map expects a return value, but we are not using it here.
        });
        return totalCost;
      }

      const contextValue = { // Value object passed to context provider
        items: cartProducts,
        getProductQuantity,
        addOneToCart,
        removeOneFromCart,
        deleteFromCart,
        getTotalCost
      };

      return (
        <CartContext.Provider value={contextValue}> {/* Context Provider component */}
          {children} {/* Render child components */}
        </CartContext.Provider>
      );
    }

    export default CartProvider;
    ```

    *   `const [cartProducts, setCartProducts] = useState([])`:  Uses `useState` to create a state variable `cartProducts` (initialized as an empty array) to store cart items and a setter function `setCartProducts` to update it.
    *   `getProductQuantity(id)`:  Retrieves the quantity of a product in the cart based on its `id`. It uses `cartProducts.find()` to locate the product and returns its `quantity` or `0` if not found.
    *   `addOneToCart(id)`:  Adds one unit of a product to the cart. If the product is not already in the cart, it adds a new item with a quantity of 1. If it is in the cart, it increments the quantity.
        *   `...cartProducts`: The spread syntax is used to create a new array that includes all existing `cartProducts` items, ensuring immutability.
        *   `cartProducts.map(...)`: The `map` function iterates over `cartProducts` to update the quantity of an existing product.
        *   Ternary operator (`condition ? valueIfTrue : valueIfFalse`) is used within `map` for concise conditional logic.
    *   `removeOneFromCart(id)`:  Removes one unit of a product from the cart. If the quantity is 1, it calls `deleteFromCart` to remove the item entirely. Otherwise, it decrements the quantity.
    *   `deleteFromCart(id)`:  Removes a product entirely from the cart based on its `id`. It uses `cartProducts.filter()` to create a new array excluding the product with the matching `id`.
        *   `cartProducts.filter(...)`: The `filter` function creates a new array containing only elements that pass a provided condition.
    *   `getTotalCost()`: Calculates the total cost of all items in the cart. It iterates over `cartProducts`, retrieves product data using `getProductData`, and sums up the cost based on price and quantity.
    *   `contextValue`: An object containing all the cart-related values and functions that will be provided by the context.
    *   `<CartContext.Provider value={contextValue}>`: The `CartContext.Provider` component makes the `contextValue` available to all child components wrapped within it.
    *   `{children}`: Renders the child components that will have access to the cart context.

5.  **Wrap the `App` component with `CartProvider` in `index.js`:**

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import App from './App';
    import CartProvider from './CartContext'; // Import CartProvider

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
      <CartProvider> {/* Wrap App with CartProvider */}
        <App />
      </CartProvider>
    );
    ```

    This step ensures that the cart context is available throughout your entire application.

### Using Cart Context in Components

Now that the cart context is set up, we can access and use it in various components, such as `ProductCard` and `NavbarComponent`.

1.  **Import `CartContext` and `useContext` in `ProductCard.js` and `NavbarComponent.js`.**

2.  **Access the cart context using `useContext(CartContext)`:**

    *   **In `ProductCard.js`:**

        ```javascript
        import React, { useContext } from 'react'; // Import useContext hook
        import { Card, Button, Form, Row, Col } from 'react-bootstrap';
        import { CartContext } from '../CartContext'; // Import CartContext

        function ProductCard(props) {
          const product = props.product;
          const cart = useContext(CartContext); // Access cart context
          const productQuantity = cart.getProductQuantity(product.id); // Get quantity from context

          return (
            <Card>
              <Card.Body>
                <Card.Title>{product.title}</Card.Title>
                <Card.Text>${product.price}</Card.Text>
                { productQuantity > 0 ? // Conditional rendering based on quantity
                  <>
                    <Form as={Row}>
                      <Form.Label column sm="6">In Cart: </Form.Label>
                      <Col sm="6">
                        {productQuantity}
                      </Col>
                    </Form>
                    <Button variant="outline-danger" size="sm" onClick={() => cart.removeOneFromCart(product.id)}>-</Button> {/* Remove one button */}
                    <Button variant="outline-success" size="sm" onClick={() => cart.addOneToCart(product.id)} className="ms-2">+</Button> {/* Add one button */}
                    <Button variant="danger" size="sm" onClick={() => cart.deleteFromCart(product.id)} className="my-2">Remove from cart</Button> {/* Delete from cart button */}
                  </>
                  :
                  <Button variant="primary" onClick={() => cart.addOneToCart(product.id)}>Add to cart</Button> {/* Add to cart button if quantity is zero */}
                }
              </Card.Body>
            </Card>
          );
        }

        export default ProductCard;
        ```

        *   `useContext(CartContext)`:  A React Hook that consumes the `CartContext` value, providing access to the `cart` object containing cart data and functions.
        *   `cart.getProductQuantity(product.id)`:  Calls the `getProductQuantity` function from the context to get the current quantity of the product in the cart.
        *   Conditional rendering (`productQuantity > 0 ? ... : ...`) is used to display different UI elements based on whether the product is in the cart or not.
        *   `onClick={() => cart.addOneToCart(product.id)}`, `onClick={() => cart.removeOneFromCart(product.id)}`, `onClick={() => cart.deleteFromCart(product.id)}`:  Event handlers attached to buttons that call the respective cart management functions from the context, passing the product `id`.

    *   **In `NavbarComponent.js`:**

        ```javascript
        import React, { useState, useContext } from 'react';
        import { Button, Container, Navbar, Modal } from 'react-bootstrap';
        import { CartContext } from '../CartContext'; // Import CartContext
        import CartProduct from './CartProduct'; // Import CartProduct component

        function NavbarComponent() {
          const [showCart, setShowCart] = useState(false);
          const handleCloseCart = () => setShowCart(false);
          const handleShowCart = () => setShowCart(true);
          const cart = useContext(CartContext); // Access cart context
          const productsCount = cart.items.reduce((sum, product) => sum + product.quantity, 0); // Calculate total product count

          return (
            <>
              <Navbar expand="sm" className="bg-body-tertiary">
                <Container>
                  <Navbar.Brand href="/">E-commerce Store</Navbar.Brand>
                  <Navbar.Toggle aria-controls="basic-navbar-nav" />
                  <Navbar.Collapse id="basic-navbar-nav" className="justify-content-end">
                    <Button onClick={handleShowCart}>Cart ({productsCount} Items)</Button> {/* Dynamic cart item count */}
                  </Navbar.Collapse>
                </Container>
              </Navbar>
              <Modal show={showCart} onHide={handleCloseCart}>
                <Modal.Header closeButton>
                  <Modal.Title>Shopping Cart</Modal.Title>
                </Modal.Header>
                <Modal.Body>
                  {productsCount > 0 ? // Conditional rendering for cart items
                    <>
                      <h1>Items in your cart:</h1>
                      {cart.items.map((currentProduct, index) => (
                        <CartProduct key={index} id={currentProduct.id} quantity={currentProduct.quantity}></CartProduct> // Render CartProduct components
                      ))}
                      <h1>Total: {cart.getTotalCost().toFixed(2)}</h1> {/* Display total cost */}
                      <Button variant="success">Purchase items!</Button> {/* Purchase button */}
                    </>
                    :
                    <h1>There are no items in your cart!</h1> // Message if cart is empty
                  }
                </Modal.Body>
              </Modal>
            </>
          );
        }

        export default NavbarComponent;
        ```

        *   `useContext(CartContext)`: Accesses the cart context.
        *   `const productsCount = cart.items.reduce((sum, product) => sum + product.quantity, 0);`:  Calculates the total number of items in the cart using the `reduce` function.
            *   `reduce((sum, product) => sum + product.quantity, 0)`: A JavaScript array method that iterates through an array and accumulates a single value.
                *   `(sum, product) => sum + product.quantity`:  The reducer function, which takes the current sum and the current product, and returns the sum plus the product's quantity.
                *   `0`: The initial value of the sum.
        *   `CartProduct key={index} id={currentProduct.id} quantity={currentProduct.quantity}`: Renders `CartProduct` components for each item in the cart, passing `id` and `quantity` as props.
        *   `cart.getTotalCost().toFixed(2)`:  Calls `getTotalCost` from the context to get the cart total and uses `toFixed(2)` to format it to two decimal places.

    *   **Create `CartProduct.js` component in `components` folder:**

        ```javascript
        import React, { useContext } from 'react';
        import { Button } from 'react-bootstrap';
        import { CartContext } from '../CartContext';
        import { getProductData } from '../productsStore';

        function CartProduct(props) {
          const cart = useContext(CartContext);
          const id = props.id;
          const quantity = props.quantity;
          const productData = getProductData(id);

          return (
            <>
              <h3>{productData.title}</h3>
              <p>Quantity: {quantity}</p>
              <p>Total: ${(quantity * productData.price).toFixed(2)}</p>
              <Button size="sm" variant="danger" onClick={() => cart.deleteFromCart(id)}>Remove</Button>
              <hr></hr>
            </>
          )
        }

        export default CartProduct;
        ```

        *   `getProductData(id)`:  Uses the imported `getProductData` function to retrieve product details based on the `id` prop.
        *   Displays product `title`, `quantity`, and total price.
        *   `<Button size="sm" variant="danger" onClick={() => cart.deleteFromCart(id)}>Remove</Button>`: A button to remove the entire product item from the cart using `cart.deleteFromCart(id)`.

## Integrating Stripe for Payment Processing

To enable secure online payments, we will integrate Stripe into our application. This involves setting up a Stripe account, creating products in Stripe, and implementing a basic back-end server to handle Stripe API calls.

### Setting up Stripe Account and Products

1.  **Create a Stripe account at [stripe.com](https://stripe.com).**
2.  **Obtain your Stripe Secret Key:**
    *   Log in to your Stripe dashboard.
    *   Navigate to the "Developers" section, then "API keys".
    *   Reveal and copy your "Secret key". **Keep this key secure and do not expose it in your front-end code.**
3.  **Create Products in Stripe:**
    *   Navigate to the "Products" section in your Stripe dashboard.
    *   Click "+ Add product".
    *   Create products corresponding to your e-commerce items (e.g., Coffee, Sunglasses, Camera).
    *   Set the price and other product details.
    *   **Crucially, copy the "Price ID" for each product.** These Price IDs will be used in your application to reference the Stripe products.

### Creating a Basic Express.js Back-End

We need a back-end server to securely handle communication with the Stripe API. We will use Express.js for this purpose.

1.  **Create a new folder outside your React project directory (e.g., `stripe-backend`).**
2.  **Navigate into the back-end folder in your terminal.**
3.  **Initialize a Node.js project:**

    ```bash
    npm init -y
    ```

4.  **Install required npm packages:**

    ```bash
    npm install express cors stripe
    ```

    *   `express`:  A minimal and flexible Node.js web application framework.
    *   `cors`:  A middleware for Express.js to enable Cross-Origin Resource Sharing (CORS), allowing requests from different origins (like your React front-end).
    *   `stripe`:  The official Stripe Node.js library for interacting with the Stripe API.

5.  **Create `server.js` in your back-end folder and implement the Express server:**

    ```javascript
    const express = require('express');
    const cors = require('cors');
    const stripe = require('stripe')('YOUR_STRIPE_SECRET_KEY'); // Replace with your actual secret key

    const app = express();
    app.use(cors()); // Enable CORS for all origins
    app.use(express.json()); // Parse JSON request bodies

    app.post('/checkout', async (req, res) => {
      const items = req.body.items; // Get items from request body
      let lineItems = [];
      items.forEach((item) => {
        lineItems.push(
          {
            price: item.id, // Use product Price ID from Stripe
            quantity: item.quantity
          }
        )
      });

      const session = await stripe.checkout.sessions.create({
        line_items: lineItems,
        mode: 'payment',
        success_url: 'http://localhost:3000/success', // Redirect URL on success
        cancel_url: 'http://localhost:3000/cancel',   // Redirect URL on cancellation
      });

      res.send(JSON.stringify({ url: session.url })); // Send session URL back to front-end
    });

    app.listen(4000, () => console.log("Listening on port 4000!")); // Start the server
    ```

    *   `require('stripe')('YOUR_STRIPE_SECRET_KEY')`:  Initializes the Stripe library with your secret key. **Replace `'YOUR_STRIPE_SECRET_KEY'` with your actual Stripe Secret Key.**
    *   `app.use(cors())`: Enables CORS to allow requests from your React front-end (typically running on `http://localhost:3000`).
    *   `app.use(express.json())`:  Middleware to parse incoming requests with JSON payloads.
    *   `app.post('/checkout', async (req, res) => { ... })`: Defines a POST route at `/checkout` to handle checkout requests.
        *   `const items = req.body.items`:  Extracts the `items` array from the request body, which will contain product IDs and quantities from the front-end.
        *   `let lineItems = [];`: Initializes an empty array `lineItems` to format the items for Stripe's checkout session.
        *   `items.forEach((item) => { ... })`:  Iterates over the `items` array and transforms each item into a format Stripe expects (`price` and `quantity`). **Crucially, it uses `item.id` as the `price`, assuming `item.id` in your front-end data now holds the Stripe Price ID.**
        *   `stripe.checkout.sessions.create({ ... })`:  Uses the Stripe API to create a checkout session.
            *   `line_items: lineItems`:  Passes the formatted `lineItems` array to the session.
            *   `mode: 'payment'`:  Specifies the session mode as "payment" for one-time payments.
            *   `success_url: 'http://localhost:3000/success'`, `cancel_url: 'http://localhost:3000/cancel'`:  Sets the URLs to redirect users to after successful payment or cancellation, respectively. These should match your React application's routes.
        *   `res.send(JSON.stringify({ url: session.url }))`: Sends the session URL generated by Stripe back to the front-end as a JSON response.
    *   `app.listen(4000, () => console.log("Listening on port 4000!"))`: Starts the Express server on port 4000.

6.  **Run the back-end server:**

    ```bash
    node server.js
    ```

    You should see "Listening on port 4000!" in your terminal, indicating the server is running.

### Connecting Front-End to Back-End for Checkout

Finally, we need to connect the "Purchase items!" button in the `NavbarComponent` to our back-end server to initiate the Stripe checkout process.

1.  **Update `productsStore.js` to use Stripe Price IDs for product IDs:**

    Replace the placeholder IDs in `productsArray` with the actual Stripe Price IDs you copied earlier. For example:

    ```javascript
    const productsArray = [
      { id: "price_1N...", title: "Coffee", price: 4.99 }, // Replace "price_1N..." with your Coffee Price ID
      { id: "price_1O...", title: "Sunglasses", price: 9.99 }, // Replace "price_1O..." with your Sunglasses Price ID
      { id: "price_1P...", title: "Camera", price: 39.99 },   // Replace "price_1P..." with your Camera Price ID
    ];
    ```

    This ensures that when you send product IDs from your front-end to the back-end, they directly correspond to the Stripe Price IDs needed for checkout.

2.  **Modify the "Purchase items!" button in `NavbarComponent.js` to trigger a checkout function:**

    *   Add an `onClick` handler to the "Purchase items!" button that calls a new function, `checkout`.
    *   Implement the `checkout` function within `NavbarComponent.js` to make a fetch request to your back-end `/checkout` route.

    ```javascript
    import React, { useState, useContext } from 'react';
    import { Button, Container, Navbar, Modal } from 'react-bootstrap';
    import { CartContext } from '../CartContext';
    import CartProduct from './CartProduct';

    function NavbarComponent() {
      // ... (existing state and context access) ...

      const checkout = async () => { // Asynchronous checkout function
        await fetch('http://localhost:4000/checkout', { // Fetch request to back-end
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ items: cart.items }) // Send cart items in request body
        }).then((response) => {
          return response.json(); // Parse JSON response
        }).then((response) => {
          if(response.url) {
            window.location.assign(response.url); // Redirect to Stripe checkout URL
          }
        });
      }

      return (
        // ... (Navbar and Modal structure) ...
        <Button variant="success" onClick={checkout}>Purchase items!</Button> {/* Checkout button with onClick handler */}
        // ... (Modal closing tags) ...
      );
    }

    export default NavbarComponent;
    ```

    *   `const checkout = async () => { ... }`:  Defines an asynchronous function `checkout` to handle the checkout process.
    *   `await fetch('http://localhost:4000/checkout', { ... })`:  Makes an asynchronous `fetch` request to your back-end server's `/checkout` route.
        *   `method: 'POST'`: Specifies the request method as POST.
        *   `headers: { 'Content-Type': 'application/json' }`: Sets the `Content-Type` header to `application/json`, indicating that the request body will be in JSON format.
        *   `body: JSON.stringify({ items: cart.items })`:  Stringifies the `cart.items` array (containing product IDs and quantities) and sends it in the request body.
    *   `.then((response) => { return response.json(); })`:  Parses the JSON response from the back-end server.
    *   `.then((response) => { if(response.url) { window.location.assign(response.url); } })`:  If the response contains a `url` property (which should be the Stripe checkout URL), it redirects the user to that URL using `window.location.assign(response.url)`.

3.  **Test the complete application:**
    *   Ensure both your React front-end (using `npm start` in the `store` directory) and Express back-end (using `node server.js` in the `stripe-backend` directory) are running.
    *   Add items to your cart in the React application.
    *   Click "Purchase items!" in the cart modal.
    *   You should be redirected to Stripe's secure checkout page.
    *   Use Stripe's test credit card details to complete a test payment.
    *   After successful payment, you should be redirected to the `/success` route in your React application.
    *   Check your Stripe dashboard to verify the test payment was processed.

## Conclusion

Congratulations! You have successfully built a React and Stripe shopping cart application. This project demonstrates key concepts in front-end and back-end web development, including component-based UI design, state management with React Context, routing, API integration, and secure payment processing with Stripe. This foundation can be expanded upon to create more complex and feature-rich e-commerce platforms.
