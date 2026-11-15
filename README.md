# App.1
App.1, first project to learn how to create application using GitHub
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>My Counter App</title>
  <style>
    body {
      max-width: 500px;
      margin: 3rem auto;
      padding: 0 1rem;
      font-family: system-ui, sans-serif;
      text-align: center;
    }

    button {
      margin: 0.3rem;
      padding: 0.6rem 1rem;
      cursor: pointer;
    }

    #count {
      font-size: 3rem;
      margin: 1rem;
    }

    #test-results {
      margin-top: 1rem;
      text-align: left;
    }
  </style>
</head>
<body>
  <h1>My Counter</h1>
  <p id="count" aria-live="polite">0</p>

  <button id="decrease">− Decrease</button>
  <button id="increase">+ Increase</button>
  <button id="reset">Reset</button>

  <h2>Function checks</h2>
  <button id="run-tests">Run checks</button>
  <ul id="test-results" aria-live="polite"></ul>

  <script>
    let count = 0;

    // This function calculates the next count for an action.
    function calculateCount(currentCount, action) {
      if (action === "increase") return currentCount + 1;
      if (action === "decrease") return currentCount - 1;
      if (action === "reset") return 0;
      return currentCount;
    }

    function updateCount(action) {
      count = calculateCount(count, action);
      document.querySelector("#count").textContent = count;
    }

    document.querySelector("#increase").addEventListener("click", () => {
      updateCount("increase");
    });

    document.querySelector("#decrease").addEventListener("click", () => {
      updateCount("decrease");
    });

    document.querySelector("#reset").addEventListener("click", () => {
      updateCount("reset");
    });

    // These checks test the calculation function without changing the app.
    document.querySelector("#run-tests").addEventListener("click", () => {
      const checks = [
        ["increase: 2 becomes 3", calculateCount(2, "increase") === 3],
        ["decrease: 2 becomes 1", calculateCount(2, "decrease") === 1],
        ["reset: 2 becomes 0", calculateCount(2, "reset") === 0]
      ];

      const results = document.querySelector("#test-results");
      results.replaceChildren();

      for (const [description, passed] of checks) {
        const item = document.createElement("li");
        item.textContent = `${passed ? "PASS" : "FAIL"} — ${description}`;
        results.appendChild(item);
      }
    });
  </script>
</body>
</html>
