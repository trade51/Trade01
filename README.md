<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SAM Events & Production - Premium Casting Portal</title>
    <style>
        :root {
            --gold: #d4af37;
            --dark-gold: #aa7c11;
            --bg-dark: #0f0f0f;
            --card-bg: #181818;
            --text-light: #f5f5f5;
            --text-muted: #aaaaaa;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        /* 1. Animated Welcome Screen */
        #welcomeOverlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            animation: fadeOut 1.5s ease 2.5s forwards;
        }

        .welcome-logo {
            font-size: 28px;
            color: var(--gold);
            letter-spacing: 4px;
            font-weight: bold;
            text-align: center;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 1s ease 0.5s forwards;
        }

        .welcome-sub {
            color: var(--text-muted);
            font-size: 14px;
            text-transform: uppercase;
            margin-top: 10px;
            letter-spacing: 2px;
            opacity: 0;
            animation: fadeInUp 1s ease 1s forwards;
        }

        .welcome-spinner {
            margin-top: 30px;
            width: 40px;
            height: 40px;
            border: 3px solid #222;
            border-top: 3px solid var(--gold);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes fadeInUp {
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeOut {
            to { opacity: 0; visibility: hidden; }
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Container Styling */
        .container {
            background: var(--card-bg);
            border: 1px solid rgba(212, 175, 55, 0.3);
            border-radius: 16px;
            padding: 35px;
            width: 100%;
            max-width: 650px;
            box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.5);
            transition: all 0.3s ease;
        }

        .logo-area {
            text-align: center;
            margin-bottom: 25px;
            user-select: none;
        }

        .logo-area h2 {
            color: var(--gold);
            font-size: 26px;
            letter-spacing: 2px;
            font-weight: 800;
        }

        .logo-area p {
            color: var(--text-muted);
            font-size: 11px;
            text-transform: uppercase;
            margin-top: 5px;
            letter-spacing: 3px;
        }

        h3 {
            text-align: center;
            color: #fff;
            font-size: 20px;
            margin-bottom: 8px;
        }

        .subtitle {
            text-align: center;
            color: var(--text-muted);
            font-size: 13px;
            margin-bottom: 30px;
        }

        /* Form Styling */
        .input-group {
            margin-bottom: 20px;
        }

        .input-row {
            display: flex;
            gap: 15px;
        }

        .input-row .input-group {
            flex: 1;
        }

        label {
            display: block;
            color: var(--gold);
            font-size: 13px;
            margin-bottom: 8px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        input[type="text"],
        input[type="number"],
        input[type="tel"],
        select,
        input[type="file"] {
            width: 100%;
            padding: 14px;
            background: #222;
            border: 1px solid #333;
            border-radius: 8px;
            color: #fff;
            font-size: 15px;
            transition: all 0.3s ease;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--gold);
            background: #2a2a2a;
            box-shadow: 0 0 8px rgba(212, 175, 55, 0.2);
        }

        .submit-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, var(--gold), var(--dark-gold));
            border: none;
            border-radius: 8px;
            color: #000;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.5);
        }

        /* 2. Interactive Receipt Slip */
        .receipt-card {
            background: #fff;
            color: #000;
            border-radius: 12px;
            padding: 25px;
            margin-top: 20px;
            border: 2px dashed #ccc;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .receipt-header {
            text-align: center;
            border-bottom: 2px dashed #000;
            padding-bottom: 15px;
            margin-bottom: 15px;
        }

        .receipt-header h4 {
            font-size: 18px;
            letter-spacing: 1px;
        }

        .receipt-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-size: 14px;
        }

        .receipt-row strong {
            color: #333;
        }

        .receipt-photo {
            width: 80px;
            height: 80px;
            object-fit: cover;
            border-radius: 6px;
            border: 2px solid #000;
            display: block;
            margin: 10px auto;
        }

        .save-receipt-btn {
            background: #000;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            width: 100%;
            margin-top: 15px;
            font-weight: bold;
            cursor: pointer;
        }

        /* 3. Fake Live Notifications */
        .notif-box {
            position: fixed;
            bottom: 20px;
            left: -320px;
            width: 300px;
            background: rgba(24, 24, 24, 0.95);
            border-left: 4px solid var(--gold);
            padding: 15px;
            border-radius: 0 8px 8px 0;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            transition: left 0.5s ease;
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .notif-box.show {
            left: 0;
        }

        .notif-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #333;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--gold);
            font-weight: bold;
        }

        .notif-text {
            font-size: 13px;
            color: #fff;
        }

        .notif-text span {
            color: var(--gold);
            font-weight: bold;
        }

        /* Admin Section Styling */
        .hidden {
            display: none !important;
        }

        /* Tab Controls */
        .tab-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .tab-btn {
            flex: 1;
            padding: 10px;
            background: #222;
            border: 1px solid #333;
            color: #fff;
            font-weight: bold;
            cursor: pointer;
            border-radius: 6px;
            transition: all 0.3s;
        }

        .tab-btn.active {
            background: var(--gold);
            color: #000;
            border-color: var(--gold);
        }

        /* Filters */
        .filter-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .filter-controls input, .filter-controls select {
            padding: 10px;
            background: #222;
            border: 1px solid #333;
            color: #fff;
            border-radius: 6px;
            font-size: 14px;
            flex: 1;
        }

        /* Responsive Table */
        .table-wrapper {
            overflow-x: auto;
            margin-top: 15px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            color: #fff;
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #222;
            white-space: nowrap; /* Prevents text breaking weirdly */
        }

        th {
            background-color: #1f1f1f;
            color: var(--gold);
            font-size: 14px;
            text-transform: uppercase;
        }

        /* FIXED: Ensuring Name & Age are highly visible and properly styled */
        td.cand-name {
            font-weight: bold;
            color: #ffffff;
            font-size: 15px;
        }

        td.cand-age {
            font-weight: 600;
            color: #e0e0e0;
        }

        .preview-img {
            width: 50px;
            height: 50px;
            object-fit: cover;
            border-radius: 8px;
            border: 1px solid var(--gold);
        }

        .badge {
            background: rgba(212, 175, 55, 0.15);
            color: var(--gold);
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            text-transform: uppercase;
            font-weight: bold;
            border: 1px solid var(--gold);
        }

        /* Action Buttons */
        .action-btns {
            display: flex;
            gap: 8px;
        }

        .wa-btn {
            background: #25D366;
            color: white;
            padding: 6px 12px;
            text-decoration: none;
            border-radius: 6px;
            font-size: 12px;
            font-weight: bold;
        }

        .shortlist-btn {
            background: var(--gold);
            color: #000;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: bold;
            cursor: pointer;
        }

        .delete-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: bold;
            cursor: pointer;
        }

        .toggle-btn {
            background: transparent;
            border: 1px solid var(--gold);
            color: var(--gold);
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            display: block;
            margin: 25px auto 0 auto;
            transition: all 0.3s;
        }

        .toggle-btn:hover {
            background: var(--gold);
            color: #000;
        }
    </style>

    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
