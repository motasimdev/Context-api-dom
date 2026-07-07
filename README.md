# Context-api-dom
# make a count update with context api

# Step-1
Create a "context" folder in "src". make a file named "CartContext.jsx"/etc.

# Step-2 
paste this code -

```
import { createContext, useState } from "react";

const CartContext = createContext();

export const CartProvider = ({ children }) => {

  const [cartItems, setCartItems] = useState([]);

  const addToCart = (product) => {
  
    const existingProduct = cartItems.find((item) => item.id === product.id);
    
    console.log(cartItems);
    
    if (!existingProduct) {
      setCartItems((prevItems) => [
        ...prevItems,
        {
          ...product,
          quantity: 1,
        },
      ]);
    } else {
      setCartItems((prevItems) =>
        prevItems.map((item) => {
          if (item.id === product.id) {
            return {
              ...item,
              quantity: item.quantity + 1,
            };
          }
          return item;
        }),
      );
     }
    };
    return (
  
    <CartContext.Provider value={{ cartItems, addToCart }}>
      {children}
    </CartContext.Provider>);
   };
   export default CartContext;
```

# step-3 
go to main jsx. import "CartProvider" and wrap it like-

```
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import { RouterProvider } from "react-router/dom";
import Routes from "./routes/Routes";
import { CartProvider } from "./context/CartContext";

createRoot(document.getElementById("root")).render(
  <CartProvider>
    <StrictMode>
      <RouterProvider router={Routes} />
    </StrictMode>
  </CartProvider>
);
```
  # step-4 
  go to the page where you want to change value count then import hook and use it like this-

```
import { useContext } from "react";
import CartContext from "@/context/CartContext";

const Header = () => {
    const { cartItems } = useContext(CartContext);

  return (
    <div className="">
      <ShoppingBag className="" />
      <div className="rounded-full">
        {/* সরাসরি ভ্যালু বসে গেল */}
        {cartItems.length}
      </div>
    </div>
  );
};
export default Header;
```

# step-5 
then go to the page where you want to click then import hook and use it like this-

```
import { useContext, useEffect, useState } from "react";

import CartContext from "@/context/CartContext";

const Home = () => {


  const { addToCart } = useContext(CartContext);

  return (
  
    <button
      className="py-1 px-4 mt-2 bg-purple-900 text-purple-300 rounded-xl text-sm"
      onClick={() => addToCart(item) // 'item' hbe map() er vitore jei name disi shetar!
    >
      Add to cart
    </button>
  );
};

export default Home;
  ```
