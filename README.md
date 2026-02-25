[script.js](https://github.com/user-attachments/files/25547796/script.js)
// Mobile Navigation Toggle
const hamburger = document.querySelector('.hamburger');
const navMenu = document.querySelector('.nav-menu');

if (hamburger) {
    hamburger.addEventListener('click', () => {
        navMenu.classList.toggle('active');
        hamburger.classList.toggle('active');
    });

    // Close menu when clicking on a link
    document.querySelectorAll('.nav-menu a').forEach(link => {
        link.addEventListener('click', () => {
            navMenu.classList.remove('active');
            hamburger.classList.remove('active');
        });
    });
}

// Smooth scrolling for anchor links
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        }
    });
});

// Contact Form Handler
const contactForm = document.querySelector('.contact-form');
if (contactForm) {
    contactForm.addEventListener('submit', function(e) {
        e.preventDefault();
        
        // Get form data
        const formData = {
            name: document.getElementById('name').value,
            email: document.getElementById('email').value,
            phone: document.getElementById('phone').value,
            company: document.getElementById('company').value,
            product: document.getElementById('product').value,
            message: document.getElementById('message').value
        };

        // Here you would normally send the data to a server
        // For now, we'll just show a success message
        alert('شكراً لتواصلك معنا! سنرد عليك في أقرب وقت ممكن.');
        
        // Reset form
        contactForm.reset();
    });
}

// Scroll Animation for elements
const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
};

const observer = new IntersectionObserver(function(entries) {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.style.opacity = '1';
            entry.target.style.transform = 'translateY(0)';
        }
    });
}, observerOptions);

// Observe all cards and sections
document.addEventListener('DOMContentLoaded', () => {
    const elements = document.querySelectorAll('.product-card, .feature-card, .value-item, .product-card-full');
    elements.forEach(el => {
        el.style.opacity = '0';
        el.style.transform = 'translateY(20px)';
        el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
        observer.observe(el);
    });
});

// Navbar background change on scroll
window.addEventListener('scroll', () => {
    const navbar = document.querySelector('.navbar');
    if (window.scrollY > 100) {
        navbar.style.background = 'linear-gradient(135deg, rgba(15, 32, 39, 0.98) 0%, rgba(32, 58, 67, 0.98) 100%)';
        navbar.style.boxShadow = '0 4px 30px rgba(0,0,0,0.5)';
    } else {
        navbar.style.background = 'linear-gradient(135deg, #0f2027 0%, #203a43 100%)';
        navbar.style.boxShadow = '0 4px 20px rgba(0,0,0,0.3)';
    }
});

// Add active class to current page in navigation
const currentLocation = window.location.pathname.split('/').pop() || 'index.html';
const menuItems = document.querySelectorAll('.nav-menu a');

menuItems.forEach(item => {
    if (item.getAttribute('href') === currentLocation) {
        item.classList.add('active');
    }
});