</head>
<body>

    <div id="welcomeOverlay">
        <div class="welcome-logo">SAM EVENTS & PRODUCTION</div>
        <div class="welcome-sub">Portal is Loading...</div>
        <div class="welcome-spinner"></div>
    </div>

    <div class="notif-box" id="notifBox">
        <div class="notif-avatar" id="notifAvatar">A</div>
        <div class="notif-text" id="notifText"></div>
    </div>

    <div class="container" id="formSection">
        <div class="logo-area" onclick="handleLogoTap()">
            <h2>SAM EVENTS & PRODUCTION</h2>
            <p>Committed With Quality</p>
        </div>
        
        <h3>Casting Registration</h3>
        <p class="subtitle">Fill out your profile accurately</p>

        <form id="castingForm">
            <div class="input-group">
                <label for="fullName">Full Name</label>
                <input type="text" id="fullName" placeholder="Enter full name" required>
            </div>

            <div class="input-row">
                <div class="input-group">
                    <label for="age">Age</label>
                    <input type="number" id="age" placeholder="Age" required>
                </div>
                <div class="input-group">
                    <label for="category">Category</label>
                    <select id="category" required>
                        <option value="" disabled selected>Select Category</option>
                        <option value="girls">Girl</option>
                        <option value="boys">Boy</option>
                        <option value="children">Child</option>
                        <option value="uncles">Uncle</option>
                        <option value="aunties">Auntie</option>
                    </select>
                </div>
            </div>

            <div class="input-group">
                <label for="phone">WhatsApp Number</label>
                <input type="tel" id="phone" placeholder="e.g. 03175052697" required>
            </div>

            <div class="input-group">
                <label for="photo">Upload Photo (Will be compressed)</label>
                <input type="file" id="photo" accept="image/*" required>
            </div>

            <button type="submit" class="submit-btn" id="submitBtn">Submit Application</button>
        </form>

        <div id="receiptArea" class="hidden">
            <div class="receipt-card" id="printableReceipt">
                <div class="receipt-header">
                    <h4>SAM EVENTS & PRODUCTION</h4>
                    <p style="font-size: 11px;">Official Registration Slip</p>
                </div>
                <img id="receiptImg" class="receipt-photo" src="" alt="Candidate">
                <div class="receipt-row"><strong>Registration ID:</strong> <span id="rId"></span></div>
                <div class="receipt-row"><strong>Name:</strong> <span id="rName"></span></div>
                <div class="receipt-row"><strong>Age:</strong> <span id="rAge"></span></div>
                <div class="receipt-row"><strong>Category:</strong> <span id="rCategory"></span></div>
                <div class="receipt-row"><strong>WhatsApp:</strong> <span id="rPhone"></span></div>
                <div class="receipt-row"><strong>Status:</strong> <span style="color: green; font-weight: bold;">PENDING REVIEW</span></div>
            </div>
            <button class="save-receipt-btn" onclick="printReceipt()">Save / Print Receipt</button>
        </div>
    </div>

    <div class="container hidden" id="adminSection">
        <div class="logo-area">
            <h2>SAM EVENTS - EAGLE EYE</h2>
            <p>Admin Control Panel</p>
        </div>

        <div class="tab-controls">
            <button class="tab-btn active" id="btnAllTab" onclick="switchTab('all')">All Applications</button>
            <button class="tab-btn" id="btnShortlistTab" onclick="switchTab('shortlisted')">Shortlisted</button>
        </div>

        <div class="filter-controls">
            <input type="text" id="searchName" placeholder="Search by name..." oninput="filterData()">
            <select id="filterCategory" onchange="filterData()">
                <option value="all">All Categories</option>
                <option value="girls">Girls</option>
                <option value="boys">Boys</option>
                <option value="children">Children</option>
                <option value="uncles">Uncles</option>
                <option value="aunties">Aunties</option>
            </select>
        </div>
        
        <div class="table-wrapper">
            <table>
                <thead>
                    <tr>
                        <th>Photo</th>
                        <th>Name</th>
                        <th>Age</th>
                        <th>Category</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="adminTableBody">
                    <tr><td colspan="5" style="text-align: center; color: #888;">Connecting Realtime Database...</td></tr>
                </tbody>
            </table>
        </div>

        <button class="toggle-btn" onclick="toggleView('form')">Exit Admin Panel</button>
    </div>

    <script>
        // 1. Firebase Initialization
        const firebaseConfig = {
            apiKey: "AIzaSyBqtvNJW_HNv4H2EAzeAhNL-tiUjX1huEg",
            authDomain: "trade51-f64d5.firebaseapp.com",
            databaseURL: "https://trade51-f64d5-default-rtdb.firebaseio.com",
            projectId: "trade51-f64d5",
            storageBucket: "trade51-f64d5.firebasestorage.app",
            messagingSenderId: "38759095579",
            appId: "1:38759095579:web:013d72ab4b5183f99347be"
        };

        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();
        
        let allSubmissions = {}; 
        let currentTab = 'all'; // 'all' or 'shortlisted'
        let logoTapCount = 0;

        // 2. Eagle Eye Hidden Activation Logic (Tap 5 Times)
        function handleLogoTap() {
            logoTapCount++;
            if (logoTapCount === 5) {
                logoTapCount = 0; // Reset
                const password = prompt("Eagle Eye Secret Verification Key enter karein, sweetie:");
                if (password === "eagleeye51") {
                    toggleView('admin');
                } else if (password !== null) {
                    alert("Unauthorized access attempt locked!");
                }
            }
        }

        // 3. Compressing and Converting Image to Base64
        function compressAndConvertToBase64(file, callback) {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = function (event) {
                const img = new Image();
                img.src = event.target.result;
                img.onload = function () {
                    const canvas = document.createElement('canvas');
                    const ctx = canvas.getContext('2d');
                    
                    // Set maximum preview dimensions
                    const MAX_WIDTH = 250;
                    const scaleSize = MAX_WIDTH / img.width;
                    canvas.width = MAX_WIDTH;
                    canvas.height = img.height * scaleSize;

                    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                    
                    // Compression to JPEG with 0.6 quality (Super lightweight Firebase load!)
                    const dataUrl = canvas.toDataURL('image/jpeg', 0.6);
                    callback(dataUrl);
                }
            }
        }

        // 4. Form Submission & Custom Receipt Slip Generation
        document.getElementById('castingForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const submitBtn = document.getElementById('submitBtn');
            submitBtn.innerText = "Processing Profile...";
            submitBtn.disabled = true;

            const fullName = document.getElementById('fullName').value;
            const age = document.getElementById('age').value;
            const category = document.getElementById('category').value;
            const phone = document.getElementById('phone').value;
            const photoInput = document.getElementById('photo');

            if (photoInput.files.length > 0) {
                compressAndConvertToBase64(photoInput.files[0], function(compressedBase64) {
                    const newKey = database.ref('auditions').push().key;
                    const postData = {
                        id: newKey,
                        name: fullName,
                        age: age,
                        category: category,
                        phone: phone,
                        photo: compressedBase64,
                        shortlisted: false
                    };

                    database.ref('auditions/' + newKey).set(postData).then(() => {
                        // Display customized slip
                        document.getElementById('rId').innerText = newKey.substring(1, 8).toUpperCase();
                        document.getElementById('rName').innerText = fullName;
                        document.getElementById('rAge').innerText = age;
                        document.getElementById('rCategory').innerText = category.toUpperCase();
                        document.getElementById('rPhone').innerText = phone;
                        document.getElementById('receiptImg').src = compressedBase64;

                        document.getElementById('receiptArea').classList.remove('hidden');
                        document.getElementById('castingForm').reset();
                        submitBtn.innerText = "Submit Application";
                        submitBtn.disabled = false;
                        alert("Application Submitted successfully, sweetie! Please save your receipt.");
                    }).catch(err => {
                        alert("Firebase Error: " + err.message);
                        submitBtn.innerText = "Submit Application";
                        submitBtn.disabled = false;
                    });
                });
            }
        });

        // 5. Print/Save Receipt Feature
        function printReceipt() {
            const printContent = document.getElementById('printableReceipt').innerHTML;
            const originalContent = document.body.innerHTML;
            document.body.innerHTML = printContent;
            window.print();
            document.body.innerHTML = originalContent;
            window.location.reload(); // Quick reset after printing
        }

        // 6. View Switching
        function toggleView(view) {
            if (view === 'admin') {
                document.getElementById('formSection').classList.add('hidden');
                document.getElementById('adminSection').classList.remove('hidden');
                listenToSubmissions();
            } else {
                document.getElementById('adminSection').classList.add('hidden');
                document.getElementById('formSection').classList.remove('hidden');
            }
        }

        function switchTab(tab) {
            currentTab = tab;
            document.getElementById('btnAllTab').classList.toggle('active', tab === 'all');
            document.getElementById('btnShortlistTab').classList.toggle('active', tab === 'shortlisted');
            filterData();
        }

        // 7. Read Firebase Realtime
        function listenToSubmissions() {
            database.ref('auditions').on('value', (snapshot) => {
                allSubmissions = snapshot.val() || {};
                filterData();
            });
        }

        // 8. Delete Application Action
        function deleteCandidate(id) {
            if(confirm("Kya aap waqayi is candidate ka data delete karna chahte hain, sweetie?")) {
                database.ref('auditions/' + id).remove().then(() => {
                    alert("Candidate profile successfully deleted!");
                });
            }
        }

        // 9. Shortlist/Un-shortlist Action
        function toggleShortlist(id, currentStatus) {
            database.ref('auditions/' + id).update({
                shortlisted: !currentStatus
            });
        }

        // 10. Filter & Search Render Logic
        function filterData() {
            const searchValue = document.getElementById('searchName').value.toLowerCase();
            const categoryValue = document.getElementById('filterCategory').value;
            const tableBody = document.getElementById('adminTableBody');
            tableBody.innerHTML = '';

            const list = Object.values(allSubmissions);

            const filtered = list.filter(item => {
                const matchesName = item.name.toLowerCase().includes(searchValue);
                const matchesCategory = (categoryValue === 'all') || (item.category === categoryValue);
                const matchesTab = (currentTab === 'all') || (currentTab === 'shortlisted' && item.shortlisted === true);
                return matchesName && matchesCategory && matchesTab;
            });

            if (filtered.length === 0) {
                tableBody.innerHTML = `<tr><td colspan="5" style="text-align: center; color: #888;">No profiles match this query, sweetie!</td></tr>`;
                return;
            }

            filtered.forEach(item => {
                const row = document.createElement('tr');
                const msg = encodeURIComponent(`Hi ${item.name}! SAM Events & Production here. We have shortlisted your profile for upcoming audits. Kindly contact us.`);
                const waLink = `https://wa.me/${item.phone}?text=${msg}`;

                row.innerHTML = `
                    <td><img src="${item.photo}" class="preview-img" alt="Photo"></td>
                    <td class="cand-name">${item.name}</td>
                    <td class="cand-age">${item.age} Years</td>
                    <td><span class="badge">${item.category}</span></td>
                    <td>
                        <div class="action-btns">
                            <a href="${waLink}" target="_blank" class="wa-btn">WhatsApp</a>
                            <button class="shortlist-btn" onclick="toggleShortlist('${item.id}', ${item.shortlisted})">
                                ${item.shortlisted ? 'Unlist' : 'Shortlist'}
                            </button>
                            <button class="delete-btn" onclick="deleteCandidate('${item.id}')">Delete</button>
                        </div>
                    </td>
                `;
                tableBody.appendChild(row);
            });
        }

        // 11. 20+ Fake Notifications Loop
        const fakeNames = ["Ayesha", "Zain", "Fatima", "Hamza", "Ali", "Maryum", "Bilal", "Sana", "Usman", "Amna", "Hassan", "Rida", "Saad", "Laiba", "Ahmad", "Tayyaba", "Daniyal", "Aqsa", "Arsalan", "Hira", "Junaid"];
        const fakeCities = ["Islamabad", "Rawalpindi", "Lahore", "Karachi", "Peshawar", "Faisalabad", "Multan", "Quetta", "Gilgit", "Sialkot"];

        function showFakeNotification() {
            const notifBox = document.getElementById('notifBox');
            const notifAvatar = document.getElementById('notifAvatar');
            const notifText = document.getElementById('notifText');

            const randomName = fakeNames[Math.floor(Math.random() * fakeNames.length)];
            const randomCity = fakeCities[Math.floor(Math.random() * fakeCities.length)];

            notifAvatar.innerText = randomName[0];
            notifText.innerHTML = `<span>${randomName}</span> from ${randomCity} just registered!`;

            notifBox.classList.add('show');

            setTimeout(() => {
                notifBox.classList.remove('show');
            }, 4000);
        }

        // Run fake notifications every 10-15 seconds
        setInterval(showFakeNotification, 12000);
        setTimeout(showFakeNotification, 5000); // First load notification
    </script>
</body>
</html>
