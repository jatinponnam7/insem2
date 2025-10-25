import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";
ReactDOM.createRoot(document.getElementById("root")).render(
<BrowserRouter>
<App />
</BrowserRouter>
);
App.jsx
import React from "react";
import { Routes, Route } from "react-router-dom";
import BookList from "./pages/BookList";
import BookDetail from "./components/BookDetail";
const App = () => {
return (
<div style={{ padding: "20px", fontFamily: "Arial" }}>
<h1> Book Explorer</h1>
<Routes>
<Route path="/" element={<BookList />} />
<Route path="/book/:id" element={<BookDetail />} />
</Routes>
</div>
);
};
export default App;
BookCard.jsx
import React from "react";
import { Link } from "react-router-dom";
const BookCard = ({ book }) => {
return (
<div
style={{
border: "1px solid #ccc",
padding: "15px",
borderRadius: "8px",
width: "200px",
}}
>
<h3>{book.title}</h3>
<p>By {book.author}</p>
<Link to={`/book/${book.id}`} style={{ color: "blue" }}>
View Details →
</Link>
</div>
);
};
export default BookCard;
BookDetail.jsx
import React from "react";
import { useParams, Link } from "react-router-dom";
import booksData from "../data/booksData";
const BookDetail = () => {
const { id } = useParams();
const book = booksData.find((b) => b.id === parseInt(id));
if (!book) return <p>Book not found!</p>;
return (
<div>
<h2>{book.title}</h2>
<h4>By {book.author}</h4>
<p>{book.description}</p>
<p> Rating: {book.rating}</p>
<Link to="/">← Back to List</Link>
</div>
);
};
export default BookDetail;
BookList.jsx
import React, { useState, useEffect } from "react";
import BookCard from "../components/BookCard";
import booksData from "../data/booksData";
const BookList = () => {
const [books, setBooks] = useState([]);
// Simulate API Fetch
useEffect(() => {
setTimeout(() => {
setBooks(booksData);
}, 500);
}, []);
return (
<div>
<h2>Available Books</h2>
{books.length === 0 ? (
<p>Loading books...</p>
) : (
<div style={{ display: "flex", gap: "15px", flexWrap: "wrap" }}>
{books.map((book) => (
<BookCard key={book.id} book={book} />
))}
</div>
)}
</div>
);
};
export default BookList;
BooksData.jsx
const booksData = [
{
id: 1,
title: "Full Stack Web Development ",
author: "Stepen Roy",
description: "Full-stack development is a multifaceted discipline within the realm of 
software engineering that encompasses the complete spectrum of designing, building, and 
maintaining software applications.",
rating: 4.8,
},
{
id: 2,
title: "Deep Work",
author: "Cal Newport",
description: "Rules for focused success in a distracted world.",
rating: 4.5,
},
{
id: 3,
title: "The Alchemist",
author: "Paulo Coelho",
description: "A philosophical story about following your dreams.",
rating: 4.7,
},
];
export default booksData;
