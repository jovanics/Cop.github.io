
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Jovanics - EDU.COM</title>
<style>
body {
font-family: Arial, sans-serif;
margin: 0;
padding: 40px 20px;
background-color: #1a1a1a;
color: #111827;
}
.notes-section {
text-align: center;
max-width: 800px;
margin: auto;
}
.notes-section input[type="text"] {
width: 80%;
max-width: 500px;
padding: 12px 16px;
font-size: 1rem;
border: 1px solid #d1d5db;
border-radius: 8px;
margin-bottom: 10px;
outline: none;
}
.notes-section input[type="text"]:focus {
border-color: #2563eb;
}
#clearSearch {
padding: 10px 20px;
margin-left: 10px;
font-size: 1rem;
border-radius: 8px;
background-color: #e0e7ff;
border: none;
cursor: pointer;
transition: background 0.3s;
}
#clearSearch:hover {
background-color: #c7d2fe;
}
.notesContainer {
display: flex;
flex-wrap: wrap;
gap: 20px;
justify-content: center;
margin-top: 20px;
}
.note-card {
width: 100%;
max-width: 500px;
background-color: #ffffff;
padding: 30px 20px;
text-align: left;
border-radius: 12px;
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
transition: transform 0.3s ease;
}
.note-card:hover {
transform: translateY(-5px);
}
.note-card a {
display: inline-block;
margin-top: 10px;
background-color: #1d4ed8;
color: white;
padding: 8px 12px;
text-decoration: none;
border-radius: 6px;
}
.note-card a:hover {
background-color: #2563eb;
}
footer {
background-color: #1d4ed8;
color: white;
padding: 20px;
text-align: center;
border-radius: 12px;
margin-top: 50px;
}
/* Upgraded Navbar */
.navbar {
position: sticky;
top: 0;
background-color: #1d4ed8;
color: white;
z-index: 1000;
box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
.nav-container {
max-width: 1100px;
margin: 0 auto;
padding: 10px 20px;
display: flex;
justify-content: space-between;
align-items: center;
}
.logo {
font-size: 1.5rem;
font-weight: bold;
color: white;
}
nav {
display: flex;
align-items: center;
gap: 20px;
}
nav a, nav select {
color: white;
text-decoration: none;
font-weight: 500;
background: transparent;
border: none;
padding: 8px 12px;
border-radius: 6px;
cursor: pointer;
font-size: 1rem;
}
nav a:hover, nav select:hover {
background-color: #2563eb;
}
.hamburger {
display: none;
font-size: 1.8rem;
cursor: pointer;
}
/* Responsive styles */
@media (max-width: 768px) {
.hamburger {
display: block;
}
nav {
display: none;
position: absolute;
top: 60px;
right: 20px;
background-color: #1d4ed8;
flex-direction: column;
padding: 10px;
border-radius: 10px;
box-shadow: 0 8px 16px rgba(0,0,0,0.15);
}
nav.show {
display: flex;
}
nav a, nav select {
width: 100%;
text-align: left;
}
}
.note-card {
padding: 40px 20px;
text-align: center;
border-radius: 12px;
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
margin-bottom: 30px;
}
</head>
</style>
<body>
<header class="navbar">
<div class="nav-container">
<div class="logo">
EDU.COM
</div>
<nav id="nav-links">
<a href="gag.html">Home</a>
<a href="search.html">Search</a>
</nav>
<div class="hamburger" onclick="toggleMenu()">
☰
</div>
</div>
</header>
<body>
<div class="notes-section">
<h2>Smart Subject Notes</h2>
<input type="text" id="noteSearch" placeholder="Type a subject and press Enter..." />
<button id="clearSearch">Clear</button>

<div class="notesContainer" id="notesContainer">
<div class="note-card" data-subject="math">
<h3>Math</h3>
<p>Learn basic arithmetic, geometry, and problem-solving techniques. Includes worksheets for practice.
</p>
<a href="https://www.education.com">Go to Notes</a>
</div>

<div class="note-card" data-subject="biology">
<h3>Biology</h3>
<p>
Explore cells, plants, animals, and human anatomy with clear diagrams and activities.
</p>
<a href="https://www.biologyonline.com">Go to Notes</a>
</div>

<div class="note-card" data-subject="physics">
<h3>Physics</h3>
<p>
Understand motion, forces, energy, and simple experiments to reinforce concepts.
</p>
<a href="https://www.physicsworld.com">Go to Notes</a>
</div>

<div class="note-card" data-subject="chemistry">
<h3>Chemistry</h3>
<p>
Cover basic concepts like elements, compounds, reactions, and lab safety.
</p>
<a href="https://www.wikipedia.com/wiki/Chemistry" target="_blank">Go to Notes</a>

<!-- Dynamic cards go here -->
</div>
</div>

<footer>
&copy; 2025 EDU.COM | Designed by: Jovanics Pro
</footer>
<script>
const noteSearchInput = document.getElementById('noteSearch');
const clearSearchBtn = document.getElementById('clearSearch');
const notesContainer = document.getElementById('notesContainer');
// Clear button
clearSearchBtn.addEventListener('click', () => {
noteSearchInput.value = '';
notesContainer.innerHTML = '';
});
// Enter key: Fetch Wikipedia summary
noteSearchInput.addEventListener('keypress', function (e) {
if (e.key === 'Enter') {
const query = e.target.value.trim();
if (!query) return;
// Show loading
notesContainer.innerHTML = `<p>Searching Jovanics ai for "${query}"...</p>`;
fetch(`https://en.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(query)}`)
.then(res => {
if (!res.ok) throw new Error('Not found');
return res.json();
})
.then(data => {
if (data.title && data.extract && data.content_urls) {
notesContainer.innerHTML = `
<div class="note-card">
<h3>${data.title}</h3>
<p>${data.extract}</p>
<a href="${data.content_urls.desktop.page}" target="_blank">Read more</a>
</div>
`;
} else {
notesContainer.innerHTML = `<p>Jovanics say no. Try a different topic.</p>`;
}
})
.catch(err => {
console.error(err);
notesContainer.innerHTML = `<p>Topic not found. Try something else.</p>`;
});
}
});
function toggleMenu() {
document.getElementById('nav-links').classList.toggle('show');
}
</script>
</body>
</html>
