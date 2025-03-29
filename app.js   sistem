// Global variables
const TELEGRAM_BOT_TOKEN = '7868590635:AAG8j0WA-thE5mbAKHxDFu5bRcyzgi3E4dY';
const TELEGRAM_CHAT_ID = '7464909625';

// Initialize when document is ready
document.addEventListener('DOMContentLoaded', () => {
    // Add click handlers for sections
    document.querySelectorAll('[data-section]').forEach(button => {
        button.addEventListener('click', () => {
            const sectionId = button.getAttribute('data-section');
            showSection(sectionId);
        });
    });

    // Close sections when clicking outside
    document.querySelectorAll('.section').forEach(section => {
        section.addEventListener('click', (e) => {
            if (e.target === section) {
                hideSection(section.id);
            }
        });
    });

    // Prevent closing when clicking inside section content
    document.querySelectorAll('.section > div').forEach(content => {
        content.addEventListener('click', (e) => {
            e.stopPropagation();
        });
    });

    // Close button handlers
    document.querySelectorAll('[data-close-section]').forEach(button => {
        button.addEventListener('click', () => {
            const sectionId = button.getAttribute('data-close-section');
            hideSection(sectionId);
        });
    });
});

// Show section with animation
function showSection(sectionId) {
    const section = document.getElementById(sectionId);
    if (!section) return;

    // Hide any currently visible sections
    document.querySelectorAll('.section.active').forEach(activeSection => {
        if (activeSection !== section) {
            hideSection(activeSection.id);
        }
    });

    // Show the selected section
    section.classList.add('active');
    document.body.style.overflow = 'hidden';

    // If it's the appointment section, inject the form
    if (sectionId === 'appointment') {
        injectAppointmentForm();
    }

    // Animate content
    const content = section.querySelector('.max-w-4xl');
    if (content) {
        content.style.opacity = '0';
        content.style.transform = 'translateY(20px)';
        setTimeout(() => {
            content.style.transition = 'all 0.5s ease-out';
            content.style.opacity = '1';
            content.style.transform = 'translateY(0)';
        }, 50);
    }
}

// Hide section with animation
function hideSection(sectionId) {
    const section = document.getElementById(sectionId);
    if (!section) return;

    const content = section.querySelector('.max-w-4xl');
    if (content) {
        content.style.opacity = '0';
        content.style.transform = 'translateY(20px)';
    }

    setTimeout(() => {
        section.classList.remove('active');
        document.body.style.overflow = 'auto';
        if (content) {
            content.style.transition = '';
            content.style.opacity = '';
            content.style.transform = '';
        }
    }, 300);
}

// Show notification
function showNotification(message, isError = false) {
    const notification = document.createElement('div');
    notification.className = `fixed top-4 right-4 p-4 rounded-lg ${
        isError ? 'bg-red-500' : 'bg-green-500'
    } text-white max-w-md shadow-lg z-50 flex items-center gap-2 notification`;
    
    notification.innerHTML = `
        <i class="fas ${isError ? 'fa-exclamation-circle' : 'fa-check-circle'}"></i>
        <span>${message}</span>
    `;
    
    // Add animation styles
    notification.style.transform = 'translateY(-100%)';
    notification.style.opacity = '0';
    document.body.appendChild(notification);
    
    // Trigger animation
    setTimeout(() => {
        notification.style.transition = 'all 0.3s ease-out';
        notification.style.transform = 'translateY(0)';
        notification.style.opacity = '1';
    }, 50);
    
    // Remove notification
    setTimeout(() => {
        notification.style.transform = 'translateY(-100%)';
        notification.style.opacity = '0';
        setTimeout(() => notification.remove(), 300);
    }, 5000);
}

