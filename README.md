<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Service Buy Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(45deg, #ff758c, #ff7eb3);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }
        .form-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 450px;
            text-align: center;
            opacity: 0;
            transform: translateY(-50px);
            animation: fadeIn 1s ease-in-out forwards;
            max-height: 90vh;
            overflow-y: auto;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }
        h2 { color: #333; }
        .real-label {
            background: #ff4f81;
            color: white;
            padding: 5px 10px;
            display: inline-block;
            border-radius: 5px;
            margin-top: 15px;
            font-size: 14px;
            font-weight: bold;
        }
        label { font-weight: bold; display: block; margin-top: 10px; }
        input, select {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .hidden { display: none; }
        button {
            background: green;
            color: white;
            border: none;
            padding: 10px;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 15px;
            transition: 0.3s;
            font-size: 14px;
            font-weight: bold;
        }
        button:hover { background: #ff3c5e; }
        .loading {
            display: none;
            font-size: 18px;
            color: #ff3c5e;
            font-weight: bold;
            margin-top: 15px;
            
            
        }
        .trusted-text {
            background: blue;
            color: white;
            padding: 5px 10px;
            display: inline-block;
            border-radius: 5px;
            margin-top: 10px;
            font-size: 14px;
            font-weight: bold;
        }
        .real-label {
    background: red;
    color: white;
    padding: 5px 10px;
    display: inline-block;
    border-radius: 5px;
    margin-top: 15px;
    font-size: 14px;
    font-weight: bold;
}
    </style>
</head>
<body>
<div class="form-container">
    <h2>📢 Buy Social Media Services</h2>
    <form id="serviceForm">
        <label for="name">Full Name:</label>
        <input type="text" id="name" required>

        <label for="email">Gmail ID:</label>
        <input type="email" id="email" required>

        <label for="service">Select Service:</label>
        <select id="service" onchange="showOptions()" required>
            <option value="">-- Select --</option>
            <option value="youtube">📺 YouTube</option>
            <option value="instagram">📸 Instagram</option>
            <option value="facebook">📘 Facebook</option>
            <option value="telegram">📢 Telegram</option>
            <option value="other">🔍 Other</option>
        </select>

        <div id="otherServiceBox" class="hidden">
            <label for="otherService">Enter Your Required Service:</label>
            <input type="text" id="otherService" required>
        </div>

        <div id="serviceOptions" class="hidden">
            <label for="subService">Select Sub-Service:</label>
            <select id="subService" onchange="updatePrice()" required>
                <option value="">-- Select --</option>
            </select>
        </div>

        <div id="priceSection" class="hidden">
            <label for="quantity">Enter Quantity (Minimum 50):</label>
            <input type="number" id="quantity" value="50" min="50" oninput="updateTotal()" required>

            <p>Price per <span id="priceUnit">1000</span>: ₹<span id="unitPrice">0</span></p>
            <p><strong>Total Price: ₹<span id="totalPrice">0</span></strong></p>
        </div>

        <button type="submit">Proceed to Next</button>
        <div class="loading">🔄 Processing... Please wait</div>
    </form>

    <div class="real-label">✅ 100% Trusted & High-Quality Services</div>
    <div class="trusted-text">🔒 All Services Are Non-Drop & Lifetime</div>
</div>

<script>
        const priceList = {
            youtube: {
                "🎥 YouTube Views": 199,
                "👍 YouTube Likes": 199,
                "📢 YouTube Subscribers": 499,
                "⏳ 4000HR Watch Time": 4000,
                "📊 YouTube Community Vote": 10,
                "💬 YouTube Comments": 499,
                "👍💬 Likes + Comments": 50,
                "🎬 Live Stream View (30 min)": 50,
                "🎬 Live Stream View (90 min)": 100,
                "🎬 Live Stream View (2hr)": 150,
                "🎬 Live Stream View (15 min)": 25,
                "❤️ YouTube Live Stream Likes": 150
            },
            facebook: {
                "👥 Facebook Followers": 199,
                "📖 Facebook Story Views": 99,
                "🎥 Facebook Video View (10s)": 50,
                "🎬 Facebook Reel Views": 20,
                "❤️ Facebook Post Likes": 150,
                "👍 Facebook Page Likes": 200,
                "👤 Facebook Page Followers": 200,
                "👍👤 Likes + Followers": 250,
                "💰 60k Min Monetization": 199
            },
            instagram: {
                "👁 Instagram Story Impressions": 20,
                "📍 Instagram Profile Visits": 20,
                "👁‍🗨 Instagram Story Views": 20,
                "👀 Story Views + Impressions": 50,
                "🔄 Instagram Saves & Shares": 20,
                "💬 Instagram Comments": 100,
                "🎥 Instagram Video Views": 15,
                "🔥 Instagram Reel Views": 10,
                "🎬 Reel Views + Impressions": 20,
                "👥 Instagram Followers": 200,
                "👍 Instagram Likes": 25,
                "❤️👀 Likes + Impressions": 50,
                "✔️ Blue Tick Comments": 25
            },
            telegram: {
                "✔️ Telegram Group Members": 100,
                "📣 Telegram Channel Subscribers": 100,
                "👁‍🗨 Telegram Post Views": 100,
                "🔥 Telegram Reactions": 100
            }
        };

    function showOptions() {
        let service = document.getElementById('service').value;
        let subServiceDropdown = document.getElementById('subService');
        let otherServiceBox = document.getElementById('otherServiceBox');
        let serviceOptions = document.getElementById('serviceOptions');
        let priceSection = document.getElementById('priceSection');
        let submitButton = document.querySelector("button[type='submit']");

        if (service === "other") {
            otherServiceBox.classList.remove('hidden');
            serviceOptions.classList.add('hidden');
            priceSection.classList.add('hidden');
            submitButton.textContent = "Submit";
            return;
        } else {
            otherServiceBox.classList.add('hidden');
            serviceOptions.classList.remove('hidden');
            submitButton.textContent = "Proceed to Next";
        }

        subServiceDropdown.innerHTML = '<option value="">-- Select --</option>';
        for (let subService in priceList[service]) {
            let option = document.createElement('option');
            option.value = subService;
            option.textContent = subService;
            subServiceDropdown.appendChild(option);
        }
    }

    function updatePrice() {
        let service = document.getElementById('service').value;
        let subService = document.getElementById('subService').value;
        let unitPrice = priceList[service][subService] || 0;
        document.getElementById('unitPrice').textContent = unitPrice;
        document.getElementById('priceUnit').textContent = subService.includes("4000HR") ? "4000" : "1000";
        updateTotal();
        document.getElementById('priceSection').classList.remove('hidden');
    }

    function updateTotal() {
        let unitPrice = parseFloat(document.getElementById('unitPrice').textContent);
        let quantity = parseInt(document.getElementById('quantity').value);
        document.getElementById('totalPrice').textContent = (unitPrice * quantity) / (document.getElementById('priceUnit').textContent);
    }
        // 📩 EmailJS Integration
    (function() {
        emailjs.init("Wt1rPnRn_frLu5aO6"); // 🛑 YOUR EMAILJS USER ID

        document.getElementById('serviceForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Stop form submission

            let formData = {
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                service: document.getElementById('service').value,
                subService: document.getElementById('subService').value,
                quantity: document.getElementById('quantity').value,
                totalPrice: document.getElementById('totalPrice').textContent
            };

            emailjs.send("service_y415hfc", "template_dsuyzuj", formData)
                .then(function(response) {
                    alert("✅ Order received! Email sent successfully.");
                }, function(error) {
                    alert("❌ Failed to send email. Please try again.");
                });
        });
    })();
</script>
</body>
</html>
