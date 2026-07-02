# Context-api-dom
# make a count update with context api

# Step-1
Create a "context" folder in "src". make a file named "CartContext.jsx"/etc.

# Step-2 
paste this code -

import { createContext, useState } from "react";

const CartContext = createContext();

export const CartProvider = ({ children }) => {

    const [cartItems, setCartItems] = useState([]);
    return (
        <CartContext.Provider value={{ cartItems }}>
            {children}
        </CartContext.Provider>
    );
};

export default CartContext;

# step-3 
go to main jsx. import and wrap it like-

import { CartProvider } from "./context/CartContext";

  <CartProvider>
   <StrictMode>
      <RouterProvider router={Routes} />
   </StrictMode>
  </CartProvider>

  # step-4 
  go to the page where you want to change value count then import hook and use it like this-

  import { useCart } from "../context/CartContext"; // হুকটা ইমপোর্ট করো
import { ShoppingBag } from "lucide-react";

const Header = () => {
  // সরাসরি cartCount নিয়ে আসলাম
  const { cartCount } = useCart();

  return (
    <div className="">
      <ShoppingBag className="" />
      <div className="">
        {/* সরাসরি ভ্যালু বসে গেল */}
        {cartCount}
      </div>
    </div>
  );
};
export default Header;

# step-5 
then go to the page where you want to click then import hook and use it like this-

import { useCart } from "../context/CartContext"; // হুকটা ইমপোর্ট করো

const Home = () => {
  // সরাসরি addToCart ফাংশনটা নিয়ে আসলাম
  const { addToCart } = useCart();

  return (
    // তোমার বাকি ডিজাইনের কোড...
    <button
      className="py-1 px-4 mt-2 bg-purple-900 text-purple-300 rounded-xl text-sm"
      onClick={addToCart} // ক্লিকের সাথে সাথে গ্লোবাল স্টেট চেঞ্জ হবে!
    >
      Add to cart
    </button>
  );
};

export default Home;
  
