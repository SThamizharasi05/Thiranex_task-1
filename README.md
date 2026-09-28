<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Strength Analyzer</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #eef2f7;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            background: white;
            width: 400px;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }

        h1 {
            text-align: center;
            color: #222;
        }

        input {
            width: 100%;
            padding: 12px;
            box-sizing: border-box;
            border: 1px solid #aaa;
            border-radius: 6px;
            font-size: 16px;
            margin-top: 15px;
        }

        .strength {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }

        .bar {
            height: 10px;
            background: #ddd;
            border-radius: 5px;
            margin-top: 10px;
            overflow: hidden;
        }

        #progress {
            height: 100%;
            width: 0%;
            transition: 0.3s;
        }

        ul {
            padding-left: 20px;
        }

        li {
            margin: 8px 0;
        }

        .suggestion {
            margin-top: 15px;
            background: #f1f5f9;
            padding: 12px;
            border-radius: 6px;
        }
    </style>
</head>

<body>

<div class="container">

    <h1>Password Strength Analyzer</h1>

    <input
        type="password"
        id="password"
        placeholder="Enter your password"
        oninput="checkPassword()"
    >

    <div class="strength">
        Strength: <span id="result">None</span>
    </div>

    <div class="bar">
        <div id="progress"></div>
    </div>

    <h3>Password Requirements</h3>

    <ul>
        <li id="length">❌ At least 8 characters</li>
        <li id="upper">❌ Contains uppercase letter</li>
        <li id="lower">❌ Contains lowercase letter</li>
        <li id="number">❌ Contains number</li>
        <li id="special">❌ Contains special character</li>
        <li id="unique">❌ Avoid repeated characters</li>
    </ul>

    <div class="suggestion" id="suggestion">
        Enter a password to get suggestions.
    </div>

</div>

<script>

function checkPassword() {

    let password = document.getElementById("password").value;

    let score = 0;
    let suggestions = [];

    // Length
    if (password.length >= 8) {
        score++;
        document.getElementById("length").innerHTML =
            "✅ At least 8 characters";
    } else {
        document.getElementById("length").innerHTML =
            "❌ At least 8 characters";

        suggestions.push("Use at least 8 characters.");
    }

    // Uppercase
    if (/[A-Z]/.test(password)) {
        score++;
        document.getElementById("upper").innerHTML =
            "✅ Contains uppercase letter";
    } else {
        document.getElementById("upper").innerHTML =
            "❌ Contains uppercase letter";

        suggestions.push("Add an uppercase letter.");
    }

    // Lowercase
    if (/[a-z]/.test(password)) {
        score++;
        document.getElementById("lower").innerHTML =
            "✅ Contains lowercase letter";
    } else {
        document.getElementById("lower").innerHTML =
            "❌ Contains lowercase letter";

        suggestions.push("Add a lowercase letter.");
    }

    // Number
    if (/[0-9]/.test(password)) {
        score++;
        document.getElementById("number").innerHTML =
            "✅ Contains number";
    } else {
        document.getElementById("number").innerHTML =
            "❌ Contains number";

        suggestions.push("Add a number.");
    }

    // Special character
    if (/[^A-Za-z0-9]/.test(password)) {
        score++;
        document.getElementById("special").innerHTML =
            "✅ Contains special character";
    } else {
        document.getElementById("special").innerHTML =
            "❌ Contains special character";

        suggestions.push("Add a special character like @, #, $, or !.");
    }

    // Repeated characters
    if (password.length > 0 && !/(.)\1\1/.test(password)) {
        score++;
        document.getElementById("unique").innerHTML =
            "✅ Avoid repeated characters";
    } else {
        document.getElementById("unique").innerHTML =
            "❌ Avoid repeated characters";

        suggestions.push("Avoid repeating the same character three times.");
    }

    // Result
    let result = document.getElementById("result");
    let progress = document.getElementById("progress");

    if (password.length === 0) {

        result.innerHTML = "None";
        progress.style.width = "0%";

    } else if (score <= 2) {

        result.innerHTML = "Weak";
        progress.style.width = "30%";
        progress.style.background = "red";

    } else if (score <= 4) {

        result.innerHTML = "Medium";
        progress.style.width = "60%";
        progress.style.background = "orange";

    } else {

        result.innerHTML = "Strong";
        progress.style.width = "100%";
        progress.style.background = "green";
    }

    // Suggestions
    if (suggestions.length === 0) {

        document.getElementById("suggestion").innerHTML =
            "✅ Your password satisfies all basic security requirements!";

    } else {

        document.getElementById("suggestion").innerHTML =
            "<b>Suggestions:</b><br>• " +
            suggestions.join("<br>• ");
    }
}

</script>

</body>
</html># Thiranex_task-1
