STEP 1: Install required packages
Inside your React project:
npm install axios bootstrap

STEP 2: Import Bootstrap (important)
In src/main.jsx (or index.js):
import 'bootstrap/dist/css/bootstrap.min.css';

STEP 3: Create Products.jsx
Create a file:
src/Products.jsx

import { useEffect, useState } from "react";
import axios from "axios";

function Products() {
  const [products, setProducts] = useState([]);
  const [currentPage, setCurrentPage] = useState(1);

  const productsPerPage = 9;

  // Fetch products using Axios
  useEffect(() => {
    axios.get("https://fakestoreapi.com/products")
      .then(res => setProducts(res.data))
      .catch(err => console.error(err));
  }, []);

  // Pagination logic
  const lastIndex = currentPage * productsPerPage;
  const firstIndex = lastIndex - productsPerPage;
  const currentProducts = products.slice(firstIndex, lastIndex);

  const totalPages = Math.ceil(products.length / productsPerPage);

  return (
    <div className="container my-4">
      <div className="row">
        {currentProducts.map(product => (
          <div className="col-md-4 mb-4" key={product.id}>
            <div className="card h-100 shadow-sm">
              <img
                src={product.image}
                className="card-img-top p-3"
                style={{ height: "250px", objectFit: "contain" }}
                alt={product.title}
              />

              <div className="card-body d-flex flex-column">
                <h6 className="card-title">
                  {product.title.substring(0, 40)}...
                </h6>

                <p className="text-success fw-bold">
                  ₹ {product.price}
                </p>

                <button className="btn btn-primary mt-auto">
                  Add to Cart
                </button>
              </div>
            </div>
          </div>
        ))}
      </div>

      {/* Pagination */}
      <div className="d-flex justify-content-center">
        <nav>
          <ul className="pagination">
            {[...Array(totalPages)].map((_, index) => (
              <li
                key={index}
                className={`page-item ${currentPage === index + 1 ? "active" : ""}`}
              >
                <button
                  className="page-link"
                  onClick={() => setCurrentPage(index + 1)}
                >
                  {index + 1}
                </button>
              </li>
            ))}
          </ul>
        </nav>
      </div>
    </div>
  );
}

export default Products;




STEP 4: Create Header & Footer
Header.jsx
function Header() {
  return (
    <nav className="navbar navbar-dark bg-dark">
      <div className="container">
        <span className="navbar-brand">
          🛒 Product Store
        </span>
      </div>
    </nav>
  );
}

export default Header;
Footer.jsx
function Footer() {
  return (
    <footer className="bg-dark text-white text-center p-3 mt-4">
      © 2026 Product Store | Built with React & Axios
    </footer>
  );
}

export default Footer;






STEP 5: Update App.jsx
import Header from "./Header";
import Footer from "./Footer";
import Products from "./Products";

function App() {
  return (
    <>
      <Header />
      <Products />
      <Footer />
    </>
  );
}

export default App;




STEP 6: Run the app
npm run dev
Open browser 👉
http://localhost:5173








Verify
Header
9 product cards per page
Product images
Price & button
Pagination
Footer
Bootstrap responsive layout
This looks very close to a real e-commerce UI 

Topics covered.

Axios → fetch data
useEffect → call API once
useState → store products
Bootstrap → styling
map() → display cards
slice() → pagination


