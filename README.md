- 👋 Hi, I’m @yazir00-ux
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
yazir00-ux/yazir00-ux is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-Time Chat Platform</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css">
    
    <!-- Custom CSS -->
    <style>
        :root {
            --primary-color: #4a6bff;
            --secondary-color: #f8f9fa;
            --text-color: #333;
            --border-color: #dee2e6;
            --success-color: #28a745;
            --error-color: #dc3545;
            --dark-bg: #2c3e50;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: var(--text-color);
            background-color: #f5f7fb;
            height: 100vh;
            overflow: hidden;
        }
        
        .auth-container {
            max-width: 400px;
            margin: 0 auto;
            padding: 2rem;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
        }
        
        .auth-tabs .nav-link {
            color: var(--text-color);
            font-weight: 500;
        }
        
        .auth-tabs .nav-link.active {
            color: var(--primary-color);
            border-bottom: 2px solid var(--primary-color);
        }
        
        .main-container {
            height: 100vh;
            display: none;
        }
        
        .sidebar {
            height: 100%;
            border-right: 1px solid var(--border-color);
            background-color: white;
        }
        
        .contact-list {
            overflow-y: auto;
            height: calc(100% - 60px);
        }
        
        .contact-item {
            cursor: pointer;
            transition: background-color 0.2s;
            border-bottom: 1px solid var(--border-color);
            padding: 12px 15px;
        }
        
        .contact-item:hover {
            background-color: var(--secondary-color);
        }
        
        .contact-item.active {
            background-color: rgba(74, 107, 255, 0.1);
            border-left: 3px solid var(--primary-color);
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            object-fit: cover;
        }
        
        .chat-container {
            display: flex;
            flex-direction: column;
            height: 100%;
            background-color: white;
        }
        
        .chat-header {
            padding: 15px;
            border-bottom: 1px solid var(--border-color);
            background-color: white;
        }
        
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background-color: #f5f7fb;
        }
        
        .message {
            margin-bottom: 15px;
            max-width: 70%;
        }
        
        .message-sent {
            align-self: flex-end;
            margin-left: auto;
        }
        
        .message-received {
            align-self: flex-start;
        }
        
        .message-content {
            padding: 10px 15px;
            border-radius: 18px;
            position: relative;
        }
        
        .message-sent .message-content {
            background-color: var(--primary-color);
            color: white;
            border-bottom-right-radius: 5px;
        }
        
        .message-received .message-content {
            background-color: #e9ecef;
            color: var(--text-color);
            border-bottom-left-radius: 5px;
        }
        
        .message-time {
            font-size: 12px;
            margin-top: 5px;
            color: #6c757d;
        }
        
        .chat-input {
            padding: 15px;
            border-top: 1px solid var(--border-color);
            background-color: white;
        }
        
        .input-message {
            border-radius: 20px;
            resize: none;
            padding: 10px 15px;
        }
        
        .btn-send {
            border-radius: 50%;
            width: 40px;
            height: 40px;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--primary-color);
            border: none;
        }
        
        .btn-send:hover {
            background-color: #3955cc;
        }
        
        .btn-video {
            background-color: #28a745;
            border: none;
            color: white;
        }
        
        .btn-video:hover {
            background-color: #218838;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1050;
            min-width: 250px;
        }
        
        .online-indicator {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background-color: var(--success-color);
            display: inline-block;
            margin-right: 5px;
        }
        
        .offline-indicator {
            background-color: #6c757d;
        }
        
        .typing-indicator {
            display: none;
            font-style: italic;
            color: #6c757d;
            margin-bottom: 10px;
        }
        
        .loading-spinner {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .search-container {
            padding: 15px;
            border-bottom: 1px solid var(--border-color);
        }
        
        .search-input {
            border-radius: 20px;
            padding-left: 35px;
        }
        
        .search-icon {
            position: absolute;
            left: 25px;
            top: 12px;
            color: #6c757d;
        }
        
        @media (max-width: 767px) {
            .sidebar {
                position: fixed;
                z-index: 999;
                width: 80%;
                left: -100%;
                transition: left 0.3s ease;
            }
            
            .sidebar.show {
                left: 0;
            }
            
            .message {
                max-width: 90%;
            }
        }
        
        /* Video call container */
        .video-container {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.9);
            z-index: 1100;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .video-interface {
            width: 100%;
            max-width: 1000px;
            height: 80vh;
            background-color: #000;
            border-radius: 10px;
            overflow: hidden;
            position: relative;
        }
        
        .video-controls {
            position: absolute;
            bottom: 20px;
            left: 0;
            right: 0;
            text-align: center;
        }
        
        .video-controls .btn {
            margin: 0 10px;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }
        
        .btn-end-call {
            background-color: var(--error-color);
            border-color: var(--error-color);
        }
    </style>
</head>
<body>
    <!-- Authentication Container -->
    <div class="auth-container mt-5" id="auth-container">
        <h2 class="text-center mb-4">Welcome to ChatConnect</h2>
        
        <ul class="nav nav-tabs auth-tabs mb-4" id="auth-tabs">
            <li class="nav-item flex-fill text-center">
                <a class="nav-link active" id="login-tab" data-bs-toggle="tab" href="#login">Login</a>
            </li>
            <li class="nav-item flex-fill text-center">
                <a class="nav-link" id="register-tab" data-bs-toggle="tab" href="#register">Register</a>
            </li>
        </ul>
        
        <div class="tab-content">
            <!-- Login Form -->
            <div class="tab-pane fade show active" id="login">
                <form id="login-form">
                    <div class="mb-3">
                        <label for="login-email" class="form-label">Email address</label>
                        <input type="email" class="form-control" id="login-email" required>
                    </div>
                    <div class="mb-3">
                        <label for="login-password" class="form-label">Password</label>
                        <input type="password" class="form-control" id="login-password" required>
                    </div>
                    <div class="mb-3 form-check">
                        <input type="checkbox" class="form-check-input" id="remember-me">
                        <label class="form-check-label" for="remember-me">Remember me</label>
                    </div>
                    <button type="submit" class="btn btn-primary w-100">Login</button>
                </form>
            </div>
            
            <!-- Register Form -->
            <div class="tab-pane fade" id="register">
                <form id="register-form">
                    <div class="mb-3">
                        <label for="register-name" class="form-label">Full Name</label>
                        <input type="text" class="form-control" id="register-name" required>
                    </div>
                    <div class="mb-3">
                        <label for="register-email" class="form-label">Email address</label>
                        <input type="email" class="form-control" id="register-email" required>
                    </div>
                    <div class="mb-3">
                        <label for="register-password" class="form-label">Password</label>
                        <input type="password" class="form-control" id="register-password" required>
                        <div class="form-text">Password must be at least 8 characters long.</div>
                    </div>
                    <div class="mb-3">
                        <label for="confirm-password" class="form-label">Confirm Password</label>
                        <input type="password" class="form-control" id="confirm-password" required>
                    </div>
                    <button type="submit" class="btn btn-primary w-100">Register</button>
                </form>
            </div>
        </div>
    </div>
    
    <!-- Main Chat Container -->
    <div class="main-container container-fluid" id="main-container">
        <div class="row h-100">
            <!-- Sidebar with Contacts -->
            <div class="col-md-4 col-lg-3 p-0 sidebar" id="sidebar">
                <div class="d-flex justify-content-between align-items-center p-3 border-bottom">
                    <div class="d-flex align-items-center">
                        <img src="https://via.placeholder.com/40" alt="Your Avatar" class="user-avatar me-2">
                        <div>
                            <h6 class="mb-0" id="user-name">John Doe</h6>
                            <small><span class="online-indicator"></span> Online</small>
                        </div>
                    </div>
                    <div class="d-md-none">
                        <button class="btn btn-sm btn-light" id="close-sidebar">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                </div>
                
                <div class="search-container position-relative">
                    <i class="fas fa-search search-icon"></i>
                    <input type="text" class="form-control search-input" placeholder="Search contacts...">
                </div>
                
                <div class="contact-list">
                    <!-- Contact items will be dynamically populated -->
                    <div class="contact-item active">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/2c3e50/ffffff?text=MS" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Marketing Squad</h6>
                                <small class="text-muted">Group Chat · 5 members</small>
                            </div>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Jane Smith</h6>
                                <small class="text-muted"><span class="online-indicator"></span> Let's review the designs</small>
                            </div>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/e74c3c/ffffff?text=MB" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Mike Brown</h6>
                                <small class="text-muted"><span class="online-indicator offline-indicator"></span> I'll check and get back to you</small>
                            </div>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/9b59b6/ffffff?text=AT" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Alex Turner</h6>
                                <small class="text-muted"><span class="online-indicator"></span> Thanks for the update!</small>
                            </div>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/f1c40f/ffffff?text=SW" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Sarah Wilson</h6>
                                <small class="text-muted"><span class="online-indicator offline-indicator"></span> Let's schedule a call tomorrow</small>
                            </div>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="d-flex align-items-center">
                            <img src="https://via.placeholder.com/40/27ae60/ffffff?text=DT" alt="Contact Avatar" class="user-avatar me-3">
                            <div>
                                <h6 class="mb-0">Dev Team</h6>
                                <small class="text-muted">Group Chat · 8 members</small>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Chat Area -->
            <div class="col-md-8 col-lg-9 p-0">
                <div class="chat-container">
                    <!-- Chat Header -->
                    <div class="chat-header d-flex justify-content-between align-items-center">
                        <div class="d-flex align-items-center">
                            <button class="btn btn-sm btn-light d-md-none me-2" id="show-sidebar">
                                <i class="fas fa-bars"></i>
                            </button>
                            <img src="https://via.placeholder.com/40/2c3e50/ffffff?text=MS" alt="Group Avatar" class="user-avatar me-2">
                            <div>
                                <h5 class="mb-0">Marketing Squad</h5>
                                <small><span class="online-indicator"></span> 3 members online</small>
                            </div>
                        </div>
                        <div>
                            <button class="btn btn-sm btn-video" id="start-video-call">
                                <i class="fas fa-video"></i> Video Call
                            </button>
                        </div>
                    </div>
                    
                    <!-- Chat Messages -->
                    <div class="chat-messages" id="chat-messages">
                        <div class="text-center text-muted mb-4">
                            <small>Today, 12:45 PM</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Hey team, how's the progress on the new landing page?
                                    </div>
                                    <div class="message-time">12:45 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/e74c3c/ffffff?text=MB" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Mike Brown</small>
                                    <div class="message-content">
                                        Almost done with the hero section, just need to optimize some images.
                                    </div>
                                    <div class="message-time">12:47 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                I've completed the copy revisions and sent them over to Mike for integration.
                            </div>
                            <div class="message-time">12:49 PM</div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Great! Let's aim to finalize everything by EOD. The client demo is scheduled for tomorrow morning.
                                    </div>
                                    <div class="message-time">12:51 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/f1c40f/ffffff?text=SW" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Sarah Wilson</small>
                                    <div class="message-content">
                                        I'll handle the final QA. Also, has anyone reviewed the SEO meta tags?
                                    </div>
                                    <div class="message-time">12:53 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                I did! All meta tags are ready and optimized as per the requirements.
                            </div>
                            <div class="message-time">12:55 PM</div>
                        </div>
                        
                        <div class="typing-indicator" id="typing-indicator">
                            Someone is typing...
                        </div>
                        
                        <div class="loading-spinner" id="loading-spinner">
                            <div class="spinner-border text-primary" role="status">
                                <span class="visually-hidden">Loading...</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Chat Input -->
                    <div class="chat-input">
                        <form id="message-form">
                            <div class="d-flex align-items-center">
                                <textarea class="form-control input-message me-2" id="message-input" placeholder="Type a message..." rows="1"></textarea>
                                <button type="submit" class="btn btn-send">
                                    <i class="fas fa-paper-plane text-white"></i>
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Video Call Container -->
    <div class="video-container" id="video-container">
        <div class="video-interface">
            <div class="d-flex h-100 justify-content-center align-items-center text-white">
                <div class="text-center">
                    <div class="spinner-border mb-3" role="status">
                        <span class="visually-hidden">Loading...</span>
                    </div>
                    <h4>Initializing video call...</h4>
                    <p>Connecting to the Marketing Squad</p>
                </div>
            </div>
            <div class="video-controls">
                <button class="btn btn-light" id="mute-video">
                    <i class="fas fa-video"></i>
                </button>
                <button class="btn btn-light" id="mute-audio">
                    <i class="fas fa-microphone"></i>
                </button>
                <button class="btn btn-end-call" id="end-call">
                    <i class="fas fa-phone-slash"></i>
                </button>
            </div>
        </div>
    </div>
    
    <!-- Notification Template -->
    <div class="toast-container position-fixed top-0 end-0 p-3">
        <div class="toast align-items-center text-white bg-success border-0" id="notification" role="alert" aria-live="assertive" aria-atomic="true">
            <div class="d-flex">
                <div class="toast-body" id="notification-message">
                    Message sent successfully!
                </div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
            </div>
        </div>
    </div>
    
    <!-- Bootstrap, jQuery, and Popper.js -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
    
    <!-- Main Script -->
    <script>
        $(document).ready(function() {
            // Login form submission remains a simulated auth process for this demo.
            $('#login-form').on('submit', function(e) {
                e.preventDefault();
                const email = $('#login-email').val();
                const password = $('#login-password').val();
                
                // Show loading state
                $('#loading-spinner').show();
                
                // Simulate authentication delay
                setTimeout(function() {
                    $('#loading-spinner').hide();
                    
                    if (email && password) {
                        // Success case: Hide auth container, show main
                        $('#auth-container').hide();
                        $('#main-container').show();
                        
                        // Set user name
                        $('#user-name').text(email.split('@')[0]);
                        
                        // Show notification
                        showNotification('Login successful!', 'success');
                    } else {
                        // Error case
                        showNotification('Invalid email or password!', 'danger');
                    }
                }, 1000);
            });
            
            // Register form submission using UserAPI Magic Loop
            $('#register-form').on('submit', async function(e) {
                e.preventDefault();
                const name = $('#register-name').val();
                const email = $('#register-email').val();
                const password = $('#register-password').val();
                const confirmPassword = $('#confirm-password').val();
                
                // Show loading state
                $('#loading-spinner').show();
                
                if (password !== confirmPassword) {
                    $('#loading-spinner').hide();
                    showNotification('Passwords do not match!', 'danger');
                    return;
                }
                
                if (!name || !email || !password || password.length < 8) {
                    $('#loading-spinner').hide();
                    showNotification('Please fill all fields correctly!', 'danger');
                    return;
                }
                
                // Construct payload for UserAPI Loop
                const payload = {
                    action: "register",
                    userDetails: {
                        username: email.split('@')[0],
                        password: password,
                        profile: {
                            fullName: name,
                            email: email
                        }
                    }
                };
                
                try {
                    const response = await fetch('https://magicloops.dev/api/loop/b6f4e08e-91ab-4b45-9c42-af6c14b064b4/run', {
                        method: 'POST',
                        body: JSON.stringify(payload),
                        headers: {
                            'Content-Type': 'application/json'
                        }
                    });
                    const result = await response.json();
                    $('#loading-spinner').hide();
                    
                    if (result.status === "success") {
                        showNotification('Registration successful! Please login.', 'success');
                        $('#login-tab').tab('show');
                        $('#login-email').val(email);
                    } else {
                        showNotification('Registration failed. Please try again.', 'danger');
                    }
                } catch (error) {
                    $('#loading-spinner').hide();
                    showNotification('Error during registration.', 'danger');
                }
            });
            
            // Message form submission using ChatAPILoop
            $('#message-form').on('submit', async function(e) {
                e.preventDefault();
                const messageInput = $('#message-input');
                const messageText = messageInput.val().trim();
                
                if (messageText) {
                    // Create sent message element in UI
                    const now = new Date();
                    const timeStr = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
                    
                    const messageHtml = `
                        <div class="message message-sent">
                            <div class="message-content">
                                ${messageText}
                            </div>
                            <div class="message-time">${timeStr}</div>
                        </div>
                    `;
                    
                    $('#chat-messages').append(messageHtml);
                    messageInput.val('');
                    scrollToBottom();
                    
                    // Construct payload for ChatAPILoop
                    const payload = {
                        action: "sendMessage",
                        message: {
                            from: $('#user-name').text(),
                            to: $('.contact-item.active h6').text(),
                            content: messageText,
                            timestamp: (new Date()).toISOString()
                        }
                    };
                    
                    try {
                        const response = await fetch('https://magicloops.dev/api/loop/b4c0dea0-7668-40f2-9068-f41bcbf9d936/run', {
                            method: 'POST',
                            body: JSON.stringify(payload),
                            headers: {
                                'Content-Type': 'application/json'
                            }
                        });
                        const result = await response.json();
                        // Optionally, update the UI with the returned chat history or confirmation from result
                        showNotification('Message sent!', 'success');
                    } catch (error) {
                        showNotification('Failed to send message.', 'danger');
                    }
                    
                    // Simulate response typing indicator and dummy response
                    simulateResponse();
                }
            });
            
            // Sidebar toggle for mobile
            $('#show-sidebar').on('click', function() {
                $('#sidebar').addClass('show');
            });
            
            $('#close-sidebar').on('click', function() {
                $('#sidebar').removeClass('show');
            });
            
            // Contact item click
            $('.contact-item').on('click', function() {
                $('.contact-item').removeClass('active');
                $(this).addClass('active');
                
                const contactName = $(this).find('h6').text();
                const isGroup = $(this).find('small').text().includes('Group');
                
                $('.chat-header h5').text(contactName);
                if (isGroup) {
                    $('.chat-header small').html('<span class="online-indicator"></span> 3 members online');
                } else {
                    $('.chat-header small').html('<span class="online-indicator"></span> Online');
                }
                
                if ($(window).width() < 768) {
                    $('#sidebar').removeClass('show');
                }
                
                $('#chat-messages').html('<div class="loading-spinner" style="display:block;"><div class="spinner-border text-primary" role="status"><span class="visually-hidden">Loading...</span></div></div>');
                setTimeout(function() {
                    loadDummyMessages(contactName);
                }, 800);
            });
            
            // Video call functionality
            $('#start-video-call').on('click', function() {
                $('#video-container').css('display', 'flex');
                setTimeout(function() {
                    showNotification('Video call initiated!', 'info');
                }, 1500);
            });
            
            $('#end-call').on('click', function() {
                $('#video-container').hide();
                showNotification('Call ended', 'info');
            });
            
            $('#mute-video, #mute-audio').on('click', function() {
                $(this).toggleClass('btn-light btn-secondary');
                if ($(this).attr('id') === 'mute-video') {
                    const icon = $(this).find('i');
                    if (icon.hasClass('fa-video')) {
                        icon.removeClass('fa-video').addClass('fa-video-slash');
                    } else {
                        icon.removeClass('fa-video-slash').addClass('fa-video');
                    }
                } else {
                    const icon = $(this).find('i');
                    if (icon.hasClass('fa-microphone')) {
                        icon.removeClass('fa-microphone').addClass('fa-microphone-slash');
                    } else {
                        icon.removeClass('fa-microphone-slash').addClass('fa-microphone');
                    }
                }
            });
            
            $('#message-input').on('input', function() {
                this.style.height = 'auto';
                this.style.height = (this.scrollHeight) + 'px';
                if ($(this).val().trim() !== '') {
                    simulateTyping();
                }
            });
            
            function showNotification(message, type) {
                const notification = $('#notification');
                $('#notification-message').text(message);
                notification.removeClass('bg-success bg-danger bg-info bg-warning')
                    .addClass(`bg-${type}`);
                const toast = new bootstrap.Toast(notification);
                toast.show();
            }
            
            function scrollToBottom() {
                const chatMessages = $('#chat-messages');
                chatMessages.scrollTop(chatMessages[0].scrollHeight);
            }
            
            function simulateResponse() {
                setTimeout(function() {
                    $('#typing-indicator').show();
                    setTimeout(function() {
                        $('#typing-indicator').hide();
                        const responses = [
                            "Sounds good! I'll work on that right away.",
                            "Thanks for the update!",
                            "Got it, I'll add that to my task list.",
                            "Let's discuss this further in our next meeting.",
                            "Can you share more details on this?",
                            "I'll check with the team and get back to you."
                        ];
                        const randomIndex = Math.floor(Math.random() * responses.length);
                        const response = responses[randomIndex];
                        
                        const activeContact = $('.contact-item.active');
                        const contactName = activeContact.find('h6').text();
                        const contactAvatar = activeContact.find('img').attr('src');
                        
                        const now = new Date();
                        const timeStr = now.getHours().toString().padStart(2, '0') + ':' + 
                                         now.getMinutes().toString().padStart(2, '0');
                        
                        const messageHtml = `
                            <div class="message message-received">
                                <div class="d-flex align-items-start">
                                    <img src="${contactAvatar}" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                    <div>
                                        <small class="text-muted">${contactName}</small>
                                        <div class="message-content">
                                            ${response}
                                        </div>
                                        <div class="message-time">${timeStr}</div>
                                    </div>
                                </div>
                            </div>
                        `;
                        
                        $('#chat-messages').append(messageHtml);
                        scrollToBottom();
                        
                    }, 1500);
                }, 1000);
            }
            
            function simulateTyping() {
                clearTimeout(window.typingTimeout);
                window.typingTimeout = setTimeout(function() {
                    $('#typing-indicator').show();
                    setTimeout(function() {
                        $('#typing-indicator').hide();
                    }, 2000);
                }, 500);
            }
            
            function loadDummyMessages(contactName) {
                let messageHtml;
                if (contactName === 'Marketing Squad') {
                    messageHtml = `
                        <div class="text-center text-muted mb-4">
                            <small>Today, 12:45 PM</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Hey team, how's the progress on the new landing page?
                                    </div>
                                    <div class="message-time">12:45 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/e74c3c/ffffff?text=MB" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Mike Brown</small>
                                    <div class="message-content">
                                        Almost done with the hero section, just need to optimize some images.
                                    </div>
                                    <div class="message-time">12:47 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                I've completed the copy revisions and sent them over to Mike for integration.
                            </div>
                            <div class="message-time">12:49 PM</div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Great! Let's aim to finalize everything by EOD. The client demo is scheduled for tomorrow morning.
                                    </div>
                                    <div class="message-time">12:51 PM</div>
                                </div>
                            </div>
                        </div>
                    `;
                } else if (contactName === 'Jane Smith') {
                    messageHtml = `
                        <div class="text-center text-muted mb-4">
                            <small>Today, 10:15 AM</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Hi there! Can we review the design mockups today?
                                    </div>
                                    <div class="message-time">10:15 AM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                Sure! I'm free around 2 PM. Does that work for you?
                            </div>
                            <div class="message-time">10:17 AM</div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        Perfect! I'll send a calendar invite.
                                    </div>
                                    <div class="message-time">10:18 AM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/3498db/ffffff?text=JS" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Jane Smith</small>
                                    <div class="message-content">
                                        By the way, I really liked your approach on the last project. Great work! 👍
                                    </div>
                                    <div class="message-time">10:20 AM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                Thanks, Jane! Looking forward to our meeting.
                            </div>
                            <div class="message-time">10:22 AM</div>
                        </div>
                    `;
                } else if (contactName === 'Dev Team') {
                    messageHtml = `
                        <div class="text-center text-muted mb-4">
                            <small>Yesterday, 4:30 PM</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/27ae60/ffffff?text=DT" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Alex (Team Lead)</small>
                                    <div class="message-content">
                                        Sprint planning tomorrow at 10 AM. Please update your current tasks status in Jira.
                                    </div>
                                    <div class="message-time">4:30 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/9b59b6/ffffff?text=AT" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Sam</small>
                                    <div class="message-content">
                                        I'm stuck with that authentication bug. Anyone free to help?
                                    </div>
                                    <div class="message-time">4:35 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="message message-sent">
                            <div class="message-content">
                                I ran into that last week. It's an issue with the JWT token expiration. I'll send you my fix in a bit.
                            </div>
                            <div class="message-time">4:38 PM</div>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/9b59b6/ffffff?text=AT" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Sam</small>
                                    <div class="message-content">
                                        That would be awesome, thanks!
                                    </div>
                                    <div class="message-time">4:39 PM</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="text-center text-muted my-3">
                            <small>Today, 9:15 AM</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30/27ae60/ffffff?text=DT" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">Alex (Team Lead)</small>
                                    <div class="message-content">
                                        Don't forget our sprint planning in 45 minutes!
                                    </div>
                                    <div class="message-time">9:15 AM</div>
                                </div>
                            </div>
                        </div>
                    `;
                } else {
                    const now = new Date();
                    const timeStr = now.getHours().toString().padStart(2, '0') + ':' + 
                                     now.getMinutes().toString().padStart(2, '0');
                    
                    messageHtml = `
                        <div class="text-center text-muted mb-4">
                            <small>Today</small>
                        </div>
                        
                        <div class="message message-received">
                            <div class="d-flex align-items-start">
                                <img src="https://via.placeholder.com/30" alt="Contact Avatar" class="user-avatar me-2" style="width: 30px; height: 30px;">
                                <div>
                                    <small class="text-muted">${contactName}</small>
                                    <div class="message-content">
                                        Hey there! How are you doing today?
                                    </div>
                                    <div class="message-time">${timeStr}</div>
                                </div>
                            </div>
                        </div>
                    `;
                }
                
                $('#chat-messages').html(messageHtml);
                scrollToBottom();
            }
            
            scrollToBottom();
        });
    </script>
</body>
</html>