// Dynamically inject appointment form
function injectAppointmentForm() {
    const appointmentSection = document.getElementById('appointment');
    if (!appointmentSection.querySelector('form')) {
        const formContainer = document.createElement('div');
        formContainer.className = 'max-w-4xl mx-auto p-4';
        formContainer.innerHTML = `
            <div class="flex justify-between items-center mb-8">
                <h2 class="font-playfair text-3xl text-gold">Randevu Al</h2>
                <button onclick="hideSection('appointment')" class="text-gold hover:text-white transition-colors">
                    <i class="fas fa-times text-2xl"></i>
                </button>
            </div>
            <form id="appointmentForm" class="space-y-6 bg-black/50 p-6 rounded-lg border border-gold/20">
                <div class="input-group">
                    <label class="block mb-2 text-gold">
                        <i class="fas fa-user mr-2"></i>Ad Soyad
                    </label>
                    <input type="text" id="name" required 
                           class="w-full p-4 rounded bg-black/50 text-white border border-gold/20 focus:border-gold focus:outline-none"
                           placeholder="Adınız ve Soyadınız">
                </div>
                <div class="input-group">
                    <label class="block mb-2 text-gold">
                        <i class="fas fa-phone mr-2"></i>Telefon
                    </label>
                    <input type="tel" id="phone" required 
                           pattern="[0-9]{10}"
                           class="w-full p-4 rounded bg-black/50 text-white border border-gold/20 focus:border-gold focus:outline-none"
                           placeholder="5XX XXX XXXX">
                </div>
                <div class="input-group">
                    <label class="block mb-2 text-gold">
                        <i class="fas fa-cut mr-2"></i>Hizmet
                    </label>
                    <select id="service" required 
                            class="w-full p-4 rounded bg-black/50 text-white border border-gold/20 focus:border-gold focus:outline-none">
                        <option value="">Hizmet Seçiniz</option>
                        <option value="Manikür">Manikür - 250₺</option>
                        <option value="Pedikür">Pedikür - 300₺</option>
                        <option value="Saç Kesim">Saç Kesim - 250₺</option>
                        <option value="Komple Sir">Komple Sir - 600₺</option>
                        <option value="Bıyık Üstü">Bıyık Üstü - 50₺</option>
                        <option value="Kaş">Kaş - 100₺</option>
                        <option value="Kol Sir">Kol Sir - 200₺</option>
                        <option value="Dip Boyası">Dip Boyası - 500₺</option>
                        <option value="Saç Boyası">Saç Boyası - 700₺</option>
                        <option value="Keratin">Keratin - 1000₺</option>
                        <option value="Fön">Fön - 200₺</option>
                        <option value="Maşa">Maşa - 300₺</option>
                        <option value="Komple Yüz Alım">Komple Yüz Alım - 300₺</option>
                        <option value="Özel Bölge">Özel Bölge - 300₺</option>
                        <option value="Bacak Sir">Bacak Sir - 200₺</option>
                        <option value="Cilt Bakım">Cilt Bakım - 600₺</option>
                    </select>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="input-group">
                        <label class="block mb-2 text-gold">
                            <i class="fas fa-calendar mr-2"></i>Tarih
                        </label>
                        <input type="date" id="date" required 
                               class="w-full p-4 rounded bg-black/50 text-white border border-gold/20 focus:border-gold focus:outline-none">
                    </div>
                    <div class="input-group">
                        <label class="block mb-2 text-gold">
                            <i class="fas fa-clock mr-2"></i>Saat
                        </label>
                        <input type="time" id="time" required 
                               min="09:00" max="20:00"
                               class="w-full p-4 rounded bg-black/50 text-white border border-gold/20 focus:border-gold focus:outline-none">
                        <p class="text-sm text-gray-400 mt-1">Çalışma Saatleri: 09:00 - 20:00</p>
                    </div>
                </div>
                <button type="submit" 
                        class="w-full bg-gold text-black p-4 rounded-lg hover:bg-opacity-90 transition text-lg font-semibold flex items-center justify-center gap-2">
                    <i class="fas fa-calendar-check"></i>
                    Randevu Oluştur
                </button>
            </form>
        `;
        
        appointmentSection.appendChild(formContainer);
        initializeAppointmentForm();
    }
}

// Initialize form
function initializeAppointmentForm() {
    const form = document.getElementById('appointmentForm');
    const dateInput = document.getElementById('date');
    const phoneInput = document.getElementById('phone');

    // Set minimum date to today
    const today = new Date().toISOString().split('T')[0];
    dateInput.min = today;

    // Format phone number
    phoneInput.addEventListener('input', (e) => {
        let value = e.target.value.replace(/\D/g, '');
        if (value.length > 10) value = value.slice(0, 10);
        e.target.value = value;
    });

    // Form submission
    form.addEventListener('submit', handleAppointmentSubmission);
}

// Handle form submission
async function handleAppointmentSubmission(e) {
    e.preventDefault();
    
    const form = e.target;
    const submitButton = form.querySelector('button[type="submit"]');
    const originalButtonText = submitButton.innerHTML;
    
    const formData = {
        name: form.name.value.trim(),
        phone: form.phone.value.trim(),
        service: form.service.value,
        date: form.date.value,
        time: form.time.value
    };
    
    if (!validateForm(formData)) return;
    
    submitButton.disabled = true;
    submitButton.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Gönderiliyor...';
    
    try {
        const formattedDate = new Date(formData.date).toLocaleDateString('tr-TR', {
            year: 'numeric',
            month: 'long',
            day: 'numeric',
            weekday: 'long'
        });

        const message = `
🆕 Yeni Randevu!

👤 Müşteri: ${formData.name}
📞 Telefon: ${formData.phone}
💇‍♀️ Hizmet: ${formData.service}
📅 Tarih: ${formattedDate}
⏰ Saat: ${formData.time}
        `;

        const response = await fetch(`https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                chat_id: TELEGRAM_CHAT_ID,
                text: message,
                parse_mode: 'HTML'
            })
        });

        if (!response.ok) throw new Error('Telegram API error');

        showNotification('Randevunuz başarıyla oluşturuldu! Size en kısa sürede dönüş yapılacaktır.');
        form.reset();
        hideSection('appointment');

    } catch (error) {
        console.error('Error:', error);
        showNotification('Randevu oluşturulurken bir hata oluştu. Lütfen daha sonra tekrar deneyin.', true);
    } finally {
        submitButton.disabled = false;
        submitButton.innerHTML = originalButtonText;
    }
}

// Validate form
function validateForm(data) {
    const errors = [];
    
    if (data.name.length < 3) {
        errors.push('İsim en az 3 karakter olmalıdır');
    }
    
    if (!/^5[0-9]{9}$/.test(data.phone)) {
        errors.push('Geçerli bir telefon numarası giriniz (5XX XXX XXXX)');
    }
    
    if (!data.service) {
        errors.push('Lütfen bir hizmet seçiniz');
    }
    
    const selectedDate = new Date(data.date);
    const today = new Date();
    today.setHours(0, 0, 0, 0);
    
    if (selectedDate < today) {
        errors.push('Geçmiş bir tarih seçemezsiniz');
    }
    
    const [hours, minutes] = data.time.split(':').map(Number);
    if (hours < 9 || (hours === 20 && minutes > 0) || hours > 20) {
        errors.push('Randevu saati 09:00 - 20:00 arasında olmalıdır');
    }
    
    if (errors.length > 0) {
        errors.forEach(error => showNotification(error, true));
        return false;
    }
    
    return true;
}

// Make functions globally available
window.showSection = showSection;
window.hideSection = hideSection;