<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Digital Plug</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #0f0f0f, #1a1a1a);
      color: #f4f4f4;
    }
    header {
      background: linear-gradient(90deg, #111111, #1f1f1f);
      padding: 2rem;
      text-align: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.5);
    }
    h1 {
      font-size: 2.8rem;
      margin-bottom: 0.5rem;
    }
    h2 {
      font-size: 1.5rem;
      font-weight: 400;
      color: #cccccc;
    }
    .products {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
      padding: 3rem 2rem;
    }
    .card {
      background: linear-gradient(145deg, #1a1a1a, #121212);
      border-radius: 16px;
      padding: 2rem;
      box-shadow: 0 10px 25px rgba(0,0,0,0.4);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
    }
    .card:hover {
      transform: scale(1.05);
      box-shadow: 0 15px 30px rgba(0,255,174,0.4);
    }
    .card h3 {
      margin-top: 0;
      color: #00ffae;
    }
    .card p {
      color: #cccccc;
    }
    .price {
      font-weight: 600;
      color: #00ffae;
      margin: 0.5rem 0;
    }
    .button {
      background-color: #00ffae;
      color: #0f0f0f;
      padding: 0.7rem 1.5rem;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      font-weight: 600;
      text-decoration: none;
      display: inline-block;
      margin-top: 1rem;
      transition: background-color 0.3s;
    }
    .button:hover {
      background-color: #00e2a0;
    }
    form {
      background: linear-gradient(145deg, #1a1a1a, #121212);
      max-width: 500px;
      margin: 2rem auto;
      padding: 2.5rem;
      border-radius: 16px;
      box-shadow: 0 0 20px rgba(0,0,0,0.5);
      display: none;
    }
    form.active {
      display: block;
    }
    form label {
      display: block;
      margin-top: 1rem;
      margin-bottom: 0.5rem;
    }
    form input,
    form textarea,
    form select {
      width: 100%;
      padding: 0.8rem;
      border-radius: 10px;
      border: none;
      background-color: #2a2a2a;
      color: #f4f4f4;
      margin-bottom: 1rem;
    }
    form button {
      background-color: #00ffae;
      color: #0f0f0f;
      padding: 0.8rem 1.5rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-weight: 600;
      transition: background-color 0.3s;
    }
    form button:hover {
      background-color: #00e2a0;
    }
    footer {
      text-align: center;
      padding: 2rem;
      background-color: #1f1f1f;
      color: #888;
    }
    #confirmation {
      max-width: 500px;
      margin: 2rem auto;
      padding: 2rem;
      background-color: #2a2a2a;
      border-radius: 16px;
      text-align: center;
      display: none;
      box-shadow: 0 0 20px rgba(0,0,0,0.5);
    }
    #confirmation h3 {
      color: #00ffae;
    }
    .terms {
      font-size: 0.8rem;
      color: #aaa;
      max-width: 800px;
      margin: 2rem auto;
      padding: 1rem;
      line-height: 1.5;
    }
    .note {
      text-align:center; 
      color:#aaa; 
      font-size:0.85rem;
      margin-top: 1rem;
    }
  </style>
  <script>
    function showPaymentForm(product) {
      const form = document.getElementById("form");
      const productSelect = document.querySelector("select[name='product']");
      const customOptionsContainer = document.getElementById("custom-options");
      const confirmation = document.getElementById("confirmation");

      confirmation.style.display = "none";
      form.classList.add("active");
      form.scrollIntoView({ behavior: "smooth" });

      productSelect.value = product;

      let customFields = '';
      if (product === "monthly") {
        customFields += '<label>Meal Type</label><select name="meal_type"><option value="regular">Regular</option><option value="vegan">Vegan</option><option value="keto">Keto</option></select>';
      } else if (product === "yearly") {
        customFields += '<label>Meal Type</label><select name="meal_type"><option value="weight_loss">Weight Loss</option><option value="muscle_gain">Muscle Gain</option><option value="maintenance">Maintenance</option></select>';
      }

      customOptionsContainer.innerHTML = customFields;
    }

    function redirectToPayment(event) {
      event.preventDefault();
      const form = document.getElementById("form");
      const confirmation = document.getElementById("confirmation");
      confirmation.style.display = "block";
      form.classList.remove("active");

      setTimeout(() => {
        window.location.href = "https://www.paypal.com/paypalme/BobFreman3";
      }, 3000);
    }

    window.addEventListener('DOMContentLoaded', function () {
      const cards = document.querySelectorAll('.card');
      cards.forEach(card => {
        card.addEventListener('click', () => {
          const productTitle = card.querySelector("h3").textContent;
          const valueMap = {
            "Monthly Subscription": "monthly",
            "Yearly Subscription": "yearly"
          };
          showPaymentForm(valueMap[productTitle]);
        });
      });
    });
  </script>
</head>
<body>
  <header>
    <h1>The Digital Plug</h1>
    <h2>Custom Fitness Meal Plans. Start your 7-day free trial today.</h2>
    <a class="button" href="#form">Start Free Trial</a>
  </header>

  <section class="products">
    <div class="card">
      <h3>Monthly Subscription</h3>
      <p>Monthly plan with weekly updates and meal customization. First 7 days free.</p>
      <div class="price">$9.99/month</div>
    </div>
    <div class="card">
      <h3>Yearly Subscription</h3>
      <p>Yearly plan with exclusive content and meal flexibility. First 7 days free.</p>
      <div class="price">$99.99/year</div>
    </div>
  </section>

  <form id="form" onsubmit="redirectToPayment(event)">
    <h2 style="text-align:center">Payment Details</h2>
    <label for="name">Name</label>
    <input type="text" name="name" required>

    <label for="email">Email</label>
    <input type="email" name="email" required>

    <label for="product">Subscription Plan</label>
    <select name="product" required>
      <option value="monthly">Monthly Subscription</option>
      <option value="yearly">Yearly Subscription</option>
    </select>

    <div id="custom-options"></div>

    <label for="details">Custom Notes or Instructions</label>
    <textarea name="details" rows="5"></textarea>

    <p class="note">
      After you submit, please send your form details to <strong>bobf80614@gmail.com</strong>
    </p>

    <button type="submit">Submit</button>
  </form>

  <div id="confirmation">
    <h3>Thank you for starting your trial!</h3>
    <p>Your subscription has been received. Redirecting to PayPal now...</p>
  </div>

  <div class="terms">
    <h4>Terms and Conditions</h4>
    <p>By subscribing, you agree to be billed on a recurring basis unless you cancel before your next billing cycle. Free trial lasts for 7 days, after which your selected plan will be charged. Plans are non-refundable after the billing date. You must be 18 years or older or have a guardian’s consent to use our service. We reserve the right to modify these terms at any time.</p>
  </div>

  <footer>
    &copy; 2025 The Digital Plug. All rights reserved.
  </footer>
</body>
</html>
