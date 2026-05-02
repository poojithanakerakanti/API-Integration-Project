<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Movie Search App</title>

<style>
body {
    font-family: Arial;
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    text-align: center;
    background: rgba(0,0,0,0.5);
    padding: 20px;
    border-radius: 10px;
    width: 350px;
}

input {
    padding: 10px;
    width: 70%;
    border-radius: 5px;
    border: none;
}

button {
    padding: 10px;
    border: none;
    background: #ffcc00;
    cursor: pointer;
    border-radius: 5px;
}

#result img {
    width: 150px;
    margin-top: 10px;
}

.loading {
    color: yellow;
}

.error {
    color: red;
}
</style>

</head>
<body>

<div class="container">
    <h2>🎬 Movie Search</h2>

    <input type="text" id="movie" placeholder="Enter movie name">
    <button onclick="searchMovie()">Search</button>

    <div id="result"></div>
</div>

<script>
async function searchMovie() {
    let movie = document.getElementById("movie").value;
    let result = document.getElementById("result");

    if(movie === "") {
        result.innerHTML = "<p class='error'>Enter movie name</p>";
        return;
    }

    result.innerHTML = "<p class='loading'>Loading...</p>";

    try {
        // 🔑 FREE API KEY (public demo key)
        let response = await fetch(`https://www.omdbapi.com/?t=${movie}&apikey=trilogy`);
        let data = await response.json();

        if(data.Response === "False") {
            result.innerHTML = "<p class='error'>Movie not found</p>";
            return;
        }

        result.innerHTML = `
            <h3>${data.Title}</h3>
            <img src="${data.Poster}" alt="poster">
            <p>📅 Year: ${data.Year}</p>
            <p>⭐ Rating: ${data.imdbRating}</p>
            <p>🎭 Genre: ${data.Genre}</p>
        `;
    } catch (error) {
        result.innerHTML = "<p class='error'>Error fetching data</p>";
    }
}
</script>

</body>
</html>
