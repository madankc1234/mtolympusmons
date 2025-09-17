<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mt Olympus Mons - Journey to Mars</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #0B0F1A; /* Space Black */
            color: #F6F7F9; /* Off-White */
            font-family: 'Orbitron', sans-serif; /* Futuristic font */
            overflow-x: hidden;
        }
        @import url('https://fonts.googleapis.com/css2?family=Orbitron&display=swap');
        header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://via.placeholder.com/1920x800?text=Olympus+Mons+Panorama');
            background-size: cover;
            height: 100vh;
            text-align: center;
            padding-top: 20vh;
            animation: fadeIn 2s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        nav {
            background: #333;
            padding: 1rem;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
        }
        nav a {
            color: #F6F7F9;
            text-decoration: none;
            margin: 0 2rem;
            transition: color 0.3s;
        }
        nav a:hover {
            color: #FF6A3D; /* Sunset Orange */
        }
        .section {
            padding: 5rem 2rem;
            text-align: center;
            min-height: 100vh;
        }
        .booking-form {
            max-width: 600px;
            margin: 2rem auto;
            background: rgba(255, 255, 255, 0.05);
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(193, 68, 14, 0.3); /* Martian Red glow */
        }
        .booking-form input, .booking-form select {
            width: 100%;
            padding: 1rem;
            margin: 0.5rem 0;
            border: none;
            border-radius: 5px;
            background: rgba(255, 255, 255, 0.1);
            color: #F6F7F9;
        }
        .booking-btn {
            background: #C1440E; /* Martian Red */
            color: white;
            padding: 1rem 2rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s;
        }
        .booking-btn:hover {
            transform: scale(1.05);
        }
        .disclaimer {
            color: #8FBCE6; /* Ice Blue */
            font-size: 0.9rem;
            margin-top: 1rem;
        }
        .explorer {
            width: 100%;
            height: 70vh;
            border: 1px solid #C1440E;
            border-radius: 10px;
        }
        .leaderboard {
            background: linear-gradient(45deg, #C1440E, #FF6A3D);
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(255, 106, 61, 0.5);
        }
        .passport, .golden-ticket {
            display: none;
            background: #FF6A3D;
            padding: 1rem;
            margin: 1rem auto;
            max-width: 400px;
            border-radius: 10px;
        }
        footer {
            background: #333;
            padding: 1rem;
            text-align: center;
            position: relative;
            bottom: 0;
            width: 100%;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>
    <header>
        <h1>Mt Olympus Mons</h1>
        <h3>The First Travel Agency for Mars</h3>
        <p>For Fun, Forever</p>
    </header>
    <nav>
        <a href="#home">Home</a>
        <a href="#explore">Explore</a>
        <a href="#leaderboard">Leaderboard</a>
        <a href="#contact">Contact</a>
    </nav>
    <div class="section" id="home">
        <h2>Reserve Your Fun Ticket to Mars</h2>
        <p>Embark on a futuristic journey to Olympus Mons—only $5 for your digital boarding pass!</p>
        <div class="disclaimer">This is a novelty digital ticket, not an actual Mars flight. All purchases are for entertainment only.</div>
        <div class="booking-form">
            <input type="text" id="name" placeholder="Your Name" required>
            <input type="email" id="email" placeholder="Your Email" required>
            <select id="year" required>
                <option value="">Departure Year</option>
                <option value="2080">2080</option>
                <option value="2085">2085</option>
                <option value="2090">2090</option>
            </select>
            <select id="package" required>
                <option value="">Select Package</option>
                <option value="olympus">Olympus Mons Climb</option>
                <option value="sunset">Martian Sunset Dinner</option>
            </select>
            <button class="booking-btn" onclick="bookTicket()">Buy Your Novelty Ticket ($5)</button>
        </div>
    </div>
    <div class="section" id="explore">
        <h2>Explore Olympus Mons</h2>
        <p>Navigate the solar system’s tallest volcano in 3D!</p>
        <div class="explorer" id="explorer-container"></div>
    </div>
    <div class="section" id="leaderboard">
        <h2>Mars Tourists Leaderboard</h2>
        <p>12,345 brave souls have booked their Mars adventure!</p>
        <div class="passport" id="passport">
            <h3>Mars Passport</h3>
            <p>Name: [Generated]</p>
            <p>Status: Approved for Mars 2080</p>
        </div>
        <div class="golden-ticket" id="golden-ticket">
            <h3>Golden Ticket Upgrade!</h3>
            <p>Congrats, you’re a VIP Mars Explorer!</p>
        </div>
    </div>
    <div class="section" id="contact">
        <h2>Contact Us</h2>
        <p>Email: info@mtolympusmons.com</p>
    </div>
    <footer>
        <p>&copy; 2025 Mt Olympus Mons. All tickets are novelty items for entertainment only. No real travel provided.</p>
    </footer>
    <script>
        // 3D Explorer with Three.js
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true });
        renderer.setSize(window.innerWidth, 700);
        document.getElementById('explorer-container').appendChild(renderer.domElement);

        const geometry = new THREE.SphereGeometry(5, 32, 32);
        const material = new THREE.MeshPhongMaterial({ color: 0xC1440E, shininess: 100 });
        const sphere = new THREE.Mesh(geometry, material);
        scene.add(sphere);

        const light = new THREE.PointLight(0xFFFFFF, 1, 100);
        light.position.set(10, 10, 10);
        scene.add(light);

        camera.position.z = 10;
        function animate() {
            requestAnimationFrame(animate);
            sphere.rotation.y += 0.01;
            renderer.render(scene, camera);
        }
        animate();
        window.addEventListener('resize', () => {
            renderer.setSize(window.innerWidth, 700);
            camera.aspect = window.innerWidth / 700;
            camera.updateProjectionMatrix();
        });

        // Booking Function (Simulated)
        function bookTicket() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const year = document.getElementById('year').value;
            const package = document.getElementById('package').value;

            if (!name || !email || !year || !package) {
                alert('Please fill all fields!');
                return;
            }

            // Simulated Payment (Replace with Stripe/PayPal)
            alert(`Processing $5 payment for ${name}... Success!`);
            generateTicket(name, email, year, package);
        }

        function generateTicket(name, email, year, package) {
            const flightNumber = `MTO-${Math.floor(Math.random() * 10000).toString().padStart(4, '0')}`;
            const ticketContent = `
                <div style="font-family: Arial; padding: 20px; background: url('https://via.placeholder.com/800x600?text=Mars+Background'); color: #F6F7F9;">
                    <h1 style="color: #C1440E;">Mt Olympus Mons Boarding Pass</h1>
                    <p>Traveler: ${name}</p>
                    <p>Departure: ${year}</p>
                    <p>Flight: ${flightNumber}</p>
                    <p>Boarding Gate: Launch Pad 39A, Cape Canaveral</p>
                    <p>Package: ${package}</p>
                    <p style="font-size: 0.7em; color: #8FBCE6;">This is a novelty item for entertainment only. No real travel provided.</p>
                </div>
            `;
            const blob = new Blob([ticketContent], { type: 'application/pdf' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `${name}_Mars_Ticket.pdf`;
            a.click();
            URL.revokeObjectURL(url);

            // Simulated Email
            alert(`Thank you, ${name}! Your novelty boarding pass is downloaded. You’re booked for a once-in-a-lifetime adventure… someday. 😉`);

            // Mars Passport
            document.getElementById('passport').innerHTML = `
                <h3>Mars Passport</h3>
                <p>Name: ${name}</p>
                <p>Status: Approved for Mars ${year}</p>
            `;
            document.getElementById('passport').style.display = 'block';

            // Golden Ticket (1% chance)
            if (Math.random() < 0.01) {
                document.getElementById('golden-ticket').style.display = 'block';
                alert('Congrats! You’ve won a Golden Ticket Upgrade!');
            }
        }

        // Navigation
        document.querySelectorAll('nav a').forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                document.querySelector(link.getAttribute('href')).scrollIntoView({ behavior: 'smooth' });
            });
        });
    </script>
</body>
</html>
