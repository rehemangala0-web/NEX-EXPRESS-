<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>NEX EXPRESS - Modern Bus Ticket Booking</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary-blue: #0066cc;
            --secondary-blue: #004d99;
            --accent-gray: #f5f7fa;
            --dark-gray: #333333;
            --light-gray: #e6e9f0;
            --white: #ffffff;
            --success-green: #28a745;
            --warning-red: #dc3545;
            --seat-available: #e6e9f0;
            --seat-selected: #0066cc;
            --seat-booked: #dc3545;
            --shadow: 0 4px 12px rgba(0,0,0,0.1);
            --transition: all 0.3s ease;
        }

        body {
            background: linear-gradient(135deg, var(--accent-gray) 0%, var(--white) 100%);
            min-height: 100vh;
            color: var(--dark-gray);
        }

        /* Header & Navigation */
        header {
            background: var(--white);
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 1000;
            padding: 1rem 5%;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .logo {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary-blue);
            letter-spacing: 1px;
        }

        .logo span {
            color: var(--dark-gray);
            font-weight: 300;
        }

        .bus-icon {
            width: 50px;
            height: 50px;
            background: var(--primary-blue);
            border-radius: 50%;
            position: relative;
            animation: bounce 2s infinite;
        }

        .bus-icon::before {
            content: '🚌';
            font-size: 2rem;
            position: absolute;
            top: -5px;
            left: 5px;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            text-decoration: none;
            color: var(--dark-gray);
            font-weight: 500;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            transition: var(--transition);
            position: relative;
        }

        .nav-links a:hover {
            color: var(--primary-blue);
            background: var(--accent-gray);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 2px;
            background: var(--primary-blue);
            transition: var(--transition);
        }

        .nav-links a:hover::after {
            width: 80%;
        }

        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="0 0 100 100"><rect width="100" height="100" fill="%230066cc"/><circle cx="50" cy="50" r="30" fill="%23ffffff" opacity="0.1"/></svg>');
            background-size: cover;
            background-position: center;
            min-height: 500px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: var(--white);
            padding: 2rem;
        }

        .hero-content {
            max-width: 800px;
            width: 100%;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            animation: slideInDown 0.8s ease;
        }

        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            animation: slideInUp 0.8s ease;
        }

        /* Search Form */
        .search-form {
            background: var(--white);
            border-radius: 15px;
            padding: 2rem;
            box-shadow: var(--shadow);
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            animation: fadeIn 1s ease;
            margin-top: -50px;
            position: relative;
            z-index: 10;
        }

        .form-group {
            text-align: left;
        }

        .form-group label {
            display: block;
            color: var(--dark-gray);
            font-weight: 500;
            margin-bottom: 0.5rem;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid var(--light-gray);
            border-radius: 8px;
            font-size: 1rem;
            transition: var(--transition);
        }

        .form-group input:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary-blue);
        }

        .search-btn {
            background: var(--primary-blue);
            color: var(--white);
            border: none;
            padding: 0.8rem 2rem;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            align-self: flex-end;
        }

        .search-btn:hover {
            background: var(--secondary-blue);
            transform: translateY(-2px);
            box-shadow: var(--shadow);
        }

        /* Main Content */
        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        /* Booking Form Section */
        .booking-section {
            background: var(--white);
            border-radius: 15px;
            padding: 2rem;
            box-shadow: var(--shadow);
            margin-bottom: 2rem;
        }

        .section-title {
            color: var(--primary-blue);
            margin-bottom: 2rem;
            font-size: 1.8rem;
            position: relative;
            padding-bottom: 0.5rem;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 60px;
            height: 3px;
            background: var(--primary-blue);
        }

        .booking-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        /* Seat Selection */
        .seat-map-container {
            background: var(--white);
            border-radius: 10px;
            padding: 1.5rem;
            border: 2px solid var(--light-gray);
        }

        .seat-map {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
            max-width: 400px;
            margin: 0 auto;
        }

        .seat-row {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
        }

        .seat {
            width: 45px;
            height: 45px;
            background: var(--seat-available);
            border: 2px solid var(--light-gray);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
        }

        .seat.aisle {
            margin-left: 1rem;
        }

        .seat.aisle::before {
            content: '⬇️';
            position: absolute;
            left: -20px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 0.8rem;
            opacity: 0.5;
        }

        .seat.aisle::after {
            content: '⬆️';
            position: absolute;
            right: -20px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 0.8rem;
            opacity: 0.5;
        }

        .seat:hover:not(.booked) {
            background: var(--primary-blue);
            color: var(--white);
            transform: scale(1.05);
            border-color: var(--primary-blue);
        }

        .seat.selected {
            background: var(--seat-selected);
            color: var(--white);
            border-color: var(--seat-selected);
        }

        .seat.booked {
            background: var(--seat-booked);
            color: var(--white);
            border-color: var(--seat-booked);
            cursor: not-allowed;
            opacity: 0.7;
        }

        .seat[data-tooltip] {
            position: relative;
        }

        .seat[data-tooltip]:hover::before {
            content: attr(data-tooltip);
            position: absolute;
            bottom: 100%;
            left: 50%;
            transform: translateX(-50%);
            padding: 0.5rem;
            background: var(--dark-gray);
            color: var(--white);
            border-radius: 4px;
            font-size: 0.75rem;
            white-space: nowrap;
            z-index: 100;
        }

        /* Signature Pad */
        .signature-pad {
            border: 2px solid var(--light-gray);
            border-radius: 8px;
            padding: 1rem;
            margin-top: 1rem;
        }

        .signature-pad canvas {
            width: 100%;
            height: 150px;
            border: 1px solid var(--light-gray);
            border-radius: 4px;
            background: var(--white);
        }

        .signature-actions {
            display: flex;
            gap: 1rem;
            margin-top: 0.5rem;
        }

        .btn-small {
            padding: 0.5rem 1rem;
            background: var(--light-gray);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9rem;
        }

        .btn-small:hover {
            background: var(--primary-blue);
            color: var(--white);
        }

        /* Payment Button */
        .payment-section {
            text-align: center;
            margin: 2rem 0;
        }

        .payment-btn {
            background: var(--success-green);
            color: var(--white);
            border: none;
            padding: 1rem 3rem;
            border-radius: 50px;
            font-size: 1.2rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: var(--shadow);
        }

        .payment-btn:hover {
            background: #218838;
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(40, 167, 69, 0.3);
        }

        /* Ticket Card */
        .ticket-card {
            background: var(--white);
            border-radius: 15px;
            padding: 2rem;
            box-shadow: var(--shadow);
            border: 2px solid var(--light-gray);
            margin-top: 2rem;
            display: none;
        }

        .ticket-card.show {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        .ticket-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding-bottom: 1rem;
            border-bottom: 2px dashed var(--light-gray);
        }

        .ticket-qr {
            text-align: center;
        }

        .ticket-qr canvas {
            width: 100px;
            height: 100px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
        }

        .ticket-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .detail-item {
            padding: 0.5rem;
            background: var(--accent-gray);
            border-radius: 5px;
        }

        .detail-item strong {
            color: var(--primary-blue);
            display: block;
            margin-bottom: 0.25rem;
        }

        .ticket-actions {
            display: flex;
            gap: 1rem;
            justify-content: flex-end;
            margin-top: 1.5rem;
        }

        .download-btn {
            background: var(--primary-blue);
            color: var(--white);
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 5px;
            cursor: pointer;
            transition: var(--transition);
            font-weight: 500;
        }
        download-btn:hover {
            background: var(--secondary-blue);
        }

        /* Admin Panel */
        .admin-panel {
            background: var(--white);
            border-radius: 15px;
            padding: 2rem;
            box-shadow: var(--shadow);
            margin-top: 2rem;
        }

        .admin-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            border-bottom: 2px solid var(--light-gray);
            padding-bottom: 1rem;
        }

        .tab-btn {
            padding: 0.5rem 1.5rem;
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 500;
            color: var(--dark-gray);
            cursor: pointer;
            transition: var(--transition);
            border-radius: 5px;
        }

        .tab-btn:hover {
            background: var(--light-gray);
            color: var(--primary-blue);
        }

        .tab-btn.active {
            background: var(--primary-blue);
            color: var(--white);
        }

        .admin-content {
            display: none;
        }

        .admin-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        .bookings-table {
            width: 100%;
            border-collapse: collapse;
        }

        .bookings-table th {
            background: var(--primary-blue);
            color: var(--white);
            padding: 1rem;
            text-align: left;
        }

        .bookings-table td {
            padding: 1rem;
            border-bottom: 1px solid var(--light-gray);
        }

        .bookings-table tr:hover {
            background: var(--accent-gray);
        }

        /* User Account */
        .user-bookings {
            background: var(--white);
            border-radius: 15px;
            padding: 2rem;
            box-shadow: var(--shadow);
        }

        .booking-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            margin-bottom: 1rem;
            transition: var(--transition);
        }

        .booking-item:hover {
            border-color: var(--primary-blue);
            box-shadow: var(--shadow);
        }

        .booking-info {
            flex: 1;
        }

        .booking-actions {
            display: flex;
            gap: 0.5rem;
        }

        .action-btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9rem;
        }

        .edit-btn {
            background: var(--primary-blue);
            color: var(--white);
        }

        .cancel-btn {
            background: var(--warning-red);
            color: var(--white);
        }

        .action-btn:hover {
            opacity: 0.8;
            transform: translateY(-2px);
        }

        /* Footer */
        footer {
            background: var(--dark-gray);
            color: var(--white);
            text-align: center;
            padding: 2rem;
            margin-top: 3rem;
        }

        /* Animations */
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        @keyframes slideInDown {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes slideInUp {
            from {
                transform: translateY(50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }

            .hero h1 {
                font-size: 2rem;
            }

            .search-form {
                grid-template-columns: 1fr;
                margin-top: -30px;
                padding: 1.5rem;
            }

            .booking-grid {
                grid-template-columns: 1fr;
            }

            .seat-row {
                gap: 0.25rem;
            }

            .seat {
                width: 35px;
                height: 35px;
                font-size: 0.7rem;
            }

            .seat.aisle::before,
            .seat.aisle::after {
                display: none;
            }

            .ticket-details {
                grid-template-columns: 1fr;
            }

            .ticket-actions {
                flex-direction: column;
            }

            .download-btn {
                width: 100%;
            }

            .bookings-table {
                display: block;
                overflow-x: auto;
            }

            .booking-item {
                flex-direction: column;
                gap: 1rem;
                text-align: center;
            }

            .booking-actions {
                width: 100%;
                justify-content: center;
            }

            .admin-tabs {
                flex-wrap: wrap;
            }

            .tab-btn {
                flex: 1 1 auto;
            }
        }

        /* Utility Classes */
        .text-center { text-align: center; }
        .mt-2 { margin-top: 2rem; }
        .mb-2 { margin-bottom: 2rem; }
        .hidden { display: none; }
    </style>
</head>
<body>
    <header>
        <nav>
            <div class="logo-container">
                <div class="bus-icon"></div>
                <div class="logo">NEX <span>EXPRESS</span></div>
            </div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#booking">Book Ticket</a></li>
                <li><a href="#my-bookings">My Bookings</a></li>
                <li><a href="#admin">Admin</a></li>
            </ul>
        </nav>
    </header>

    <section class="hero" id="home">
        <div class="hero-content">
            <h1>Travel Safely with NEX EXPRESS</h1>
            <p>Book your bus tickets online with ease • MBEYA ↔ DAR ES SALAAM</p>
        </div>
    </section>

    <div class="container">
        <!-- Search Form -->
        <div class="search-form">
            <div class="form-group">
                <label>From</label>
                <select id="from-location">
                    <option value="MBEYA">MBEYA</option>
                    <option value="DAR ES SALAAM">DAR ES SALAAM</option>
                </select>
            </div>
            <div class="form-group">
                <label>To</label>
                <select id="to-location">
                    <option value="DAR ES SALAAM">DAR ES SALAAM</option>
                    <option value="MBEYA">MBEYA</option>
                </select>
            </div>
            <div class="form-group">
                <label>Travel Date</label>
                <input type="date" id="travel-date" min="2025-01-01" value="2025-02-20">
            </div>
            <div class="form-group">
                <label>Passengers</label>
                <input type="number" id="passengers" min="1" max="10" value="1">
            </div>
            <button class="search-btn" onclick="searchBuses()">Search Available Buses</button>
        </div>

        <!-- Booking Form Section -->
        <section class="booking-section" id="booking">
            <h2 class="section-title">Book Your Ticket</h2>
            <div class="booking-grid">
                <!-- Passenger Details -->
                <div>
                    <h3 style="color: var(--primary-blue); margin-bottom: 1rem;">Passenger Information</h3>
                    <div class="form-group">
                        <label>Full Name</label>
                        <input type="text" id="passenger-name" placeholder="Enter your full name">
                    </div>
                    <div class="form-group">
                        <label>Phone Number</label>
                        <input type="tel" id="phone-number" placeholder="+255 xxx xxx xxx">
                    </div>
                    <div class="form-group">
                        <label>Bus Plate Number</label>
                        <select id="bus-plate">
                            <option value="T 123 ABC">T 123 ABC - Executive Coach</option>
                            <option value="T 456 DEF">T 456 DEF - Luxury Bus</option>
                            <option value="T 789 GHI">T 789 GHI - Standard Bus</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Fare (TZS)</label>
                        <input type="text" id="fare" value="45,000" readonly>
                    </div>
                    <div class="form-group">
                        <label>Ticket Issue Date</label>
                        <input type="text" id="issue-date" readonly>
                    </div>
                    <div class="form-group">
                        <label>Departure Time</label>
                        <select id="departure-time">
                            <option value="06:00">06:00 AM</option>
                            <option value="09:00">09:00 AM</option>
                            <option value="14:00">02:00 PM</option>
                            <option value="19:00">07:00 PM</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Arrival Time</label>
                        <select id="arrival-time">
                            <option value="14:00">02:00 PM</option>
                            <option value="17:00">05:00 PM</option>
                            <option value="22:00">10:00 PM</option>
                            <option value="03:00">03:00 AM (+1)</option>
                        </select>
                    </div>

                    <!-- Signature Pad -->
                    <div class="signature-pad">
                        <label style="display: block; margin-bottom: 0.5rem;">Passenger Signature</label>
                        <canvas id="signature-canvas" width="300" height="150"></canvas>
                        <div class="signature-actions">
                            <button class="btn-small" onclick="clearSignature()">Clear</button>
                            <button class="btn-small" onclick="saveSignature()">Save</button>
                        </div>
                    </div>
                </div>

                <!-- Seat Selection -->
                <div>
                    <h3 style="color: var(--primary-blue); margin-bottom: 1rem;">Select Your Seat</h3>
                    <div class="seat-map-container">
                        <div class="seat-map" id="seat-map">
                            <!-- Seats will be generated by JavaScript -->
                        </div>
                        <div style="display: flex; gap: 1rem; justify-content: center; margin-top: 1rem; flex-wrap: wrap;">
                            <div style="display: flex; align-items: center; gap: 0.5rem;">
                                <div style="width: 20px; height: 20px; background: var(--seat-available); border: 1px solid var(--light-gray);"></div>
                                <span>Available</span>
                            </div>
                            <div style="display: flex; align-items: center; gap: 0.5rem;">
                                <div style="width: 20px; height: 20px; background: var(--seat-selected);"></div>
                                <span>Selected</span>
                            </div>
                            <div style="display: flex; align-items: center; gap: 0.5rem;">
                                <div style="width: 20px; height: 20px; background: var(--seat-booked);"></div>
                                <span>Booked</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Payment Section -->
            <div class="payment-section">
                <button class="payment-btn" onclick="processPayment()">Confirm Booking & Pay via WhatsApp</button>
            </div>

            <!-- Generated Ticket -->
            <div class="ticket-card" id="ticket-card">
                <div class="ticket-header">
                    <h2 style="color: var(--primary-blue);">NEX EXPRESS - E-Ticket</h2>
                    <div class="ticket-qr" id="qr-code"></div>
                </div>
                <div class="ticket-details" id="ticket-details">
                    <!-- Ticket details will be filled by JavaScript -->
                </div>
                <div class="signature-pad" style="margin-top: 1rem;">
                    <p><strong>Passenger Signature:</strong></p>
                    <canvas id="ticket-signature" width="300" height="100" style="width: 100%; height: 80px;"></canvas>
                </div>
                <div class="ticket-actions">
                    <button class="download-btn" onclick="downloadTicket()">Download PDF Ticket</button>
                    <button class="download-btn" onclick="printTicket()">Print Ticket</button>
                </div>
            </div>
        </section>

        <!-- User Bookings Section -->
        <section class="user-bookings" id="my-bookings">
            <h2 class="section-title">My Bookings</h2>
            <div id="bookings-list">
                <!-- Bookings will be displayed here -->
            </div>
        </section>
            <!-- Admin Panel -->
        <section class="admin-panel" id="admin">
            <h2 class="section-title">Admin Dashboard</h2>
            <div class="admin-tabs">
                <button class="tab-btn active" onclick="showAdminTab('routes')">Routes</button>
                <button class="tab-btn" onclick="showAdminTab('bookings')">Bookings</button>
                <button class="tab-btn" onclick="showAdminTab('reports')">Reports</button>
            </div>
            
            <!-- Routes Management -->
            <div class="admin-content active" id="routes-content">
                <button class="search-btn" style="margin-bottom: 1rem;" onclick="addRoute()">+ Add New Route</button>
                <table class="bookings-table">
                    <thead>
                        <tr>
                            <th>Route</th>
                            <th>Departure</th>
                            <th>Arrival</th>
                            <th>Price</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="routes-list">
                        <tr>
                            <td>MBEYA → DAR ES SALAAM</td>
                            <td>06:00 AM</td>
                            <td>02:00 PM</td>
                            <td>45,000 TZS</td>
                            <td>
                                <button class="btn-small" onclick="editRoute(this)">Edit</button>
                                <button class="btn-small" style="background: var(--warning-red); color: white;" onclick="deleteRoute(this)">Delete</button>
                            </td>
                        </tr>
                        <tr>
                            <td>DAR ES SALAAM → MBEYA</td>
                            <td>09:00 AM</td>
                            <td>05:00 PM</td>
                            <td>45,000 TZS</td>
                            <td>
                                <button class="btn-small" onclick="editRoute(this)">Edit</button>
                                <button class="btn-small" style="background: var(--warning-red); color: white;" onclick="deleteRoute(this)">Delete</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Bookings Management -->
            <div class="admin-content" id="bookings-content">
                <table class="bookings-table">
                    <thead>
                        <tr>
                            <th>Booking ID</th>
                            <th>Passenger</th>
                            <th>Route</th>
                            <th>Date</th>
                            <th>Seat</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="admin-bookings-list">
                        <!-- Bookings will be populated here -->
                    </tbody>
                </table>
            </div>

            <!-- Reports -->
            <div class="admin-content" id="reports-content">
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; margin-bottom: 2rem;">
                    <div class="detail-item">
                        <strong>Daily Revenue</strong>
                        <span id="daily-revenue">0 TZS</span>
                    </div>
                    <div class="detail-item">
                        <strong>Monthly Revenue</strong>
                        <span id="monthly-revenue">0 TZS</span>
                    </div>
                    <div class="detail-item">
                        <strong>Yearly Revenue</strong>
                        <span id="yearly-revenue">0 TZS</span>
                    </div>
                </div>
                <button class="search-btn" onclick="generateReport('daily')">Download Daily Report</button>
                <button class="search-btn" onclick="generateReport('monthly')">Download Monthly Report</button>
                <button class="search-btn" onclick="generateReport('yearly')">Download Yearly Report</button>
            </div>
        </section>
    </div>

    <footer>
        <p>&copy; 2025 NEX EXPRESS. All rights reserved. | Safe Travels, Modern Comfort</p>
    </footer>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script>
        // Global variables
        let selectedSeat = null;
        let bookedSeats = ['1A', '2B', '3C']; // Example booked seats
        let currentBooking = null;
        let signatureData = null;
        let bookings = JSON.parse(localStorage.getItem('bookings')) || [];

        // Initialize the page
        document.addEventListener('DOMContentLoaded', function() {
            generateSeatMap();
            setCurrentDate();
            initializeSignaturePad();
            loadBookings();
            updateAdminBookings();
            updateReports();
        });

        // Set current date for ticket issue
        function setCurrentDate() {
            const today = new Date();
            const dateString = today.toLocaleDateString('en-US', { 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            });
            document.getElementById('issue-date').value = dateString;
        }

        // Generate interactive seat map
        function generateSeatMap() {
            const seatMap = document.getElementById('seat-map');
            seatMap.innerHTML = '';
            
            const rows = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'];
            const seatsPerRow = 4; // 2x2 layout
            
            rows.forEach(row => {
                const rowDiv = document.createElement('div');
                rowDiv.className = 'seat-row';
                
                for (let i = 1; i <= seatsPerRow; i++) {
                    const seatNumber = row + i;
                    const seat = document.createElement('div');
                    seat.className = 'seat';
                    
                    // Add aisle indicator after second seat
                    if (i === 2) {
                        seat.classList.add('aisle');
                    }
                    
                    seat.textContent = seatNumber;
                    seat.setAttribute('data-seat', seatNumber);
                    seat.setAttribute('data-tooltip', `Seat ${seatNumber} - ${bookedSeats.includes(seatNumber) ? 'Booked' : 'Available'}`);
                    
                    if (bookedSeats.includes(seatNumber)) {
                        seat.classList.add('booked');
                    } else {
                        seat.onclick = function() { selectSeat(this); };
                    }
                    
                    rowDiv.appendChild(seat);
                }
                seatMap.appendChild(rowDiv);
            });
        }

        // Select seat function
        function selectSeat(seatElement) {
            if (seatElement.classList.contains('booked')) {
                alert('This seat is already booked!');
                return;
            }
            
            // Deselect previous seat
            if (selectedSeat) {
                selectedSeat.classList.remove('selected');
            }
            
            // Select new seat
            seatElement.classList.add('selected');
            selectedSeat = seatElement;
        }

        // Clear signature pad
        function clearSignature() {
            const canvas = document.getElementById('signature-canvas');
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            signatureData = null;
        }

        // Save signature
        function saveSignature() {
            const canvas = document.getElementById('signature-canvas');
            signatureData = canvas.toDataURL();
            alert('Signature saved successfully!');
        }

        // Initialize signature pad with drawing capability
        function initializeSignaturePad() {
            const canvas = document.getElementById('signature-canvas');
            const ctx = canvas.getContext('2d');
            let drawing = false;
            
            canvas.addEventListener('mousedown', startDrawing);
            canvas.addEventListener('mousemove', draw);
            canvas.addEventListener('mouseup', stopDrawing);
            canvas.addEventListener('mouseleave', stopDrawing);
            
            // Touch support for mobile
            canvas.addEventListener('touchstart', startDrawing);
            canvas.addEventListener('touchmove', draw);
            canvas.addEventListener('touchend', stopDrawing);
            
            function startDrawing(e) {
                e.preventDefault();
                drawing = true;
                ctx.beginPath();
                ctx.lineWidth = 2;
                ctx.strokeStyle = '#000';
            }
            
            function draw(e) {
                e.preventDefault();
                if (!drawing) return;
                
                const rect = canvas.getBoundingClientRect();
                const x = (e.clientX || e.touches[0].clientX) - rect.left;
                const y = (e.clientY || e.touches[0].clientY) - rect.top;
                
                ctx.lineTo(x, y);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(x, y);
            }
            
            function stopDrawing() {
                drawing = false;
            }
        }

        // Process payment and send via WhatsApp
        function processPayment() {
            // Validate form
            if (!validateBookingForm()) {
                return;
            }
            
            if (!selectedSeat) {
                alert('Please select a seat!');
                return;
            }
            
            // Get form values
            const passengerName = document.getElementById('passenger-name').value;
            const phoneNumber = document.getElementById('phone-number').value;
            const fromLocation = document.getElementById('from-location').value;
            const toLocation = document.getElementById('to-location').value;
            const travelDate = document.getElementById('travel-date').value;
            const busPlate = document.getElementById('bus-plate').value;
            const departureTime = document.getElementById('departure-time').value;
            const arrivalTime = document.getElementById('arrival-time').value;
            const fare = document.getElementById('fare').value;
            const seatNumber = selectedSeat.getAttribute('data-seat');
            
            // Create booking object
            currentBooking = {
                id: 'BK' + Date.now(),
                passengerName,
                phoneNumber,
                fromLocation,
                toLocation,
                travelDate,
                busPlate,
                departureTime,
                arrivalTime,
                fare,
                seatNumber,
                signature: signatureData,
                timestamp: new Date().toISOString(),
                status: 'pending'
            };
            
            // Create WhatsApp message
            const message = `NEW BOOKING REQUEST - NEX EXPRESS%0A%0A` +
                `Booking ID: ${currentBooking.id}%0A` +
                `Passenger: ${passengerName}%0A` +
                `Phone: ${phoneNumber}%0A` +
                `Route: ${fromLocation} → ${toLocation}%0A` +
                `Date: ${travelDate}%0A` +
                `Time: ${departureTime} - ${arrivalTime}%0A` +
                `Bus: ${busPlate}%0A` +
                `Seat: ${seatNumber}%0A` +
                `Fare: ${fare} TZS%0A%0A` +
                `Please confirm payment to generate ticket.`;
            
            // Open WhatsApp
            const whatsappUrl = `https://wa.me/255789269000?text=${message}`;
            window.open(whatsappUrl, '_blank');
            
            // After payment confirmation (simulated)
            setTimeout(() => {
                confirmPayment();
            }, 5000);
        }

        // Confirm payment and generate ticket
        function confirmPayment() {
            if (!currentBooking) return;
            
            // Update booking status
            currentBooking.status = 'confirmed';
            bookings.push(currentBooking);
            localStorage.setItem('bookings', JSON.stringify(bookings));
            
            // Generate ticket
            generateTicket(currentBooking);
            
            // Mark seat as booked
            if (selectedSeat) {
                selectedSeat.classList.remove('selected');
                selectedSeat.classList.add('booked');
                bookedSeats.push(selectedSeat.getAttribute('data-seat'));
            }
            
            // Show ticket
            document.getElementById('ticket-card').classList.add('show');
            
            // Update bookings list
            loadBookings();
            updateAdminBookings();
            updateReports();
            
            alert('Payment confirmed! Your ticket has been generated.');
        }
        
        // Generate ticket with QR code
        function generateTicket(booking) {
            // Fill ticket details
            const ticketDetails = document.getElementById('ticket-details');
            ticketDetails.innerHTML = `
                <div class="detail-item">
                    <strong>Booking ID</strong>
                    <span>${booking.id}</span>
                </div>
                <div class="detail-item">
                    <strong>Passenger</strong>
                    <span>${booking.passengerName}</span>
                </div>
                <div class="detail-item">
                    <strong>Phone</strong>
                    <span>${booking.phoneNumber}</span>
                </div>
                <div class="detail-item">
                    <strong>Route</strong>
                    <span>${booking.fromLocation} → ${booking.toLocation}</span>
                </div>
                <div class="detail-item">
                    <strong>Date</strong>
                    <span>${booking.travelDate}</span>
                </div>
                <div class="detail-item">
                    <strong>Time</strong>
                    <span>${booking.departureTime} - ${booking.arrivalTime}</span>
                </div>
                <div class="detail-item">
                    <strong>Bus Plate</strong>
                    <span>${booking.busPlate}</span>
                </div>
                <div class="detail-item">
                    <strong>Seat</strong>
                    <span>${booking.seatNumber}</span>
                </div>
                <div class="detail-item">
                    <strong>Fare</strong>
                    <span>${booking.fare} TZS</span>
                </div>
            `;
            
            // Generate QR code
            const qrContainer = document.getElementById('qr-code');
            qrContainer.innerHTML = '';
            new QRCode(qrContainer, {
                text: `NEX-TICKET:${booking.id}`,
                width: 100,
                height: 100
            });
            
            // Copy signature to ticket
            if (signatureData) {
                const ticketSignature = document.getElementById('ticket-signature');
                const ctx = ticketSignature.getContext('2d');
                const img = new Image();
                img.onload = function() {
                    ctx.drawImage(img, 0, 0, ticketSignature.width, ticketSignature.height);
                };
                img.src = signatureData;
            }
        }

        // Download PDF ticket
        function downloadTicket() {
            if (!currentBooking) return;
            
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Add content to PDF
            doc.setFontSize(20);
            doc.setTextColor(0, 102, 204);
            doc.text('NEX EXPRESS - E-Ticket', 20, 20);
            
            doc.setFontSize(12);
            doc.setTextColor(0, 0, 0);
            
            let y = 40;
            const details = [
                `Booking ID: ${currentBooking.id}`,
                `Passenger: ${currentBooking.passengerName}`,
                `Phone: ${currentBooking.phoneNumber}`,
                `Route: ${currentBooking.fromLocation} → ${currentBooking.toLocation}`,
                `Date: ${currentBooking.travelDate}`,
                `Time: ${currentBooking.departureTime} - ${currentBooking.arrivalTime}`,
                `Bus: ${currentBooking.busPlate}`,
                `Seat: ${currentBooking.seatNumber}`,
                `Fare: ${currentBooking.fare} TZS`
            ];
            
            details.forEach(detail => {
                doc.text(detail, 20, y);
                y += 10;
            });
            
            // Save PDF
            doc.save(`NEX-Ticket-${currentBooking.id}.pdf`);
        }

        // Print ticket
        function printTicket() {
            window.print();
        }

        // Validate booking form
        function validateBookingForm() {
            const name = document.getElementById('passenger-name').value;
            const phone = document.getElementById('phone-number').value;
            
            if (!name || name.length < 3) {
                alert('Please enter a valid name');
                return false;
            }
            
            if (!phone || phone.length < 10) {
                alert('Please enter a valid phone number');
                return false;
            }
            
            return true;
        }

        // Search buses
        function searchBuses() {
            const from = document.getElementById('from-location').value;
            const to = document.getElementById('to-location').value;
            const date = document.getElementById('travel-date').value;
            const passengers = document.getElementById('passengers').value;
            
            alert(`Found buses from ${from} to ${to} on ${date} for ${passengers} passenger(s)`);
            
            // Scroll to booking form
            document.getElementById('booking').scrollIntoView({ behavior: 'smooth' });
        }

        // Load user bookings
        function loadBookings() {
            const bookingsList = document.getElementById('bookings-list');
            const userBookings = bookings.filter(b => b.status === 'confirmed');
            
            if (userBookings.length === 0) {
                bookingsList.innerHTML = '<p style="text-align: center; padding: 2rem;">No bookings found.</p>';
                return;
            }
            
            bookingsList.innerHTML = userBookings.map(booking => `
                <div class="booking-item">
                    <div class="booking-info">
                        <strong>${booking.id}</strong><br>
                        ${booking.fromLocation} → ${booking.toLocation}<br>
                        ${booking.travelDate} | Seat: ${booking.seatNumber}
                    </div>
                    <div class="booking-actions">
                        <button class="action-btn edit-btn" onclick="modifyBooking('${booking.id}')">Modify</button>
                        <button class="action-btn cancel-btn" onclick="cancelBooking('${booking.id}')">Cancel</button>
                        <button class="action-btn edit-btn" onclick="downloadExistingTicket('${booking.id}')">Download</button>
                    </div>
                </div>
            `).join('');
        }

        // Modify booking
        function modifyBooking(bookingId) {
            alert(`Modify booking: ${bookingId}`);
            // Implement modification logic
        }

        // Cancel booking
        function cancelBooking(bookingId) {
            if (confirm('Are you sure you want to cancel this booking?')) {
                bookings = bookings.filter(b => b.id !== bookingId);
                localStorage.setItem('bookings', JSON.stringify(bookings));
                loadBookings();
                updateAdminBookings();
                updateReports();
                alert('Booking cancelled successfully!');
            }
        }

        // Download existing ticket
        function downloadExistingTicket(bookingId) {
            const booking = bookings.find(b => b.id === bookingId);
            if (booking) {
                currentBooking = booking;
                downloadTicket();
            }
        }

        // Admin functions
        function showAdminTab(tabName) {
            // Update tab buttons
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.admin-content').forEach(content => content.classList.remove('active'));
            
            document.querySelector(`[onclick="showAdminTab('${tabName}')"]`).classList.add('active');
            document.getElementById(`${tabName}-content`).classList.add('active');
        }

        function addRoute() {
            const route = prompt('Enter route (e.g., MBEYA → DAR ES SALAAM):');
            if (route) {
                const tbody = document.getElementById('routes-list');
                const newRow = tbody.insertRow();
                newRow.innerHTML = `
                    <td>${route}</td>
                    <td>06:00 AM</td>
                    <td>02:00 PM</td>
                    <td>45,000 TZS</td>
                    <td>
                        <button class="btn-small" onclick="editRoute(this)">Edit</button>
                        <button class="btn-small" style="background: var(--warning-red); color: white;" onclick="deleteRoute(this)">Delete</button>
                    </td>
                `;
            }
        }

        function editRoute(btn) {
            const row = btn.closest('tr');
            const route = row.cells[0].textContent;
            const newRoute = prompt('Edit route:', route);
            if (newRoute) {
                row.cells[0].textContent = newRoute;
            }
        }

        function deleteRoute(btn) {
            if (confirm('Are you sure you want to delete this route?')) {
                btn.closest('tr').remove();
            }
        }

        function updateAdminBookings() {
            const tbody = document.getElementById('admin-bookings-list');
            const confirmedBookings = bookings.filter(b => b.status === 'confirmed');
            
            tbody.innerHTML = confirmedBookings.map(booking => `
                <tr>
                    <td>${booking.id}</td>
                    <td>${booking.passengerName}</td>
                    <td>${booking.fromLocation} → ${booking.toLocation}</td>
                    <td>${booking.travelDate}</td>
                    <td>${booking.seatNumber}</td>
                    <td><span style="color: var(--success-green);">Confirmed</span></td>
                    <td>
                        <button class="btn-small" onclick="viewBookingDetails('${booking.id}')">View</button>
                    </td>
                </tr>
            `).join('');
        }

        function updateReports() {
            const confirmedBookings = bookings.filter(b => b.status === 'confirmed');
            const totalRevenue = confirmedBookings.reduce((sum, b) => sum + 45000, 0);
            
            document.getElementById('daily-revenue').textContent = `${totalRevenue.toLocaleString()} TZS`;
            document.getElementById('monthly-revenue').textContent = `${(totalRevenue * 30).toLocaleString()} TZS`;
            document.getElementById('yearly-revenue').textContent = `${(totalRevenue * 365).toLocaleString()} TZS`;
        }

        function generateReport(period) {
            const confirmedBookings = bookings.filter(b => b.status === 'confirmed');
            const revenue = confirmedBookings.length * 45000;
            
            let report = `NEX EXPRESS - ${period.toUpperCase()} REPORT\n`;
            report += `Generated: ${new Date().toLocaleString()}\n`;
            report += `Total Bookings: ${confirmedBookings.length}\n`;
            report += `Total Revenue: ${revenue.toLocaleString()} TZS\n\n`;
            report += `Bookings Details:\n`;
            
            confirmedBookings.forEach(booking => {
                report += `${booking.id} - ${booking.passengerName} - ${booking.fromLocation}→${booking.toLocation} - ${booking.travelDate}\n`;
            });
            
            // Create and download report file
            const blob = new Blob([report], { type: 'text/plain' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `nex-express-${period}-report-${new Date().toISOString().split('T')[0]}.txt`;
            a.click();
        }

        function viewBookingDetails(bookingId) {
            const booking = bookings.find(b => b.id === bookingId);
            if (booking) {
                alert(`Booking Details:\n\nID: ${booking.id}\nPassenger: ${booking.passengerName}\nPhone: ${booking.phoneNumber}\nRoute: ${booking.fromLocation} → ${booking.toLocation}\nDate: ${booking.travelDate}\nSeat: ${booking.seatNumber}`);
            }
        }

        // Smooth scroll for navigation
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    targetElement.scrollIntoView({ behavior: 'smooth' });
                }
            });
        });
    </script>
</body>
</html># NEX-EXPRESS-
