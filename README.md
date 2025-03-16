<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, initial-scale=1, maximum-scale=1">
    <title>Solar Power Mart - Your One Stop Solar Solution</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css">
    <link rel="stylesheet" href="styles.css">
    <script src="https://checkout.razorpay.com/v1/checkout.js"></script>
    <script>
        function validateForm(event) {
            event.preventDefault();
            let name = document.getElementById('name').value;
            let email = document.getElementById('email').value;
            let message = document.getElementById('message').value;
            let emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            
            if (name.trim() === "") {
                alert("Please enter your name.");
                return false;
            }
            if (!emailPattern.test(email)) {
                alert("Please enter a valid email address.");
                return false;
            }
            if (message.trim() === "") {
                alert("Please enter your message.");
                return false;
            }
            
            alert("Form submitted successfully!");
            document.getElementById('contactForm').submit();
        }

        function shopNow(product) {
            alert("You clicked on " + product + ". Redirecting to product page...");
            window.location.href = "shop.html?product=" + encodeURIComponent(product);
        }
        
        function initiatePayment() {
            var options = {
                "key": "your_razorpay_key", 
                "amount": "10000", 
                "currency": "INR",
                "name": "Solar Power Mart",
                "description": "Payment for Solar Products",
                "handler": function (response) {
                    alert("Payment Successful! Payment ID: " + response.razorpay_payment_id);
                },
                "theme": {
                    "color": "#F37254"
                }
            };
            var rzp1 = new Razorpay(options);
            rzp1.open();
        }
    </script>
</head>
<body>
    <header>
        <h1>Solar Power Mart</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#products">Products</a></li>
                <li><a href="#about">About Us</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <section id="home">
        <h2>Welcome to Solar Power Mart</h2>
        <p>Providing high-quality solar panels, inverters, and batteries at the best prices.</p>
        <a href="#products" class="btn">Explore Products</a>
    </section>

    <section id="products">
        <h2>Our Products</h2>
        <div class="product-list">
            <div class="product">
                <img src="solar-panel.jpg" alt="Solar Panel">
                <h3>Solar Panels</h3>
                <p>High-efficiency Mono & Polycrystalline panels.</p>
                <button onclick="shopNow('Solar Panels')">Shop Now</button>
                <button onclick="initiatePayment()">Buy Now</button>
            </div>
            <div class="product">
                <img src="solar-inverter.jpg" alt="Solar Inverter">
                <h3>Solar Inverters</h3>
                <p>Reliable On-grid and Off-grid inverters.</p>
                <button onclick="shopNow('Solar Inverters')">Shop Now</button>
                <button onclick="initiatePayment()">Buy Now</button>
            </div>
            <div class="product">
                <img src="solar-battery.jpg" alt="Solar Battery">
                <h3>Solar Batteries</h3>
                <p>Long-lasting Lithium-ion and Lead Acid batteries.</p>
                <button onclick="shopNow('Solar Batteries')">Shop Now</button>
                <button onclick="initiatePayment()">Buy Now</button>
            </div>
        </div>
    </section>

    <section id="reviews">
        <h2>Customer Reviews</h2>
        <p>"Great quality solar panels! Highly recommend." - Rahul S.</p>
        <p>"Fast delivery and great support!" - Priya K.</p>
    </section>

    <section id="solar-calculator">
        <h2>Solar Savings Calculator</h2>
        <p>Enter your monthly electricity bill to see how much you can save with solar.</p>
        <input type="number" id="billAmount" placeholder="Enter bill amount in INR">
        <button onclick="calculateSavings()">Calculate Savings</button>
        <p id="savingsResult"></p>
    </section>
    
    <script>
        function calculateSavings() {
            let billAmount = document.getElementById('billAmount').value;
            if (billAmount > 0) {
                let savings = billAmount * 0.7;
                document.getElementById('savingsResult').innerText = "Estimated Monthly Savings: ₹" + savings.toFixed(2);
            } else {
                alert("Please enter a valid bill amount.");
            }
        }
    </script>
    
    <section id="contact">
        <h2>Contact Us</h2>
        <form id="contactForm" onsubmit="return validateForm(event)">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>
            
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            
            <label for="message">Message:</label>
            <textarea id="message" name="message" required></textarea>
            
            <button type="submit">Send Inquiry</button>
        </form>
    </section>

    <footer>
        <p>&copy; 2025 Solar Power Mart. All Rights Reserved.</p>
    </footer>
</body>
</html>
