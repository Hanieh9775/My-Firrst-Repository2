import requests
from flask import Flask, render_template_string

app = Flask(__name__)

HTML_TEMPLATE = """
<!DOCTYPE html>
<html lang="en">

    <meta charset="UTF-8">
    <title>Random Joke App</title>
</head>
<body>
    <h1>Random Joke Generator</h1>
    {% if joke %}
        <p><strong>{{ joke }}</strong></p>
    {% endif %}
    <form method="get">
        <button type="submit">Get Another Joke</button>
    
</body>
</html>
"""
<head>
@app.route("/", methods=["GET"])
def home():
    try:
        response = requests.get("https://official-joke-api.appspot.com/random_joke", timeout=5)
        if response.status_code == 200:
            data = response.json()
            joke = f"{data['setup']} - {data['punchline']}"
        else:
            joke = "Could not fetch a joke at the moment."
    except Exception:
        joke = "Error connecting to the joke service."
    return render_template_string(HTML_TEMPLATE, joke=joke)

if __name__ == "__main__":
    app.run(debug=True)
