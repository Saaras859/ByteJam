<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            background-color: #1e1e1e; /* Dark background color */
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        h2 {
            text-align: center;
            color: #FF69B4; /* Pink */
        }
        form {
            background-color: #2e2e2e; /* Darker gray */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); /* Darker shadow */
            max-width: 300px;
            width: 100%;
            margin-right: auto; /* Center the form to the left */
            margin-left: 20px; /* Add some space to the left */
        }
        form div {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            color: #FF69B4; /* Pink */
        }
        input[type="text"],
        input[type="password"] {
            width: calc(100% - 20px);
            padding: 10px;
            border: 1px solid #FF69B4; /* Pink */
            border-radius: 5px;
            outline: none;
            background-color: #333; /* Dark input background */
            color: #FFF; /* White text */
        }
        button[type="submit"] {
            background-color: #FF69B4; /* Pink */
            color: #FFF;
            border: none;
            padding: 10px;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button[type="submit"]:hover {
            background-color: #E75480; /* Lighter pink */
        }
    </style>
</head>
<body>
    <form id="loginForm">
        <div>
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required>
        </div>
        <div>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
        </div>
        <button type="submit">Login</button>
    </form>
    <script> 
        document.getElementById("loginForm").addEventListener("submit", function(event) {
            event.preventDefault();   
            var username = document.getElementById("username").value;
            var password = document.getElementById("password").value;
            // Create JSON object with username and password
            var data = {
                "username": username,
                "password": password
            };
            const apiLink = "http://127.0.0.1:5000/login";
            fetch(apiLink, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(data)
            })
            .then(response => response.text())
            .then(data => {
                const jwtToken = data
                console.log(data)
                localStorage.setItem('jwtToken', jwtToken);

                window.location.href="./game"
            })
            .catch(error => {
                console.error("Error:", error);
            });
        });
    </script>
</body>
</html>
