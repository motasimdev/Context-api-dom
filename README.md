# Context-api-dom
# make a count update with context api

# Step-1
Create a "context" folder in "src". make a file named "CartContext.jsx"/etc.

# Step-2 
paste this code -
import { createContext, useState, useContext } from "react";

// ১. বয়ামটা তৈরি করলাম
const CartContext = createContext();

// ২. এই প্রোভাইডারটাই পুরো অ্যাপে ডাটা সাপ্লাই দেবে
export const CartProvider = ({ children }) => {
  const [cartCount, setCartCount] = useState(0);

  // কার্ট সংখ্যা ১ বাড়ানোর ফাংশন
  const addToCart = () => {
    setCartCount((prev) => prev + 1);
  };

  return (
    // value এর ভেতর আমরা যে ডাটা বা ফাংশন দেব, সেটা সবাই পাবে
    <CartContext.Provider value={{ cartCount, addToCart }}>
      {children}
    </CartContext.Provider>
  );
};

// ৩. একটা কাস্টম হুক বানিয়ে রাখলাম যাতে সহজে অন্য ফাইলে ব্যবহার করা যায়
export const useCart = () => useContext(CartContext);

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
  
